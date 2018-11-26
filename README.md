# Hyperledger Sawtooth Like/Unlike Application
Simple use case of Hyperledger Sawtooth by making Like/Unlike Application.

# Introduction
This is a minimal example of a Sawtooth 1.0 application, with a transaction processor and corresponding client. 
This example demonstrates a simple use case, where a user likes and dislikes some content.

A user can :
- like Content
- Unlike Content
- Count total number of likes

# Components
The like jar transaction family contains two parts, both written in Python 3:
1. The client application has two parts:
- pyclient/likejar_client.py contains the client class which interfaces to the Sawtooth validator via the REST API
- pyclient/likejar.py is the Like Jar CLI app The client container is built with files setup.py and Dockerfile.

2. The Transaction Processor, pyprocessor/likejar_tp.py

# Docker Usage
## Prerequisites
This example uses docker-compose and Docker containers. If you do not have these installed please follow the instructions here: https://docs.docker.com/install/

### NOTE
The preferred OS environment is Ubuntu Linux 16.04.3 LTS x64. Although other Linux distributions which support Docker should work.
Building Docker containers

To build TP code for Python and run the likejar.py example:
```
 sudo docker-compose up --build
```
The `docker-compose.yaml` file creates a genesis block, which contain initial Sawtooth settings, generates Sawtooth and client keys, and starts the Validator, Settings TP, Like Jar TP, and REST API.
Docker client

In a separate shell from above, launch the client shell container:

sudo docker exec -it likejar-client bash

You can locate the correct Docker client container name, if desired, with `sudo docker ps` .

In the client shell you just started above, run the `likejar.py` application. Here are some sample commands:
```
likejar.py like
likejar.py unlike
likejar.py count
```
To stop the validator and destroy the containers, type ^c in the docker-compose window, wait for it to stop, then type
```
sudo docker-compose down
```
Everytime a user like/dislikes something, the new block is created and added to blockchain. The new head is set by validator and distributed across all the ledgers.

## Thank You
