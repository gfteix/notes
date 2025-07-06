---
created-date: 2024-04-24
tags:
  - tech
---

Docker before docker:
- chroot
- cgroups (limitação pro processo que está rodando)
- namespace (monta um ambiente isolado pro processo)

https://www.baeldung.com/linux/rootfs


Container é um processo ou um grupo de processos que usa o sistema operacional de forma isolada.

---

Creating a docker container for mysql

Pull MySQL image
`sudo docker pull mysql`

Start a MySQL container using the image, passing a password and a default database name

`sudo docker run --name mysql_docker -p 33060:3306 -e MYSQL_ROOT_PASSWORD=mysql123 -e MYSQL_DATABASE=projectmanager -d mysql`

Execute the mysql cli to be able to create tables, users, etc
`sudo docker exec -it mysql_docker mysql -p`

Dockerfile example:

```
FROM golang:1.22.0 AS build-stage
    WORKDIR /app

    COPY go.mod go.sum ./
    RUN go mod download

    COPY *.go ./

    RUN CGO_ENABLED=0 GOOS=linux go build -o /api

FROM build-stage as run-test-stage
    RUN go test -v ./...

FROM scratch as run-release-stage
    WORKDIR /app

    COPY --from=build-stage /api /api

    EXPOSE 8080

    CMD ["/api"]
```

## Docker Compose

Example
```
version: '3.8'

services:
  mysql_docker:
    image: mysql
    container_name: mysql_docker
    environment:
      MYSQL_ROOT_PASSWORD: mysql123
      MYSQL_DATABASE: projectmanager
    ports:
      - "33060:3306"
    restart: unless-stopped

  backend:
    build:
      context: .
      dockerfile: Dockerfile.backend
    depends_on:
      - mysql_docker
    network_mode: "host"
```

To start the docker-compose run this comand in the root of the project
`sudo docker-compose up -d`

To see the logs of the backend container:
`sudo docker-compose logs backend`