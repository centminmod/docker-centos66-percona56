Percona 5.6.x on CentOS 6.6 64bit Docker container build intended for use with [CentminMod.com LEMP stack](http://centminmod.com). 

### My Docker Hub repo

* https://registry.hub.docker.com/u/centminmod/docker-centos66-percona56/

### Centmin Mod Docker Development forums

* https://community.centminmod.com/forums/centmin-mod-docker-development.52/

---
### Default MySQL root user password 

* The default MySQL root user password is set to = mysqlpass with added replication user = repl

#### Grab from Docker Hub

    docker pull centminmod/docker-centos66-percona56

Run docker container

    docker run -d -p 3306:3306 -t centminmod/docker-centos66-percona56

or specify a name e.g. percona1

    docker run --name percona1 -d -p 3306:3306 -t centminmod/docker-centos66-percona56

or if host system already has MySQL running on port 3306 need to map to another local host port e.g. 3307

    docker run --name percona1 -d -p 3307:3306 -t centminmod/docker-centos66-percona56

to access container via bash if started with name = percona1

    docker exec -ti percona1 /bin/bash

to connect from host system to MariaDB docker container use the -h IP address which is shown for the docker0 network interface

    ifconfig docker0 | grep 'inet '
    inet addr:172.17.42.1  Bcast:0.0.0.0  Mask:255.255.0.0

e.g. host system running CentminMod.com LEMP stack MariaDB 10 server hence the client is 10.0.16 to connect to Percona 5.6.22 docker container

    mysqladmin -P 3307 -h 172.17.42.1 -u root -p ver
    Enter password: 
    mysqladmin  Ver 8.42 Distrib 5.6.22-72.0, for Linux on x86_64
    Copyright (c) 2009-2014 Percona LLC and/or its affiliates
    Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.
    
    Server version          5.6.22-72.0
    Protocol version        10
    Connection              Localhost via UNIX socket
    UNIX socket             /var/lib/mysql/mysql.sock
    Uptime:                 4 min 57 sec
    
    Threads: 1  Questions: 2  Slow queries: 0  Opens: 67  Flush tables: 1  Open tables: 60  Queries per second avg: 0.006

---

#### Building from Dockerfile

Grab files

    git clone https://github.com/centminmod/docker-centos66-percona56.git

Build docker container with image name = centos66-percona56. Run command within same directory as Dockerfile

    docker build -t centos66-percona56 .

To run follow same run steps above.

