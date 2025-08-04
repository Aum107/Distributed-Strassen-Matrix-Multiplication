# Fast and Scalable Strassen’s Matrix Multiplication Using Apache Spark

This repository contains the implementation and results for our distributed version of **Strassen’s Matrix Multiplication Algorithm**, optimized for **Apache Spark**. The project demonstrates how recursive matrix multiplication can be efficiently performed at scale in a distributed computing environment using metadata-driven partitioning, in-memory processing, and communication-aware design.

## 📘 Overview

Traditional matrix multiplication has a computational complexity of **O(n³)**, which becomes computationally expensive for large matrices. **Strassen’s algorithm** improves this to **O(n^2.81)** using a divide-and-conquer strategy. However, implementing Strassen’s algorithm in distributed systems is challenging due to its recursive nature and the overhead of data communication.

This project addresses these challenges and presents a scalable implementation on Apache Spark that:

- Reduces computation time using Strassen’s method.
- Minimizes communication overhead via metadata replication and smart partitioning.
- Outperforms classical distributed libraries such as Spark MLlib for large-scale matrix sizes.

## 📊 Theoretical & Numerical Insights

- **Time Complexity**: Stark achieves a theoretical cost of **O(N^log₂(7))**, faster than the classical **O(N³)** approach.
- **Memory Usage**: Grows as **3ˡ·N²**, where `l` is the recursion depth and `N` is the matrix size.
- **Communication Efficiency**: Achieved by controlling inter-node data transfer through recursion-aware partitioning.

### Key Observations:
- At **4096 × 4096**, Stark showed a **20–30% performance improvement** over MLlib.
- Runtime followed a **U-shaped curve** with respect to the number of partitions: too few increases computation load; too many increases communication overhead.
- Most runtime was concentrated in the **division** and **leaf-node multiplication** stages of recursion.

## 🛠️ Tech Stack

- **Apache Spark**
- **PySpark / Scala (depending on branch)**
- **Parquet** (for matrix storage)
- **NumPy** (for baseline comparison)

## 🧪 Dataset

Randomly generated dense square matrices of dimensions:
- 512 × 512
- 1024 × 1024
- 2048 × 2048
- 4096 × 4096

These matrices are stored in Parquet format for compatibility with Spark.

