# Calculating Pi Using Hadoop

This project demonstrates how to calculate the value of Pi using the Hadoop framework. While Hadoop is generally used for large-scale data processing, this project serves as a practical example to explore its capabilities and understand its functionality through a computationally intensive task.

## Table of Contents

- [Introduction](#introduction)
- [Design](#design)
- [Implementation](#implementation)
- [Conclusion](#conclusion)
- [How to Run](#how-to-run)
- [Requirements](#requirements)
- [License](#license)

## Introduction

In this project, our objective is to calculate the value of Pi using Hadoop. Although Hadoop is typically not ideal for computationally intensive tasks, this exercise serves as a practical application to understand and utilize Hadoop's capabilities through a hands-on example. By undertaking this project, we will explore Hadoop's framework and its potential in handling large-scale data processing.

## Design

### Pi Concept:

To estimate the value of Pi, we will use a Monte Carlo method. In this approach, we will throw N darts at a square dartboard. Each dart lands at a random position (x, y) within the square. 

To determine whether a dart has landed inside the circle inscribed within the square, we use the equation of a circle. Specifically, a dart is inside the circle if the condition \( x^2 + y^2 < r^2 \) is satisfied, where \( r \) is the radius of the circle. By calculating the ratio of darts that land inside the circle to the total number of darts thrown, we can approximate the value of Pi.

### Calculating Pi: Process Design

1. **Generate Random Coordinates:** Generate random \((x, y)\) coordinates within a square.
2. **Mapping Points:** Map each \((x, y)\) pair to a result, determining if the point lies inside the circle (assign 1) or outside (assign 0).
3. **Counting Points:** Count the number of points that fall inside the circle.
4. **Summing Values:** Sum up the values to determine the proportion of points inside the circle, which will be used to approximate the value of Pi.

## Implementation

The project is implemented using Hadoop's MapReduce framework. Below are the key components:

1. **Mapper:** Generates random points and maps each point to 1 if inside the circle, or 0 if outside.
2. **Reducer:** Sums the values from the mapper to count the points inside the circle.
3. **Driver:** Manages the MapReduce job, coordinates the mapper and reducer, and calculates Pi based on the output.

### Code Structure

- `~/hadoop-3.4.0-src/`
  - `PiCalculation.java`
- `~/PiCalculate/`
  - `GenerateRandomNumbers.java`
- `/user/nhaile96456/picalculate/input`
  - Sample input data if applicable
- `/user/nhaile96456/picalculate/output/`
  - Directory for output data

## Conclusion

A crucial aspect of this algorithm is ensuring that points are randomly and uniformly distributed, meaning each point within the designated area must have an equal chance of being selected. The accuracy of the calculated value of Pi improves as the number of random points increases. By leveraging a larger dataset, the approximation of Pi becomes more precise.

## How to Run

1. **Set Up Hadoop:**
   - Ensure Hadoop is installed and configured on your system.
   - Start the Hadoop Distributed File System (HDFS) and the MapReduce framework.

2. **Compile the Code:**
   - Navigate to the `~/PiCalculate/` directory.
   - Compile the Java file using the following command:
     ```sh
     javac GenerateRandomNumbers.java
     ```
   - Return 1000000 and 200 for the random numbers and radius prompts.
   - Then navigate to the `~/hadoop-3.4.0-src/` directory.
   - Execute the following lines of code:
     ```sh
     $ bin/hdfs dfs -mkdir /user
     $ bin/hdfs dfs -mkdir /user/nhaile96456
     $ bin/hdfs dfs -mkdir /user/nhaile96456/picalculate
     $ bin/hdfs dfs -mkdir /user/nhaile96456/picalculate/input
     $ bin/hdfs/dfs -put ../PiCalculation/PiCalculationInput /user/nhaile96456/picalculate/input
     ```
   - Compile the Java file using the following command:
     ```sh
     javac PiCalculation.java
     ```


4. **Create JAR File:**
   - Package the compiled classes into a JAR file:
     ```sh
     jar cf wc.jar PiCalculation*class
     ```

5. **Run the Job:**
   - Submit the MapReduce job using the provided command:
     ```sh
     $ bin/hadoop jar pi-calculation.jar PiCalculation /user/nhaile96456/picalculate/input /user/nhaile96456/picalculate/output
     ```

6. **View Results:**
   - List the output directory:
     ```sh
     $ bin/hdfs dfs -ls /user/nhaile96456/picalculate/output
     ```
   - Display the result:
     ```sh
     $ bin/hdfs dfs -cat /user/nhaile96456/picalculate/output/part-r-00000
     ```

## Requirements

- Hadoop 2.x or later
- Java 8 or later

## Author

- Natnael Haile
