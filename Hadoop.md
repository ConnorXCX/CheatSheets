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

1. [Overview](#overview-1)
1. [Mapper](#mapper)
1. [Shuffle & Sort](#shuffle--sort)
1. [Reducer](#reducer)

#### [Spark](#spark-1)

1. [Overview](#overview-2)
1. [Scalability](#scalability)
1. [Component Library](#component-library)
1. [Resilient Distributed Dataset (RDD)](#resilient-distributed-dataset-rdd)
1. [Streaming](#streaming)

#### [YARN](#yarn-1)

1. [Overview](#overview-3)

#### [Kafka](#kafka-1)

1. [Overview](#overview-4)

#### [Flink](#flink-1)

1. [Overview](#overview-5)

#### [Relational Data Stores with Hadoop](#relational-data-stores-with-hadoop-1)

1. [Hive](#hive)
1. [MySQL](#mysql)

#### [Non-Relational Data Stores with Hadoop](#non-relational-data-stores-with-hadoop-1)

1. [HBase](#hbase)
1. [Cassandra](#cassandra)
1. [MongoDB](#mongodb)

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

### Overview

- distributes the processing of data on your cluster
- divides data into partitions that are mapped (transformed) and reduced (aggregated) by the mapper and reducer functions you design
- resilient to failure; an application master monitors your mappers and reducers on each partition
- natively in Java
- streaming enables interfacing to other languages (i.e. Python)

### Mapper

- converts raw source data into key / value pairs
- objective is to extract and organize what we care about as soon as possible

### Shuffle & Sort

- MapReduce automatically aggregates the keys and their associated values (can have multiple values for the same key), and sorts the keys
- by default, streaming treats all inputs and outputs as strings; therefore, they get sorted as strings, not numerically
- sometimes need to format in reducer so data is sorted properly (i.e. zero-pad numbers)

### Reducer

- processes each key's values
- for each key, a reducer is called once

## Spark

### Overview

- fast and general engine for large-scale data processing
- rich ecosystem and framework to enable machine learning, data mining, graph analysis, and streaming data
- write scripts in programming languages like Java, Python, and Scala
- Spark itself is written in Scala
  - Scala's functional programming lends itself well for distributed processing
  - fast performance (Scala compiles to Java bytecode)
- Spark is a memory-based solution which is why the Executor Cache is very integral
- doesn't have to run on Hadoop; can run on its own Cluster Manager
- built around one main concept: the Resilient Distributed Dataset (RDD)

### Scalability

1. Driver Program
   1. Spark Context
1. Cluster Manager (Spark, YARN)
1. Series of Executor Processors
   1. Cache
   1. Tasks

### Component Library

1. Spark Streaming
1. Spark SQL
1. MLLib
1. GraphX
1. Spark Core

### Resilient Distributed Dataset (RDD)

- an RDD object essentially represents a dataset
- you can call various functions on the RDD object to transform it or reduce it or analyze it to produce new RDDs
- since Spark 2.0, SQL focused version of RDDs were introduced called datasets
- essentially a way for Spark to store key and value information or just any information in an object that can automatically do the right thing on a cluster
- RDDs are created by the Driver Program
- Transforming RDDs:
  - map
  - flatMap
  - filter
  - distinct
  - sample
  - union, intersection, subtract, cartesian
- many RDD methods accept a function as a parameter
- RDD Actions:
  - collect
  - count
  - countByValue
  - take
  - top
  - reduce
- nothing happens in Driver Program until an action is called (lazy evaluation)
- can extend RDD to a DataFrame object
- DataFrames:
  - contain Row objects
  - can run SQL queries
  - has a schema (lends itself to more efficient storage)
  - read and write to JSON, Hive, parquet
  - communicate with JDBC / ODBC, Tableau
- DataSets:
  - in Spark 2.0, a DataFrame is really a DataSet of Row objects
  - DataSets can wrap known, typed data too

### Streaming

- processing continuous streams of data in near-real-time
- Use Cases:
  - analyze data streams in real time, instead of in huge batch jobs daily
  - analyze streams of web log data to react to user behavior
  - analyze streams of real-time sensor data for 'Internet of Things' stuff
- High-Level:
  - splits data into micro batches or little RDDs that can get managed together for transformation and output to other systems
  - usually split by one second chunks (i.e. near-real-time)
  - processing of RDDs can happen in parallel on different worker nodes
- DStreams (Discretized Streams):
  - generates the RDDs for each time step, and can produce output at each time step
  - can be transformed and acted on in much the same way as RDDs
  - or can access their underlying RDDs
  - perform operations on DStreams applied continuously over time as new batches of information gets received
  - Stateless Transformations on DStreams:
    - Map
    - FlatMap
    - Filter
    - reduceByKey
  - Stateful Data:
    - can also maintain long-lived stated on DStreams
    - windowed transformations
- Structured Streaming:
  - new, higher-level API for streaming structured data
  - uses DataSets
  - new data continuously appended, like a DataFrame that never ends

## YARN

### Overview

- TBD

## Kafka

### Overview

- TBD

## Flink

### Overview

- another stream processing framework, most similar to Storm
- can run on standalone cluster, or on top of YARN or Mesos
- highly scalable and fault tolerant
- performs steaming on an event-by-event basis, unlike micro batches in Spark streaming
- can process data based on event times, not when data was received
  - impressing windowing system
  - this plus real-time streaming and exactly-once semantics is important for financial applications

## Relational Data Stores with Hadoop

### Hive

- TBD

### MySQL

- TBD

## Non-Relational Data Stores with Hadoop

### HBase

- TBD

### Cassandra

- TBD

### MongoDB

- TBD

## References

1. [The Ultimate Hands-On Hadoop: Tame your Big Data!](https://www.udemy.com/share/101WBO3@GCG2h3kBLhu73Y-V994-4JkSTpSCM14zNlm_65RR0VfN97hBx87P8CT48KmyrX_D_Q==/)
1. [Hadoop Ecosystem](https://www.geeksforgeeks.org/hadoop-ecosystem/)
