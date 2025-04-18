---
layout: post
title:  "Create Indexes in elasticsearch"
metadate: "hide"
categories: [ NoSQL, Search Engine, Elasticsearch ]
tags: [ Elasticsearch ]
image: "assets/img/elasticsearch.svg"
---

{% include docker-prerequisites.md %}
3. Install Elasticsearch or [Run Elasticsearch container](https://github.com/JinnaBalu/elasticsearch/blob/master/2019-08-29-Elasticsearch-Single-Node-using-Docker-Compose.md)


## Create the Indice

- First, let's create a twitter user, and add some tweets

```bash
curl -XPUT 'http://127.0.0.1:9200/twitter/user/kimchy' -d '{ "name" : "Shay Banon" }'

curl -XPUT 'http://127.0.0.1:9200/twitter/tweet/1' -d '
{
    "user": "kimchy",
    "postDate": "2009-11-15T13:12:00",
    "message": "Trying out Elasticsearch multinode, so far so good?"
}'

curl -XPUT 'http://127.0.0.1:9200/twitter/tweet/2' -d '
{
    "user": "kimchy",
    "postDate": "2009-11-15T14:12:12",
    "message": "Balu tweet, will it be indexed?"
}'
```

- Now, let's see if the information was added by GETting it:

```bash
curl -XGET 'http://127.0.0.1:9200/twitter/user/kimchy?pretty=true'
curl -XGET 'http://127.0.0.1:9200/twitter/tweet/1?pretty=true'
curl -XGET 'http://127.0.0.1:9200/twitter/tweet/2?pretty=true'
```

- Create customer entity with 1000 records 

```bash
curl -sXPUT 'http://localhost:9200/customer/?pretty' -d '{
  "settings" : {
      "index" : {
          "number_of_shards" : 5,
          "number_of_replicas" : 0
      }
  }
}'

while ! curl -s "localhost:9200/_cat/indices?v" | grep green; do
  sleep 0.1
done

for i in `seq 1 500`; do
  curl -sXPUT "localhost:9200/customer/external/$i?pretty" -d "
  {
    \"number\": $i,
    \"name\": \"John Doe - $i\"
  }"
done
```


- Create student entity with 1000 records 

```bash
curl -sXPUT 'http://localhost:9200/student/?pretty' -d '{
  "settings" : {
      "index" : {
          "number_of_shards" : 5,
          "number_of_replicas" : 0
      }
  }
}'

while ! curl -s "localhost:9200/_cat/indices?v" | grep green; do
  sleep 0.1
done

for i in `seq 1 20`; do
  curl -sXPUT "localhost:9200/student/external/$i?pretty" -d "
  {
    \"number\": $i,
    \"name\": \"Ram - $i\"
  }"
done
```

- Somemore examples

```bash
curl -X PUT "localhost:9200/twitter?pretty"

curl -X PUT "localhost:9200/school?pretty" -H 'Content-Type: application/json' -d'
{
    "settings" : {
        "number_of_shards" : 3,
        "number_of_replicas" : 2
    },
    "mappings" : {
        "properties" : {
            "name" : { "type" : "text" }
        }
    }
}
'
```