# Apache Spark on Kubernetes Project: WordCount + PageRank

## Overview

This project demonstrates the deployment and utilization of Apache Spark on a Kubernetes cluster, 
showcasing its capability to handle large-scale data processing tasks efficiently. By leveraging 
Kubernetes orchestration, the project aims to optimize resource utilization, enhance scalability, 
and provide a robust platform for running distributed data analytics applications.

## Features

- **Cluster Setup:** Utilizes Google Kubernetes Engine (GKE) to create and manage a Kubernetes
                     cluster tailored for Apache Spark workloads.
  
- **NFS Server Provisioner:** Implements a stable NFS server provisioner via Helm to provide shared,
                              persistent storage across Spark nodes, ensuring data consistency and accessibility.

- **Application Deployment:** Deploys Apache Spark using Bitnami's Helm chart, simplifying the setup
                              and configuration of Spark components on the Kubernetes cluster.

- **Advanced Analytics:** Demonstrates the execution of advanced analytics tasks such as the PageRank
                          algorithm using PySpark, showcasing the platform's capability for complex computations.

- **Monitoring and Logging:** Integrates Prometheus for cluster monitoring and Grafana for visualization,
                              along with centralized logging for Spark job analysis and troubleshooting.

- **Security Measures:** Implements Kubernetes Network Policies, Secrets management, and SSL/TLS encryption
                         to enhance data security and compliance.

- **CI/CD Pipeline:** Utilizes Docker for containerization of Spark applications and establishes a CI/CD
                      pipeline for automated testing, building, and deployment, enhancing development efficiency
                      and deployment reliability.

## Usage

### Prerequisites

- Google Cloud Platform (GCP) account with access to Google Kubernetes Engine (GKE).
- Helm installed on your local machine for managing Kubernetes applications.

### Deployment Steps

1. **Cluster Creation:**
   - Create a Kubernetes cluster on GKE using `gcloud` with appropriate node configurations.

2. **NFS Server Provisioner:**
   - Install NFS Server Provisioner via Helm to enable persistent storage for Spark jobs.

3. **Spark Deployment:**
   - Deploy Apache Spark using Bitnami's Helm chart, specifying configurations for Spark components
     and resource allocation.

4. **Data Processing Tasks:**
   - Copy application JAR files and input data to the PersistentVolumeClaim (PVC) mounted by Spark pods.

5. **Execute Spark Jobs:**
   - Submit Spark jobs (e.g., WordCount, PageRank) using `spark-submit`, specifying input data paths and
     job parameters.

6. **Monitoring and Analysis:**
   - Monitor cluster health and performance metrics using Prometheus and Grafana. Analyze Spark job logs
     for debugging and performance tuning.

### Future Enhancements

- Implement auto-scaling policies for Spark worker nodes based on workload metrics.
- Enhance fault tolerance with Kubernetes StatefulSets and Spark checkpointing.
- Explore integration with additional analytics tools and machine learning frameworks.

## Conclusion

This project underscores the capability of Apache Spark on Kubernetes to efficiently handle complex data 
processing tasks at scale. By leveraging Kubernetes' orchestration capabilities and Spark's powerful analytics 
engine, organizations can achieve enhanced resource efficiency, scalability, and security in their big data 
analytics pipelines.

## Author

Natnael Haile
