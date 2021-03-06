## Exercise

- Write a Dockerfile
- Build image
- Run container
- Make API call to serivce

----

## Write a Dockerfile 

(example)

```
FROM golang:1.6

COPY . /go/src/github.com/codenode-workshop/deals

RUN go install github.com/codenode-workshop/deals

ENTRYPOINT /go/bin/deals

EXPOSE 8080
```

----

## Build and Run Docker image

```bash
cd microserivces/v1/
docker build -t codenode-workshop/deals:v1 .
docker run -d --publish 8080:8080 codenode-workshop/deals:v1
```

----

## Call service

```bash
curl localhost:8080/deals?id=1
```

----

## Stop and remove container

```bash
docker stop $(docker ps -ql)
docker rm $(docker ps -ql
```

----

## Add a Database (v2)

`open v2/main.go`

----

## Build and Run

```bash
cd v2/
docker build -t codenode-workshop/deals:v2 .
docker network create my_network
docker run --name deals-db -d --network my_network mongo
docker run -d -p 8080:8080 --network my_network codenode-workshop/deals:v2
```

----

## Clean up

```bash
docker stop $(docker ps -ql)
docker rm $(docker ps -ql
```

----

## V2 of service, with Database

./microservices/v2/

----

## Docker Compose

`vi docker-compose.yml`

```bash
version: '2'

services:
  deals:
    build: .
    ports:
      - 8080:8080
    hostname: deals
  deals-db:
    image: mongo:3.0
    hostname: deals-db
```

----

## Call service

`curl localhost:8080/deals?id=1`

----

## Clean up

`docker-compose down`

----

## Review

* Questions?
* Stop and remove *this* container
