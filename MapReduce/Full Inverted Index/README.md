# Hadoop MapReduce Full Inverted Index Calculation

## Overview

This repository contains the code and documentation for a Hadoop MapReduce job designed to calculate a full inverted index from a set of input text files. The inverted index maps words to their occurrences in the input files, enabling efficient full-text searches.

## Setup Instructions

1. **Create Directories in HDFS**:
   - Navigate to the Hadoop home directory.
   - Create necessary directories in HDFS using the provided commands.

2. **Verify Directory Creation**:
   - Ensure the input directory is created and initially empty.

3. **Create the Input Files**:
   - Create input files with sample text data as per the provided guidelines.

4. **Upload Input Files to HDFS**:
   - Use the provided commands to upload input files to the specified directory in HDFS.

5. **Compile Java Code**:
   - Navigate to the directory containing Java source files.
   - Compile the Java code using the provided command.

6. **Create JAR File**:
   - Create a JAR file containing all compiled classes using the provided command.

7. **Submit and Run the Job**:
   - Navigate to the Hadoop home directory.
   - Run the MapReduce job with the created JAR file using the provided command.

8. **Verify Output**:
   - Check the output directory for the generated inverted index using the provided command.

## Mapper and Reducer Design

- The Mapper component tokenizes input lines into words and emits word-document pairs.
- The Reducer component aggregates word-document pairs to form the inverted index.

Detailed Mapper and Reducer design and example outputs are provided in the documentation.

## Enhancement Ideas

- Optimizing Mapper Output
- Improving Reducer Efficiency
- Handling Large Input Files
- Enhancing Scalability

## Conclusion

- Successful Implementation
- Scalability and Flexibility
- Continuous Improvement
- Future Deployments and Exploration

## Author

- Natnael Haile
