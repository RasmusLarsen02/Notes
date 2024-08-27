
## Introduction

Distributed systems connect different network computers by passing messages and coordinating between them. In concurrent systems many computers run commands inside the network. Concurrency means that several programs are running at the same time with eachother. There is no global clock for the distibuted systems so keeping the programs syncronized is an important aspect of maintaining correct running of distributed systems. Failures can and will happen within the network. Because the programs are no longer running in single threaded systems, there will be a series of new challenges in imlementing the DS. Diffent models can be used to overcome these challenges and having standardized models help to limit faults and readability and maintainablity of the codebase. 

**Network** is a collection of entities that can execute different software.

**Node** A node is the name for each entity that exist within the network. 

**Communication** is the interaction between each of the Nodes in the Network 

**Architecture models** These are models that allow abstractions and patterns for entities and communication in the network. 

**Message Passing** Nodes that send information from one node to another 

**Shared Memory** Nodes communicate through some shared memory storage example a database, where each of the nodes can read and write to/from. 

**Client-Server Architecture** Are different nodes that communicate through message-passing (Invocations) in conjunction with a Server. Here the nodes send some request for the server to handle some complex actions and then send back the results

**Peer-to-Peer** networks where nodes are interconnected with serveres

Having more servers can increase resilience against failures. 

## Chapter 1 

