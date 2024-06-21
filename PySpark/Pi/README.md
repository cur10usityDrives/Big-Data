# Calculating Pi Using Hadoop and PySpark

This project demonstrates how to calculate the value of Pi using both the Hadoop framework and PySpark. 
While Hadoop is generally used for large-scale data processing, this project serves as a practical example 
to explore its capabilities and understand its functionality through a computationally intensive task. 
Additionally, PySpark is utilized to highlight its efficiency and versatility in handling similar tasks.

## Introduction

In this project, our objective is to calculate the value of Pi using Hadoop and PySpark. 
Although Hadoop is typically not ideal for computationally intensive tasks, this exercise serves as a 
practical application to understand and utilize Hadoop's capabilities through a hands-on example. 
By also incorporating PySpark, we will explore its framework and potential in handling large-scale data 
processing and computational tasks.

## Design

### Pi Concept

To estimate the value of Pi, we will use a Monte Carlo method. In this approach, we will throw N darts at a square dartboard. Each dart lands at a random position (x, y) within the square.

To determine whether a dart has landed inside the circle inscribed within the square, we use the equation of a circle. Specifically, a dart is inside the circle if the condition (x^2 + y^2 < r^2) is satisfied, where r is the radius of the circle. By calculating the ratio of darts that land inside the circle to the total number of darts thrown, we can approximate the value of Pi.

### Calculating Pi: Process Design

1. Generate Random Coordinates: Generate random (x, y) coordinates within a square.
2. Mapping Points: Map each (x, y) pair to a result, determining if the point lies inside the circle (assign 1) or outside (assign 0).
3. Counting Points: Count the number of points that fall inside the circle.
4. Summing Values: Sum up the values to determine the proportion of points inside the circle, which will be used to approximate the value of Pi.

## Implementation

### Hadoop MapReduce Implementation

The project is implemented using Hadoop's MapReduce framework. Below are the key components:

- **Mapper:** Generates random points and maps each point to 1 if inside the circle, or 0 if outside.
- **Reducer:** Sums the values from the mapper to count the points inside the circle.
- **Driver:** Manages the MapReduce job, coordinates the mapper and reducer, and calculates Pi based on the output.

### PySpark Implementation

In addition to Hadoop, we implement the Pi calculation using PySpark, leveraging its in-memory processing 
capabilities for better performance.

## Conclusion

A crucial aspect of this algorithm is ensuring that points are randomly and uniformly distributed, 
meaning each point within the designated area must have an equal chance of being selected. 
The accuracy of the calculated value of Pi improves as the number of random points increases. 
By leveraging a larger dataset, the approximation of Pi becomes more precise.

## Requirements

- Hadoop 2.x or later
- Java 8 or later
- PySpark

## Author

Natnael Haile
