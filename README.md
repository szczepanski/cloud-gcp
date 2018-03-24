#### Following notes are based on udemy course by Notez
https://www.udemy.com/hands-on-google-cloud-platformgcp-cloud-architect/learn/v4/overview

#  gcpDev1 project basics

1. Add new  gcpDev1 project
2. compute/vm instances

## google shell

linux friendly cli, such as clear (terminal)

- list all credentails allowd to work in specific project:

glcoud auth list

- list current default project:

gcloud config list project

- generic man / help 

gcloud -h

- tool specific help 

gcloud config --help
or
gcloud help config

- list command's all non default properties

gcloud config list

- list config's all settings

gcloud config list --all

# Hadoop

Appache opensource framework written in Java. It allows distributed processing of large datasets
across clusters of computers via programming models

## Architecture

![alt text](https://github.com/szczepanski/cloud-gcp/blob/master/media/architecture.png)

Components:

1. YARN - framework (job scheduling and cluster resource management)
2. HDFS - distributed file system (high throughput access to application data)
3. MapReduce -  yarn based distributed system for parallel processing of large data sets 

Common Utilities - Java libriaries and utilities required by hadoop components.

## Basic workflow

1. MapReduce - API used to define map and reduce the task as output to => 
2. YARN - works out where and how to run the task and stores the result in => 
3. HDFS

## Hadoop Ecosystem

- HIVE [GCP - Big Query]
Both are not to be used for online OLTP (Online Transaction Processing)
  - works with structured data stored in HDFS in Hive Query Language (similar to SQL)
  - runs Map Reduce for data processing in HDFS
  - assists in analytics and business intelligence (BI)

- HBase
  - non relational DB running atop of HDFS
  - designed to work on large scale - billions of rows with millions of columns
  - horizontal scaling
  - based on Google Big Table
  - runs batch processing only
  - data to be accessed in sequential order only 
  - good use case in random access of huge data
  
- Pig
  - works with structured data using PIG latin language
  - also works well with unstructured, incomplete datasets
  - use case for scripting not involving Java Python or SQL
  - Pig Lating program consists of operations series(transformations) applied to input data. 
  It runs MapReduce program in backend to produce output.
  - Pig transforms unstructed data into structured output
  - it is pre installed on Google DataProc machines
  

- Spark

- Kafka
- Flink 

## Hadoop Vs GCP
![alt txt](https://github.com/szczepanski/cloud-gcp/blob/master/media/hadoopVSgcp.png)


## Advantages

- open source
- supports user to rapidly write and test distributed systems
- FTHA - fault tolerance and availibility is hardware independent
- servers can be added or removed form cluster dynamicly with no interruptions
- wide platform compatibility as Java based
- 











