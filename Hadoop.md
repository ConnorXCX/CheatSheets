# Hadoop Cheat Sheet

## High-Level Hadoop Ecosystem

1. [Core Hadoop Ecosystem](#core-hadoop-ecosystem)
1. [External Data Storage](#external-data-storage)
1. [Query Engines](#query-engines)

## Core Hadoop Ecosystem

### Native to Hadoop

1. **HDFS** (Hadoop Distributed File System)
1. **YARN** (Yet Another Resource Negotiator)
   1. **Resource Manager**: privilege of allocating resource for the applications.
   1. **Nodes Manager**: allocates resources such as CPU, memory, and bandwidth per machine.
   1. **Application Manager**: interface between the Resource Manager and Node Manager.
1. **MapReduce** (Programming based Data Processing)
   - **Mappers**: transform data in parallel across cluster
   - **Reducers**: aggregate data

### Hadoop Common Utilities

1. **Spark**: in-memory data processing with scripts written in Python, Java, or Scala programming languages
1. **PIG** & **HIVE**: SQL-like query based processing of data services
1. **TEZ**: allows for a complex directed-acyclic-graph of tasks for processing data
1. **HBase**: NoSQL database; columnar data store; fast database for very large transaction rates (OLTP type transactions)
1. **Storm**: processing steaming data in real-time
1. **Oozie**: job scheduling
1. **Zookeeper**: managing and coordinating cluster; track up / down nodes; track shared states across cluster
1. **Mahout** & **Spark MLLib**: machine learning algorithm libraries
1. **Solar** & **Lucene**: searching and indexing

### Hadoop Data Ingestion Utilities

1. **Kafka**: general purpose pipelines to publish data from various sources into Hadoop cluster
1. **Sqoop**: connector between Hadoop and legacy databases
1. **Flume**: transporting web logs at large-scale into Hadoop cluster

## External Data Storage

Relational Data Stores:

1. **MySQL**

Non-Relational Data Stores:

1. **Cassandra**: columnar data store like HBase; good for real-time applications
1. **MongoDB**: columnar data store like HBase; good for real-time applications

## Query Engines

TBD

## References

1. [The Ultimate Hands-On Hadoop: Tame your Big Data!](https://www.udemy.com/share/101WBO3@GCG2h3kBLhu73Y-V994-4JkSTpSCM14zNlm_65RR0VfN97hBx87P8CT48KmyrX_D_Q==/)
1. [Hadoop Ecosystem](https://www.geeksforgeeks.org/hadoop-ecosystem/)
