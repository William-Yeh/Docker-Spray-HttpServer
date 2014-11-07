Docker-Spray-HttpServer
========================

## Summary

Repository name in Docker Hub: **[williamyeh/spray-httpserver](https://registry.hub.docker.com/u/williamyeh/spray-httpserver/)**

This repository contains Dockerized [spray-can simple-http-server example](http://spray.io/documentation/1.1-SNAPSHOT/spray-can/examples/#simple-http-server), published to the public [Docker Hub](https://registry.hub.docker.com/) via **automated build** mechanism.

The app is mainly used as a benchmark target for evaluating the performance of [Akka](http://akka.io/) + [Spray](http://spray.io/) framework.


## Configuration

This docker image contains the following software stack:

- OS: Debian jessie.

- Java: Oracle JDK 1.7.0

- Scala: 2.11.4

- Sbt

- [spray-can simple-http-server example](http://spray.io/documentation/1.1-SNAPSHOT/spray-can/examples/#simple-http-server), built on top of [Akka](http://akka.io/) + [Spray](http://spray.io/) framework.


### Dependencies

- [williamyeh/scala](https://github.com/William-Yeh/docker-scala)


### History

- 0.1 - Initial release.


## Installation

   ```
   $ docker pull williamyeh/spray-httpserver
   ```


## Usage

Basic usage:

   ```
   $ docker run williamyeh/spray-httpserver
   ```

Expose HTTP port:

   ```
   $ docker run -p 8080:8080 williamyeh/spray-httpserver
   ```

Pass additional JVM options:

   ```
   $ docker run williamyeh/spray-httpserver \
         -XX:+UseG1GC -Xms8G -Xmx8G -XX:+PrintGCDetails
   ```

## API Endpoints

List all endpoints of the server:

   ```
   $ curl http://CONTAINER_IP:8080/
   ```

## Benchmark

First, start the server (preferably in daemon mode) with a name (e.g., `spray`):

   ```
   $ docker run -d --name spray williamyeh/spray-httpserver
   ```

Next, benchmark the server with `wrk` (Dockerized version [`williamyeh/wrk`](https://github.com/William-Yeh/docker-wrk)).

Simple benchmark - HTML content:

   ```
   $ docker run --link spray:httpserver williamyeh/wrk  \
         http://httpserver:8080/
   ```

Short text benchmark - test the "ping/pong" service:

   ```
   $ docker run --link spray:httpserver williamyeh/wrk  \
         http://httpserver:8080/ping
   ```

Short text + server logging benchmark - test the "echo" service:

   ```
   $ docker run --link spray:httpserver williamyeh/wrk  \
        http://httpserver:8080/echo/the_text_to_be_echoed
   ```
