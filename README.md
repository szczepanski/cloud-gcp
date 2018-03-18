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

Opensource appache framework written in Java. It allows distributed processing of large datasets
across clusters of computers via programming models

## Architecture

![alt text](https://github.com/szczepanski/cloud-gcp/blob/master/media/architecture.png)

Components:

1. YARN - framework (job scheduling, resource management)
2. HDFS - distributed storage (high throughput access to application data)
3. MapReduce - distributed computing ()

plus common tools - finish here











