docker-oracle-xe-11g
============================

Oracle Express Edition 11g Release 2 on Ubuntu 18.04 LTS

<del>This **Dockerfile** is a [trusted build](https://registry.hub.docker.com/u/numesia/oracle-xe-11g/) of [Docker Registry](https://registry.hub.docker.com/).</del>

<del>Since 2019-Feb-13(the Valentine's day eve) this docker image has been removed by DockerHub due to the Docker DMCA Takedown Notice from the Copyright owner which is the Oracle.</del>

<del>Happy Valentine's day!</del>

```diff
+ The new DockerHub [numesia/oracle-xe-11g-r2] has been released, because
+ the old [numesia/oracle-xe-11g] is banned by DockerHub and I cannot restore it.
+ Thanks for the help from the staff in Oracle with my DMCA Takedown issue, however this problem
+ is totally ignored by the DockerHub and I barely can't do anything but to open a new repo.
+ Sep 29 2019
```

## Installation(Local)
```
git clone https://github.com/numesia/docker-oracle-xe-11g.git
cd docker-oracle-xe-11g
docker build -t numesia/oracle-xe-11g .
```

## Installation(DockerHub)
```
docker pull numesia/oracle-xe-11g
```
SSH server has been removed since 18.04, please use "docker exec"

## Quick Start

Run with 1521 port opened:
```
docker run -d -p 49161:1521 numesia/oracle-xe-11g
```

Run this, if you want the database to be connected remotely:
```
docker run -d -p 49161:1521 -e ORACLE_ALLOW_REMOTE=true numesia/oracle-xe-11g
```

For performance concern, you may want to disable the disk asynch IO:
```
docker run -d -p 49161:1521 -e ORACLE_DISABLE_ASYNCH_IO=true numesia/oracle-xe-11g
```

Enable XDB user with default password: xdb, run this:
```
docker run -d -p 49161:1521 -e ORACLE_ENABLE_XDB=true numesia/oracle-xe-11g
```

For APEX user:
```
docker run -d -p 49161:1521 -p 8080:8080 numesia/oracle-xe-11g
```

```
# Login http://localhost:8080/apex/apex_admin with following credential:
username: ADMIN
password: admin
```

By default, the password verification is disable(password never expired)<br/>
Connect database with following setting:
```
hostname: localhost
port: 49161
sid: xe
username: system
password: oracle
```

Password for SYS & SYSTEM
```
oracle
```

Support custom DB Initialization and running shell scripts
```
# Dockerfile
FROM numesia/oracle-xe-11g

ADD init.sql /docker-entrypoint-initdb.d/
ADD script.sh /docker-entrypoint-initdb.d/
```
Running order is alphabetically. 
