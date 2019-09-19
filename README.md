# Deceptipot
Research Honeypot

This project uses
- Honeytrap (as a MITM sensor) https://github.com/honeytrap/honeytrap
- ELK stack (captured information store/visualization)
- Cowrie (Configurable SSH honeypot) https://github.com/cowrie/cowrie

## Build Instructions (Mac, Linux)

### 1. Get Docker and Docker Compose
https://docs.docker.com/compose/install/

### 2. Clone Repo
Clone this repository and cd into it

### 3. Start Network

```
> docker network create honeytrap
```

### 4. Create data infrastructure for ElasticSearch

```
> sudo mkdir -p /data/elasticsearch/data && sudo chown -R 1000:1000 /data/elasticsearch
```

### 5. Increase memory limits for Docker

#### On Linux
```
> sudo sysctl -w vm.max_map_count=262144
```

#### On Mac
Open Docker UI then go to Preferences -> Advanced and increase memory limit

### 6. Start multi-container app (honeytrap, elasticsearch, kibana, cowrie)

```
> docker-compose -f docker-compose-honeytrap-playground.yml up
```

This will start a container running Elasticsearch, Kibana, Cowrie and HoneyTrap, all running in the honeytrap network.

### 7. Open Kibana and create the HoneyTrap index

To open Kibana open a web browser and go to http://localhost:5601

To get the data into Kibana we need to set a index-pattern. Kibana will auto-discover the pattern when we start to send the data to Elasticsearch.

Enter the index-name honeytrap in the index-pattern field.
Now when you go to Discover it should show you the HoneyTrap data coming in.



