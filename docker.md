---
title: Docker
description: 
published: true
date: 2022-04-26T21:14:17.609Z
tags: 
editor: markdown
dateCreated: 2022-04-26T22:03:09.374Z
---

# Docker
This page provide help for Docker.

## Useful Docker commands

### ps

Show the running containers.

- `-a` show all containers.

```bash
docker ps -a
```
### pull

Pull image from docker Hub.

```bash
docker pull ghcr.io/requarks/wiki:2
```

### run / create / build

- `docker build` builds a new image from the source code.
- `docker create` creates a writeable container from the image and prepares it for running.
- `docker run` creates the container (same as docker create) and runs it.

#### run

Create and run a container.

- `-d` start as a daemon.
- `-p <host-IP>:<docker-host>:<container>/<tcp|udp>` port mapping.
- `-e "<PARAMETER>=<value>"` add parameter.
- `--name` name of the container.
- `--restart unless-stopped` start with the system.

```bash
docker run -d --name postgres-wiki -e POSTGRES_USER=wiki -e POSTGRES_PASSWORD=wikipassword -p 5432:5432 postgres
```

```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=172.17.03" -e "DB_PORT=5432" -e "DB_USER=wiki" -e "DB_PASS=wikipassword" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

### start / stop

Start / Stop a container.

```bash
docker start my-wiki
```

### rename

Rename an image name. By default docker assign an automatic name if it is not defined with the run command.

```bash
docker rename old-wiki new-wiki
```

### update

Update configuration of one or more containers.

- `docker update [OPTIONS] CONTAINER [CONTAINER...]`

```bash
docker update --restart unless-stopped postgres-wiki
```

### rm / rmi

Remove a conteiner or an image by id or by name.

```bash
docker rm 068a15bdf783
```

### exec

Run a command in a running container.

- `docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`

```bash
docdocker rm 068a15bdf783ker rm 068a15bdf783
```

### network inspect

With that you can get network information from the containers, host...

```bash
docker network inspect 3b1dd0ca37ed
```

### docker inspect

This comand shows the information about the container.

- `--format` Format the output using the given Go template.

```bash
docker inspect --format '{{ .NetworkSettings.IPAddress }}' wiki-db
```

#### Get an instance’s IP address

```bash
docker inspect --format '{{ .NetworkSettings.IPAddress }}' wiki-db
```

#### Get an instance’s path

```bash
docker inspect --format '{{ .LogPath }}' wiki-db
```

## Install PostgreSQL Database

Pull image from docker Hub.

```bash
docker pull postgres
```

Run the machine.

```bash
docker run -d --name postgres-wiki -e POSTGRES_USER=wiki -e POSTGRES_PASSWORD=wikipassword -p 5432:5432 postgres
```

## Install pgAdmin

Pull image from docker Hub.

```bash
docker pull dpage/pgadmin4:latest
```

Run the machine.

```bash
docker run -p 5050:80 -e "PGADMIN_DEFAULT_EMAIL=robertouj@gmail.com" -e "PGADMIN_DEFAULT_PASSWORD=pgapass" -d dpage/pgadmin4
```

## Install Wiki.js

Pull image from docker Hub.

```bash
docker pull ghcr.io/requarks/wiki:2
```

Run the machine.

```bash
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=172.17.03" -e "DB_PORT=5432" -e "DB_USER=wiki" -e "DB_PASS=wikipassword" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
```

## TODO

Update with: <https://geekflare.com/es/docker-commands/> 

**Commands to check:**
docker ps
docker ps -a
docker start a1609c5405f9
docker exec -it ubuntu /bin/bash
docker commit -m "added Node.js" -a "robertouj" a1609c5405f9 robertouj/ubuntu-with-nodejs
docker images
docker tag roberto/ubuntu-with-nodejs robertouj/ubuntu-with-nodejs
docker push robertouj/ubuntu-with-nodejs
docker pull robertouj/ubuntu-with-nodejs
docker rm robertouj/ubuntu-with-nodejs
docker image rm robertouj/ubuntu-with-nodejs 
docker stop suspicious_taussig
docker run --name test-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
docker run --name test-postgres -e POSTGRES_USER=mytestuser -e POSTGRES_PASSWORD=mytestuserpassword -d postgres
docker run --name test-postgres -e POSTGRES_PASSWORD=password -d -p 5432:5432 postgres
docker run --name test-postgres -e POSTGRES_USER=rhcodingtask -e POSTGRES_PASSWORD=rhcodingtaskpassword -d -p 5432:5432 postgres
docker rmi requarks/wiki:latest 
docker network ls
docker info
docker network create wikinet
docker run --name postgres-wiki -e POSTGRES_USER=wikiuser -e POSTGRES_PASSWORD=wikipassword -d -p 5432:5432 postgres
docker run --rm -p 5050:5050 -e PGADMIN_DEFAULT_EMAIL=robertouj -e PGADMIN_DEFAULT_PASSWORD=ruj dpage/pgadmin4:latest
docker run -d -p 8080:3000 --name wiki --restart unless-stopped -e "DB_TYPE=postgres" -e "DB_HOST=172.17.02" -e "DB_PORT=5432" -e "DB_USER=wiki" -e "DB_PASS=wikipassword" -e "DB_NAME=wiki" ghcr.io/requarks/wiki:2
docker inspect --format '{{ .NetworkSettings.IPAddress }}' wiki-db