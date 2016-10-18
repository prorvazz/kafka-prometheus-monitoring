# kafka-promethues-monitoring
Dockerised example of monitoring Kafka with Prometheus and Grafana.

## Pre-Requisites
* install Docker and Docker Compose - https://docs.docker.com/
* set KAFKA_ADVERTISED_HOST_NAME in `docker-compose.yml` to match your docker host IP.  (Note: Do not use localhost or 127.0.0.1 as the host ip if you want to run multiple brokers).  See wurstmeister's docker-kafka for more information on configuring Kafka - https://github.com/wurstmeister/kafka-docker

## Usage

```
docker-compose up
```

- View Prometheus UI - `http://$DOCKER_HOST_IP:9090`
- Grafana UI - `http://$DOCKER_HOST_IP:3000` (admin:admin)
- Kafka metrics - `http://$DOCKER_HOST_IP:8080/metrics`

WORK IN PROGRESS

## Sending Kafka messages
In order for the Kafka broker to expose JMX topic metrics you must send some messages to the topics.
```
cat kafka-messages | docker run -i -a stdin wurstmeister/kafka /opt/kafka_2.11-0.10.0.1/bin/kafka-console-producer.sh --broker-list 192.168.99.100:9092 --topic customer
cat kafka-messages | docker run -i -a stdin wurstmeister/kafka /opt/kafka_2.11-0.10.0.1/bin/kafka-console-producer.sh --broker-list 192.168.99.100:9092 --topic audit
```
