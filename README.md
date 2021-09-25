# IOTPAAS Projects

## Overview

This is the project folder that has all the relevant microservices, datastores, message queue, observability and kustomize templates to build and deploy the IOTPaaS (internet of things platform as a service)

It is by no means, the be all and end all of IOT platforms. 

The main purpose for developing this platform and functionality is to have
- A system to deploy and execute secure IOT device data to a backend
- A simple analytics service to retrieve and view aggregated iotdata data
- A Highly scalable platform
- High availability
- A loosely coupled architecture
- A system based on linux containers
- Container orchestration (OpenShift/Kuberntes)
- A simple to implement support services (datastore, message queue)
- A customizable, easy to update and deploy data structure
- CICD to build and deploy quickly

## Project structure

This project includes the following repo's (as submodules)

- iotpaas-message-consumer (couchbase)
- iotpaas-message-consumer-redis
- iotpaas-reverse-proxy
- iotpaas-auth-interface
- iotpaas-infra-pg
- iotpaas-gobench
- iotpaas-templates
- sparkml-vitalsigns

## Technology Stack

- The data store is made up of 6 replicas, statefulset deployment (3 master, 3 slaves),redis ha cluster with persistence (I have left it up to the user to deploy couchbase - see the couchabse docs to deploy the coucbase operator)
  - It should be obvious that either redis or couchbase can be used, remembering to use the appropriate consumer, the default is using redis
- The message queue is Kafka, in a 3 replica ha statefulset deployment with persistence (kafka with zookeeper) using the strimzi operator
- Message producer and consumer use the confluent kafka driver
- Observability is realized with Grafana (dashboards) and prometheus
- CICD uses Tekton, dependencies to realize the CICD include a seperate instance of SonarQube and Gitea (repo) deployed on Kubernetes

## Usage

Clone this repo 

```
git clone --recursive https://github.com/luigizuccarelli/iotpaas-project
```

## Installation

Navigate to the README.md in the iotpaas-templates directory for instructions on installing the iotpaas ecosystem.

## Customization

By simply changing the schema in the iotpaas-message-consumer the user/developer can implement any type of IOT device/s. The only proviso is to ensure the device sending the data to the producer is secured using https. Once changed and tested new images can be built and deployed to the system with minutes

## Observability

The IOTPAAS system makes use of grafana (for visual display) and prometheus to collect metrics from the consumer and producer services

It will be up the the user/developer to implement other dashboards to monitor service like redis, couchbase, kafka, nodes etc.

## Open Source

The project was set up with the Apache License 2.0. The goal was to create a simple to use and implement system that can be cloned/forked  without any major restrictions.

I have tried my best to keep all services as simple as possible, simplicity is hard, it takes time and thought to make something simple yet extremely useful, scalable and robust.

The SonarQube quality gate was set to 80% code coverage, all microservices (iotpaas-message-consumer, iotpaas-message-consumer-redis, iotpaas-message-producer, iotpaas-auth-interface) have unit test coverage >= 80%

I have created the README's after testing and deploying, if there are any discrepencies please add an issue or create a PR. This also applies to any problems in any of the repos (code base included).

Feel free to clone/fork. 

Hope its useful - enjoy !!!

Luigi Zuccarelli 2021
