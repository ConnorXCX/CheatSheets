# Hadoop Cheat Sheet

## High-Level Hadoop Ecosystem

1. [Core Hadoop Ecosystem](#core-hadoop-ecosystem)
1. [Query Engines](#query-engines)
1. [External Data Storage](#external-data-storage)

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

1. **Spark**: In-Memory data processing
1. **PIG** & **HIVE**: Query based processing of data services
1. **HBase**: NoSQL Database
1. **Mahout** & **Spark MLLib**: Machine Learning algorithm libraries
1. **Solar** & **Lucene**: Searching and Indexing
1. **Zookeeper**: Managing cluster
1. **Oozie**: Job Scheduling

## Query Engines

TBD

## External Data Storage

TBD

## References

1. [The Ultimate Hands-On Hadoop: Tame your Big Data!](https://www.udemy.com/share/101WBO3@GCG2h3kBLhu73Y-V994-4JkSTpSCM14zNlm_65RR0VfN97hBx87P8CT48KmyrX_D_Q==/)
1. [Hadoop Ecosystem](https://www.geeksforgeeks.org/hadoop-ecosystem/)
