# PageRank Algorithm Implementation using PySpark and Scala on Google Cloud Dataproc

## Overview

This project implements the PageRank algorithm using Apache Spark, specifically using PySpark and Scala, 
deployed on Google Cloud Platform (GCP) using Google Cloud Dataproc. PageRank is a link analysis algorithm 
used by Google to rank web pages in their search engine results. This implementation showcases the scalability 
and efficiency of distributed computing for large-scale data processing tasks.

## Project Structure

The project is structured as follows:

- **Input Data:** The input data (`input.txt`) consists of web page links formatted for the PageRank algorithm.
- **Scripts:**
  - `pagerank.py`: Python script for implementing PageRank using PySpark.
  - `ScalaPageRank.scala`: Scala code for implementing PageRank using Scala and submitting as a Spark job.
- **Setup and Configuration:**
  - **Google Cloud Storage:** Used to store input data and scripts.
  - **Google Cloud Dataproc:** Managed Spark service used to create and manage the cluster for executing Spark jobs.

## Deployment

### Google Cloud Dataproc Cluster Setup

To deploy the project, follow these steps:

1. **Create a Dataproc Cluster:**
   ```bash
   gcloud dataproc clusters create pagerank-cluster \
       --region=us-central1 \
       --zone=us-central1-a \
       --single-node \
       --master-machine-type=n1-standard-4 \
       --master-boot-disk-size=50GB \
       --image-version=1.5-debian10
   ```

2. **Upload Data and Scripts:**
   - Upload `input.txt`, `pagerank.py`, and `ScalaPageRank.scala` to a Google Cloud Storage bucket
     (`gs://your-bucket-name`).

3. **Submit PySpark Job:**
   ```bash
   gcloud dataproc jobs submit pyspark gs://your-bucket-name/pagerank.py \
       --cluster=pagerank-cluster \
       --region=us-central1 \
       -- gs://your-bucket-name/input.txt 10
   ```

4. **Submit Scala Job:**
   ```bash
   gcloud dataproc jobs submit spark --cluster=pagerank-cluster --region=us-central1 \
   --jars=gs://your-bucket-name/sparkpagerank_2.12-1.0.jar --class=org.apache.spark.examples.SparkPageRank \
   -- gs://your-bucket-name/input.txt 10
   ```

### Architecture and Design

The project architecture involves setting up a Dataproc cluster to execute Spark jobs. Both PySpark and 
Scala implementations leverage Spark's capabilities for distributed computation. The PageRank algorithm 
computes the importance of web pages based on their inbound links, iterating until convergence to determine 
final page ranks.

### Enhancement Ideas

To further improve the project, consider these enhancements:

- **Scalability Improvements:** Optimize the algorithm and cluster configurations for handling larger datasets.
- **Algorithmic Enhancements:** Experiment with variations of PageRank (e.g., weighted PageRank) for better relevance.
- **User Interface:** Develop a frontend to visualize PageRank results and provide interactive analysis tools.
- **Monitoring and Logging:** Integrate robust monitoring and logging to track performance and diagnose issues.

### Conclusion

This project successfully demonstrates the implementation of the PageRank algorithm using PySpark and Scala on 
Google Cloud Dataproc, showcasing the capabilities of distributed computing for large-scale data processing tasks. 
It provides a foundation for further exploration into optimizing algorithms and leveraging cloud infrastructure 
for scalable data analytics.

## Author

Natnael Haile
