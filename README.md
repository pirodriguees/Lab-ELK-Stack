# Lab for learn ELK Stack.

[![Build](https://img.shields.io/badge/Running%20OS-Linux-orange)]()
[![Build](https://img.shields.io/badge/Elastic%20Versions-7.8-orange)]()

This repository was create to learn more about logging monitoring and elastic stack.
The ELK Stack are great tools for centralize logs of machines.

*This pipeline is still beign edited.*

## How install ##

* [Elasticsearch-download](https://www.elastic.co/downloads/elasticsearch)
* [Logstach-download](https://www.elastic.co/downloads/logstash)
* [Kibana-download](https://www.elastic.co/kibana)
* [Beats-download](https://www.elastic.co/downloads/beats)


### Ports: ###
|Application|Ports|
|-|-
|Elasticsearch|9200
|Kibana|5601
|Logstash|5044 normally, but you define input.
|Beats|It's just a client with data output.

### My Structure: ###
Beats > Elasticsearch > Kibana.

### The Elasticsearch configuration ###
```bash
$ cat /etc/elasticsearch/elasticsearch.yml | egrep -v "#.*|^$"
cluster.name: labteste
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0
```

### The filebeat configuration ###
```bash
$ cat /etc/filebeat/filebeat.yml | egrep -v "#.*|^$"
filebeat.inputs:
filebeat.config.modules:
  path: ${path.config}/modules.d/*.yml
  reload.enabled: false
setup.dashboards.enabled: true
setup.kibana:
 host: "localhost:5601
output.elasticsearch:
  hosts: ["localhost:9200"]
```
### Running filebeat and configure dashboard on Kibana ###
```bash
$ filebeat modules enable nginx #active logs check of nginx.
$ filebeat setup -e #configure dashboard of module.
```


## References: ##
- [Full Cycle](https://www.youtube.com/watch?v=Bb3g8xk0Cys)
- [Eduardo_Neves](https://www.youtube.com/channel/UCPS3_RjG-FzAEPp0ntXpODA)
- [Logz.io](https://logz.io/learn/complete-guide-elk-stack/)
- [ELK-Doc](https://www.elastic.co/guide/index.html)