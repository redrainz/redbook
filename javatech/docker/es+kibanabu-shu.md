### es kibana 
---
```yml
version: '3'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.7.1
    environment:
      - cluster.name=es
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
      - discovery.type=single-node
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - /Users/redrain/dockerData/elasticsearch/data:/usr/share/elasticsearch/data
      - /Users/redrain/dockerData/elasticsearch/logs:/usr/share/elasticsearch/logs
    ports:
      - "9200:9200"
    networks:
      - "es-network"
  kibana:
    image: docker.elastic.co/kibana/kibana:7.7.1
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    #volumes:
    #  - /Users/redrain/dockerData/kibana/config/kibana.yml:/usr/share/kibana/config/kibana.yml
    networks:
      - "es-network"
    depends_on:
      - elasticsearch
networks:
  es-network:
    external: true
```

安装IK分词器
```
./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v7.7.1/elasticsearch-analysis-ik-7.7.1.zip
```