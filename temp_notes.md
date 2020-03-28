## Microservices

- separate business logic
- several small, independent applications
- communicate via API
- Advantages
	- language independent
	- small teams
	- pairs well with containers	
	- scalable
- Disadvantages
	- complex networking
	- overhead of the # of databases, # of servers, how the architecture will be organized

## Docker

- platform as a service
- share a single operating-system kernel and are very lightweight
- no need to run the entire OS like virtual machines and be heavy and sluggish
- run applications in an isolated environment, similar to running in Vagrant (virtual machine)
- sandbox project and avoid conflicts
- no more "works on my computer tho"
- everything happens in a container
- container is a running instance of an image (template for creating the environment/snapshot)
- image contains the OS, software, application code
- image is defined using a Dockerfile (list of steps to create that image)
- dockerfile ->(build) image ->(run) to get containers 
- docker hub for community images. easy to share and use

## Kubernetes
- container-orchestration system
- enforce desired state management
- k8s cluster services run configuration in your infrastructure. Exists an API here that sits in front of all this
- workers are container hosts. Have a kubelet process that communicates with the cluster services
- configuration exists in a deployment YAML file. In this file is a pod configuration that specifies the container image(s) and other stuff like TCP port and services running. Also specify how many pods need to be run (replica). can list additional pods here and more container images and replicas.
- pod is a smallest unit of deployment. Pods can have one more running containers. 
- feed the YAML file to the API and the cluster services will schedule the pods in the environment and ensure the right # of pods running
- can have multiple pods running on a worker/container hosts
- if you lose a worker, kubernetes cluster services will notify you and the scheduler will decide which worker/where to move the lost pod to restore balance.
- in a pod, the containers can reference each other on localhost, but cannot talk to a container in another pod
- kubectl is the Kubernetes cli

## Kafka
- message: small to medium sized piece of data
- producer: application that sends messages/data to Kafka
- consumer: application that reads data from Kafka 
- broker: name of the Kafka server. Kafka acts as a message broker between the producer and consumer as they don't interact directly
- cluster: group of computers sharing workload for a common purpose. Multiple brokers in a Kafkacluster. Kafka is a distributed system
- topic: unique name for Kafka stream, so consumers can get the data they want from the Kafkacluster. A grouping of data from producers
- partition: breaking the topic apart and distributing the data to multiple computers if its too big. we decide how it is split and broken apart.
- offset: a sequence id given to messages as they arrive in a partition
- to locate a message, topic name -> partition number -> offset
- consumer group: a group of consumers acting as a single logical unit to help divide the work from consuming data from the Kafkacluster.
- storage layer is essentially a massively scalable pub/sub message queue designed as a distributed transaction log
- Zookeeper: manages the cluster and builds coordination between different nodes in a cluster. Elect a broker as a controller so when a node shuts down, we can recover from previously committed to offset.

## Redis
- open source, NoSQL, key -> value, in memory (relies on memory of computer for data storage), data structure server (choose the key and/or value)
- FAST, not CPU intensive, scalable
- commonly used as a database, cache, and message broker
- supports strings, hashes, lists, sets, bitmaps
- data persists either through snapshotting every once in a while or append only file (AOF)
- AOF: log of all operations, large file but good for recovering from server outages
- for Redis replication, there is a leader follower (master-slave) replication. Slave instances can be exact copies of master instances and reconnect to the the master every time the link breaks.

## ElasticSearch
- horizontally scalable search engine that can search ALL KINDS OF DOCUMENTS
- each "shard" is an inverted index of documents
- handles structured data and can aggregate data quickly
- often faster than Hadoop, Apache Spark
- low level: handling JSON requests and returning search results in JSON. You have to do something useful with that data.

Elastic Stack:
- Kibana
  - Web UI for searching and visualizing
  - creates complex aggregations, graphs, charts
  - often used for log analysis

- Logstash/Beats
  - feeds data into ElasticSearch
  - FileBeat monitors logs file, parses them, and imports them to ElasticSearch in real time
  - Logstash also pushes data into ElasticSearch

- X-Pack
  - offers security, alerting, monitring, reporting for ElasticSearch

Concept:
  - Documents: the things you're searching for. They can be text, JSON, etc
  - Types: defines the schema and mapping shared by documents
  - Index: powers the search into documents within a collection of types
  - Term Frequency: how often a term appears in a given documents
  - Document Frequency: how often a term appears in all documents 
  
--	

- works well with RESTful API and lots of client library support
- scalable as indexes are split into shards which can be spread throughout in a cluster to different machines
- primary shards are replicated and routing are done automatically

Summary: 

- So Elasticstack (ELK being a clingy moniker for just Elasticsearch, Logstash, and Kibana) is really just a way to parse, store, and query/visualize any large dataset - not just for network monitoring.

- The way it works is that you have data that is stored or created in flat files (standard text files, basically, though they can be more advanced). You can use Filebeats to ship this data, line-by-line, to a Logstash instance, or you can have Logstash installed where your data is, and it can hoover it up directly. (I'm technically overlooking that Filebeats can do most of Logstash's job, but I'm doing this intentionally - that's more of a philosophical debate about implementation.)

- Logstash's primary job is to take that data and 'massage' it - translate fields, or make data from disparate sources easier to parse (for example, maybe you're running Bro and Snort, and they have a different field name for "ip.source" 
  - this can be fixed at Logstash, so when you make visualizations/dashboards later, it's easier to correlate info). Logstash then takes the data and slam-dunks it into Elasticsearch.

- Elasticsearch is just a big dumb database. Don't get me wrong, it's a fast and useful one, but the ELI5 for it is that you store data there, and you query data from it. It's a big, dumb, fast database. (You know, for search)

- But you still have to get that data into human-readable format. That's where Kibana comes into play - it effectively gives you a GUI to query Elasticsearch and get pretty graphics based on your data.

- In terms of network monitoring using Elasticstack, Snort will process packets and, based on rules provided to it, create alerts in a flat file on that machine that can then be hoovered up by Filebeats. SGUIL is just a front-end for Snort alerts, it's separate from the stack I'm describing. Bro, mentioned earlier, does similar, but it gives you heuristics on all of the packets coming through, rather than only flagging on alerts.
