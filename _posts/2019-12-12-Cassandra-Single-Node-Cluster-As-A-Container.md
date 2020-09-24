---
title:  "Cassandra single node cluster as a container"
metadate: "hide"
categories: [ Cassandra, NoSQL ]
tags: [ Cassandra ]
image: "assets/images/cassandra.svg"
---


- How to run cassandra as a container?
- How to run cassandra as a single node cluster?

To answer the above, Docker provides a `Docker Official Images` for Apache Cassandra, is an open-source distributed storage system.

## Quick reference 

#### Get Help From

- [The Docker Community Forums](https://forums.docker.com/)
- [The Docker Community Slack](http://dockr.ly/slack)
- [Stack Overflow](https://stackoverflow.com/search?tab=newest&q=docker)
- [Ask me Your Questions - Bot](https://jinnabalu.github.io/resume/)

## Create the docker-compose

- Create a `docker-compose.yml` with the following

```bash
version: '3'
services:
    cassandra-one:
        image: cassandra:3.9
        # volumes:
        #     - cassandra-volume:/var/lib/cassandra/
        ports:
            - 7000:7000
            - 7001:7001
            - 7199:7199
            - 9042:9042
            - 9160:9160
        environment:
            - CASSANDRA_CLUSTER_NAME='sample-cluster'
            - CASSANDRA_NUM_TOKENS=256
            - CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch
            - CASSANDRA_DC=sample-datacenter-one
            - CASSANDRA_RPC_ADDRESS=0.0.0.0
        restart: always
# volumes:
#   cassandra-volume:
#     driver: local
#     driver_opts:
#       o: bind
#       type: none
#       device: /root/db/cassandra-volume/
    
```

[![Try in PWD](https://cdn.rawgit.com/play-with-docker/stacks/cff22438/assets/images/button.png)](http://play-with-docker.com?stack=https://raw.githubusercontent.com/JinnaBalu/cassandra/master/single-node-cluster/cassandra.yml)

- To maintain the persistancy of the data uncomment the volumes in the service and respective Volume 
