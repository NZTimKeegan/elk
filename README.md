# elk
For deploying the Elastic stack locally

## How do I work with this?

Use these commands to start a local ELK stack with Docker:

- Create a network so the services can talk to each other using by name:
  ```Bash
  docker network create elk
  ```

- Run a standalone Elastic container in the foreground:
  ```Bash
  docker run --env "discovery.type=single-node" \
  --name elasticsearch \
  --network elk \
  --publish 9200:9200 \
  --publish 9300:9300 \
  --rm \
  docker.elastic.co/elasticsearch/elasticsearch:7.13.1
  ```

- Open a new terminal window and run a Kibana container in the foreground:
  ```Bash
  docker run --env "ELASTICSEARCH_HOSTS=http://elasticsearch:9200" \
  --name kibana \
  --network elk \
  --publish 5601:5601 \
  --rm \
  docker.elastic.co/kibana/kibana:7.13.1
  ```
