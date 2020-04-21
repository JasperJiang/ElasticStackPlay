# ElasticStackPlay

## Components

* [APM Server](https://www.elastic.co/guide/en/apm/server/current/index.html) - The APM Server receives data from APM agents and transforms them into Elasticsearch documents.
* [Elastalert](https://github.com/Yelp/elastalert) - ElastAlert is a simple framework for alerting on anomalies, spikes, or other patterns of interest from data in Elasticsearch.
* [ElasticSearch](https://www.elastic.co/elasticsearch/) - Elasticsearch is a distributed, RESTful search and analytics engine capable of addressing a growing number of use cases. As the heart of the free and open Elastic Stack, it centrally stores your data for lightning fast search, fine-tuned relevancy, and powerful analytics that scale with ease.
* [Journalbeat](https://www.elastic.co/guide/en/beats/journalbeat/current/index.html) - Journalbeat is a lightweight shipper for forwarding and centralizing log data from systemd journals.
* [Kibana](https://www.elastic.co/kibana) - Kibana lets you visualize your Elasticsearch data and navigate the Elastic Stack so you can do anything from tracking query load to understanding the way requests flow through your apps.
* [Filebeat](https://www.elastic.co/beats/filebeat) - Lightweight shipper for file based logs
* [Kube-state-metrics](https://github.com/kubernetes/kube-state-metrics) - Add-on agent to generate and expose cluster-level metrics.
* [Metricbeat](https://www.elastic.co/beats/metricbeat) - Lightweight shipper for metrics. Collect metrics from your systems and services. From CPU to memory, Redis to NGINX, and much more, Metricbeat is a lightweight way to send system and service statistics.

## Install ElasticStack

When installing the Elastic Stack, you must use the same version across the entire stack. For example, if you are using Elasticsearch 7.6.2, you install Beats 7.6.2, APM Server 7.6.2, Elasticsearch Hadoop 7.6.2, Kibana 7.6.2, and Logstash 7.6.2.

If you’re upgrading an existing installation, see [Upgrading the Elastic Stack](https://www.elastic.co/guide/en/elastic-stack/current/upgrading-elastic-stack.html) for information about how to ensure compatibility with 7.6.2.

### Installation Older

Install the Elastic Stack products you want to use in the following order:

1. Elasticsearch [install instructions](https://www.elastic.co/guide/en/elasticsearch/reference/7.6/install-elasticsearch.html)
2. Kibana [install](https://www.elastic.co/guide/en/kibana/7.6/install.html)
3. Logstash [install](https://www.elastic.co/guide/en/logstash/7.6/installing-logstash.html)
4. Beats [install instructions](https://www.elastic.co/guide/en/beats/libbeat/7.6/getting-started.html)
5. APM Server [install instructions](https://www.elastic.co/guide/en/apm/server/7.0/installing.html)
6. Elasticsearch Hadoop [install instructions](https://www.elastic.co/guide/en/elasticsearch/hadoop/7.6/install.html)
Installing in this order ensures that the components each product depends on are in place.

## Install in Docker

### Install Elasticsearch

```bash
docker run -d --name elasticsearch -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.6.2
```

### Install Kibana

```bash
docker run -d --name kibana --link elasticsearch:elasticsearch -p 5601:5601 docker.elastic.co/kibana/kibana:7.6.2
```

### Install Filebeat

```bash
docker run -d --name filebeat -v /Users/jjiang153/Documents/Playground/ElasticStackPlay/Filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml --link kibana:kibana --link elasticsearch:elasticsearch docker.elastic.co/beats/filebeat:7.6.2
```
