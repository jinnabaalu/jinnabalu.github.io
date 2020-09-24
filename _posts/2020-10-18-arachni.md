# VAPT

Vulnerability Assessment and Penetration Testing, Identify the doorways of threats by stressing on the weaknesses.

## Vulnerability

Vulnerabilities are the doorways via which threats are revealed. Vulnerabilities are actually weaknesses in system. This can be identitified by the software rather manually.

## Penetration

Process of trying to gain unauthorized access to authorized resources by stressing on the weaknesses. Penetration testing is also known as an ethical hacking as “breaking into your own system to see how hard it is to do.” It is a main branch of network security evaluation, which aims at providing analysis to discover the vulnerabilities and security threats in systems and networks.


## Tools

1. [Arachni](https://github.com/JinnaBalu/vapt/blob/master/arachni/README.md)
2. ZAP
3. Samurai


1. [Arachni](https://www.arachni-scanner.com/) is a feature-full, modular, high-performance Ruby framework aimed towards helping penetration testers and administrators evaluate the security of modern web applications.

#### Recommended system requirements

- Operating systems: Linux (32bit or 64bit), Mac OS X (64bit), Windows (64bit)
- RAM: 2GB of available memory.
- Storage: 10GB of available disk space.
- Optional: PostgreSQL server for the WebUI — by default SQLite3 is used (included in the packages).
- PostgreSQL is preferred when dealing with larger workloads, for configuration instructions please see the WebUI Wiki.
- Prior to running scans, it is recommended that you consult the scan optimization guide, as there are several options you can use to significantly increase performance and/or limit resource utilization.


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
