# Movie Recommendation System with PySpark MLlib - Collaborative Filtering (Implementation-3)

## Overview

This project implements a movie recommendation system using PySpark's MLlib library for collaborative filtering. 

## Introduction

This project focuses on developing a scalable movie recommendation system using collaborative filtering with PySpark's MLlib. 
The system processes user and movie data to generate personalized recommendations.

## Data Preparation

1. **Prepare Data Files:**
   - Ensure you have the following files: `movies.csv`, `ratings.csv`, and `recommendation_engine.py`.

## Cloud Storage Setup

1. **Upload Data and Scripts to GCS:**
   - Upload the data files and PySpark script to your GCS bucket named `machine_learning_pro`:
     ```bash
     gsutil cp movies.csv gs://machine_learning_pro
     gsutil cp ratings.csv gs://machine_learning_pro
     gsutil cp recommendation_engine.py gs://machine_learning_pro
     ```

## Cluster Configuration

1. **Create the Dataproc Cluster:**
   - Create a Dataproc cluster with the desired configuration:
     ```bash
     gcloud dataproc clusters create spark-cluster-ml \
         --region us-west1 \
         --zone us-west1-a \
         --master-machine-type n1-standard-4 \
         --worker-machine-type n1-standard-4 \
         --num-workers 2
     ```

## Model Implementation

1. **Create PySpark Script:**
   - Your PySpark script (`recommendation_engine.py`) should implement the ALS algorithm to perform collaborative filtering.
   - Ensure it takes GCS paths as inputs:
     ```python
     from pyspark.sql import SparkSession
     from pyspark.ml.recommendation import ALS
     from pyspark.ml.evaluation import RegressionEvaluator

     # Initialize Spark Session
     spark = SparkSession.builder \
         .appName("Movie Recommendation") \
         .getOrCreate()

     # Load data
     movies = spark.read.csv("gs://machine_learning_pro/movies.csv", header=True, inferSchema=True)
     ratings = spark.read.csv("gs://machine_learning_pro/ratings.csv", header=True, inferSchema=True)

     # Prepare data for ALS
     (training, test) = ratings.randomSplit([0.8, 0.2])

     # Initialize ALS model
     als = ALS(userCol="userId", itemCol="movieId", ratingCol="rating", coldStartStrategy="drop")
     model = als.fit(training)

     # Make predictions
     predictions = model.transform(test)

     # Evaluate the model
     evaluator = RegressionEvaluator(metricName="rmse", labelCol="rating", predictionCol="prediction")
     rmse = evaluator.evaluate(predictions)

     print("Root-mean-square error = " + str(rmse))

     # Save the model
     model.save("gs://machine_learning_pro/als_model")
     ```

## Running the Project

1. **Submit the PySpark Job:**
   - Submit your PySpark job to the Dataproc cluster, specifying the GCS paths for the input files:
     ```bash
     gcloud dataproc jobs submit pyspark gs://machine_learning_pro/recommendation_engine.py \
         --cluster=spark-cluster-ml \
         --region=us-west1 \
         -- \
         --input_path_movies=gs://machine_learning_pro/movies.csv \
         --input_path_ratings=gs://machine_learning_pro/ratings.csv
     ```

## Conclusion

This project successfully demonstrates a movie recommendation system using PySpark's MLlib. 
The system provides personalized recommendations and is designed for scalability using Google Cloud Platform. 
Future work includes enhancing the recommendation model, integrating real-time processing, and optimizing evaluation metrics.

---

## Author

Natnael Haile
