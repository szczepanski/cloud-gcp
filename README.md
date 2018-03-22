#### Following notes are based on udemy course by Notez
https://www.udemy.com/hands-on-google-cloud-platformgcp-cloud-architect/learn/v4/overview

#  gcpDev1 project basics

1. Add new  gcpDev1 project
2. comppute/vm instances

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

- HIVE
- HBase
- Pig
- Spark
- Kafka
- Flink 

## Hadoop Vs GCP
![alt txt](https://github.com/szczepanski/cloud-gcp/blob/master/media/hadoopVSgcp.png)











