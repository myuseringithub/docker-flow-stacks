# Metrics stacks

## prometheus-grafana.yml

This stack sets up the node-exporter, cAdvisor, Prometheus, and Grafana

### Requirements

* logging-df-proxy.yml stack

```bash
docker stack deploy -c ../logging/logging.yml logging
```

### Deployment

```bash
docker stack deploy -c prometheus-grafana.yml metrics
```

Use `http://metrics_prometheus:9090` as Prometheus data source and `http://logging_elasticsearch:9200` for ElasticSearch.

## prometheus-grafana-df-proxy.yml

This stack sets up the node-exporter, cAdvisor, Prometheus, and Grafana

### Requirements

* docker-flow-proxy.yml stack
* logging-df-proxy.yml stack

```bash
docker network create --driver overlay proxy

docker stack deploy -c ../proxy/docker-flow-proxy.yml proxy

docker stack deploy -c ../logging/logging-df-proxy.yml logging
```

### Deployment

```bash
export USER=admin

export PASS=secret

docker stack deploy -c prometheus-grafana-df-proxy.yml metrics

open "http://localhost/grafana"
```

Use `http://metrics_prometheus:9090` as Prometheus data source and `http://logging_elasticsearch:9200` for ElasticSearch.
