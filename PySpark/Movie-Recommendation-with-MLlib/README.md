# Movie Recommendation System with PySpark MLlib - Collaborative Filtering (Implementation-2)

## Overview

This project implements a movie recommendation system using PySpark's MLlib library for collaborative filtering. 
The system leverages the Alternating Least Squares (ALS) algorithm to provide personalized movie recommendations 
based on user ratings.

## Introduction

This project aims to develop a scalable and efficient movie recommendation system using collaborative filtering. 
By leveraging user-movie rating data, the system can generate personalized recommendations for users.

## Objectives

- Develop a movie recommendation system using PySpark's MLlib.
- Load, transform, and prepare the rating data for analysis.
- Train and evaluate a collaborative filtering model using the ALS algorithm.
- Deploy the model on Google Cloud Platform using Dataproc for scalable processing.
- Save and manage the trained model in Google Cloud Storage for future use.

## Data Preparation

1. **Load Data:**
   - Obtain the file `u.data`.

2. **Transform Data:**
   - Create a bash script `transform_data.sh` to preprocess the data:
     ```bash
     #!/bin/bash
     cat u.data | while read userid movieid rating timestamp
     do
        echo "${userid},${movieid},${rating}"
     done > u_transformed_data.csv
     ```
   - Make the script executable and run it:
     ```bash
     chmod +x transform_data.sh
     ./transform_data.sh
     ```

## Cloud Storage Setup

1. **Create a Cloud Storage Bucket:**
   - Use `gsutil` to create a new bucket:
     ```bash
     gsutil mb gs://big_data_movie_recommendation
     ```

2. **Upload Transformed Data:**
   - Upload the transformed data to the bucket:
     ```bash
     gsutil cp u_transformed_data.csv gs://big_data_movie_recommendation
     ```

## Model Implementation

1. **Create PySpark Script:**
   - Write a PySpark script `recommendation_example.py` to perform collaborative filtering using ALS:
     ```python
     from pyspark.sql import SparkSession
     from pyspark.ml.recommendation import ALS
     from pyspark.ml.evaluation import RegressionEvaluator

     # Initialize Spark Session
     spark = SparkSession.builder \
         .appName("Movie Recommendation") \
         .getOrCreate()

     # Load data
     ratings = spark.read.csv("gs://big_data_movie_recommendation/u_transformed_data.csv", 
                              header=False, inferSchema=True) \
         .toDF("userId", "movieId", "rating")

     # Split data into training and test sets
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
     model.save("gs://big_data_movie_recommendation/als_model")
     ```

2. **Upload PySpark Script:**
   - Upload the script to the bucket:
     ```bash
     gsutil cp recommendation_example.py gs://big_data_movie_recommendation
     ```

## Running the Project

1. **Create Dataproc Cluster:**
   - Create a single-node Dataproc cluster:
     ```bash
     gcloud dataproc clusters create spark-cluster \
         --region us-west1 \
         --zone us-west1-a \
         --single-node
     ```

2. **Submit PySpark Job:**
   - Submit the PySpark job to the cluster:
     ```bash
     gcloud dataproc jobs submit pyspark gs://big_data_movie_recommendation/recommendation_example.py \
         --cluster spark-cluster \
         --region us-west1
     ```

---

Feel free to contribute and raise issues if you encounter any problems or have suggestions for improvements.

---

## Author

Natnael Haile
