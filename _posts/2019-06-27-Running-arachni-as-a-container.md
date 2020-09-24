---
layout: post
title:  "Arachni - Vulnerability Assessment & Penetration Testing Tool"
author: jinna
categories: [ Security ]
image: assets/images/Logo.png
---

# Arachni

## 1. [Introduction](https://github.com/JinnaBalu/DevOps/wiki/What-is-Arachni)

## 2. Running as a container

#### Environment variables
| Name  | Default | Options |
| ------------- | ------------- | ------------- |
| SERVER_ROOT_PASSWORD | arachni | any |
| ARACHNI_USERNAME | arachni | any |
| ARACHNI_PASSWORD | password | any |
| DB_ADAPTER | sqlite | sqlite, postgresql |
| DB_HOST | {empty} | any |
| DB_NAME | {empty} | any |
| DB_USER | {empty} | any |
| DB_PASS | {empty} | any |


### Run the docker container


```bash
docker run -d \
  -p 222:22 \
  -p 7331:7331 \
  -p 9292:9292 \
  --name arachni \
  arachni/arachni:latest
```

#### SSH 

`ssh -p 222 root@docker-machineIP  with default password is "arachni"`

#### Web endpoint can be access as:

http://${docker-machineIP}:9292

- Web-UI Admin's username and password

`username: admin@admin.admin`

`password: administrator`

- Web-UI User's username and password

`username: user@user.user`

`password: regular_user`

#### RESTful API endpoint will be

http://${docker-machineIP}:7331

#### Customise container with 

1. RUN 

```bash

docker run -d \
  -p 222:22 \
  -p 7331:7331 \
  -p 9292:9292 \
  --name arachni \
  -e SERVER_ROOT_PASSWORD="DockerArachniPWD" \
  -e ARACHNI_PARAMS="--authentication-username arachni --authentication-password Pass123 --only-positives"  \
  arachni:1.4

```
2. SSH

`ssh -p 222 root@docker-machineIP  with password is "DockerArachniPWD"`

3. RESTful API customized username and password

`username: arachni`

`password: Pass123`

### Archani with Database adopter as postgresSQL

#### RUN using docker run command 

```
docker run -d \
  -e "DB_ADAPTER=postgresql" \
  -e "DB_HOST=sample_host" \
  -e "DB_NAME=sample_db_name" \
  -e "DB_USER=sample_db_user" \
  -e "DB_PASS=sample_db_pass" \
  -p 222:22 \
  -p 7331:7331 \
  -p 9292:9292 \
  --name arachni \
  arachni/arachni:latest
```

#### RUn using `docker-compose`

```yaml
version: '3'
services:
  postgres:
    image: postgres:9.6
    container_name: postgres
    restart: always
    environment:
      POSTGRES_DB: arachni
      POSTGRES_USER: test_username
      POSTGRES_PASSWORD: test_username
      PGDATA: /var/lib/postgresql/data/pgdata
    volumes:
      - ./cache/postgres/data/:/var/lib/postgresql/data/pgdata
    ports:
      - "5432:5432"
  arachni:
    image: arachni/arachni:latest
    conatiner_name: arachni
    environment:
      DB_ADAPTER: postgresql
      DB_HOST: postgres
      DB_NAME: arachni
      DB_USER: test_username
      DB_PASS: test_username
    ports:
      - "7331:7331"
      - "9292:9292"
      - "222:22"
    depends_on:
      - postgres
```

## 3. [Running as a self contained package](https://github.com/JinnaBalu/DevOps/wiki/Running-as-a-self-contained-package)

## 4. [Using Web UI](https://github.com/JinnaBalu/DevOps/wiki/Using-Arachni-Web-UI)