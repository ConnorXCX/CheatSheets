# Hadoop Cheat Sheet

## Contents

#### [High-Level Hadoop Ecosystem](#high-level-hadoop-ecosystem-1)

1. [Core Hadoop Ecosystem](#core-hadoop-ecosystem)
1. [External Data Storage](#external-data-storage)
1. [Query Engines](#query-engines)

#### [HDFS](#hdfs-1)

1. [Overview](#overview)
1. [Architecture](#architecture)
1. [Using HDFS](#using-hdfs)

#### [MapReduce](#mapreduce-1)

1. []()

#### [References](#references-1)

## High-Level Hadoop Ecosystem

### Core Hadoop Ecosystem

#### Native to Hadoop

1. **HDFS** (Hadoop Distributed File System)
1. **YARN** (Yet Another Resource Negotiator)
   1. **Resource Manager**: privilege of allocating resource for the applications.
   1. **Nodes Manager**: allocates resources such as CPU, memory, and bandwidth per machine.
   1. **Application Manager**: interface between the Resource Manager and Node Manager.
1. **MapReduce** (programming based data processing)
   - **Mappers**: transform data in parallel across cluster
   - **Reducers**: aggregate data

#### Hadoop Common Utilities

1. **Spark**: in-memory data processing with scripts written in Python, Java, or Scala programming languages
1. **PIG** & **HIVE**: SQL-like query based processing of data services
1. **TEZ**: allows for a complex directed-acyclic-graph of tasks for processing data
1. **HBase**: NoSQL database; columnar data store; fast database for very large transaction rates (OLTP type transactions)
1. **Storm**: processing steaming data in real-time
1. **Oozie**: job scheduling
1. **Zookeeper**: managing and coordinating cluster; track up / down nodes; track shared states across cluster
1. **Mahout** & **Spark MLLib**: machine learning algorithm libraries
1. **Solr** & **Lucene**: searching and indexing
1. **Mesos**
1. **Ambari**

#### Hadoop Data Ingestion Utilities

1. **Kafka**: general purpose pipelines to publish data from various sources into Hadoop cluster
1. **Sqoop**: connector between Hadoop and legacy databases
1. **Flume**: transporting web logs at large-scale into Hadoop cluster

### External Data Storage

#### Relational Data Stores

1. **MySQL**

#### Non-Relational Data Stores

1. **Cassandra**: columnar data store like HBase; good for real-time applications; key-value data pairs
1. **MongoDB**: columnar data store like HBase; good for real-time applications; key-value data pairs

### Query Engines

1. **Drill**: write SQL queries that can work across a wide-range of NoSQL databases and compile data across disparate data stores
1. **Hue**
1. **Phoenix**: similar to Drill, but gives ACID guarantees and OLTP
1. **Presto**
1. **Zeppelin**: notebook approach to interacting with cluster

## HDFS

### Overview

- Good at handling very large files
- Breaks files into blocks; 128 MB default
- Distributes processing of large files across blocks, enabling parallel processing
- Stored across several commodity computers, with multiple distributed copies for redundancy and backup

### Architecture

#### Name Node

- single node that keeps track of where all blocks live by essentially keeping a table of directories and file names to find all associated blocks for a given file
- maintains an edit log to track what's been created, modified, and where things are stored

#### Data Nodes

- stores each block of each file
- talk to each other to maintain copies and replication of blocks
- ultimately what client application talks to once the Name Node is queried

#### Client Node

- entry point; client application
- usually exists as a client library or client API
- queries Name Node, then Data Nodes

### Using HDFS

1. UI (Ambari)
1. CLI
1. HTTP / HDFS Proxies
1. Java interface
1. NFS Gateway

## MapReduce

## References

1. [The Ultimate Hands-On Hadoop: Tame your Big Data!](https://www.udemy.com/share/101WBO3@GCG2h3kBLhu73Y-V994-4JkSTpSCM14zNlm_65RR0VfN97hBx87P8CT48KmyrX_D_Q==/)
1. [Hadoop Ecosystem](https://www.geeksforgeeks.org/hadoop-ecosystem/)
