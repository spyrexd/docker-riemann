# docker-riemann

This project provides resources for deploying Riemann in Docker.

## Image Platform

RHEL6

## Image Dependencies

EPEL for RHEL6
Riemann RPM from <http://riemann.io>

## Building

To build the Riemann image, run:

```shell
$ docker build -t riemann .
```

## Launching Riemann

To launch Riemann, run:

```shell
$ docker run riemann
```

## Graphite Forwarding

To enable Graphite forwarding, copy the graphite configuration file from the
"optional" directory and rebuild the image:

```shell
$ cp optional/graphite.clj riemann.d/
$ docker build -t riemann-graphite .
```

This image expects to communicate with the Graphite host using the hostname
"graphite". If Graphite is running as another container, you could link Riemann
as so:

```shell
$ docker run -d --link graphite:graphite --name riemann-graphite riemann-graphite
```

## InfluxDB Forwarding

To enable InfluxDB forwarding, copy the InfluxDB configuration file from the
"optional" directory and rebuild the image:

```shell
$ cp optional/influxdb.clj riemann.d/
$ docker build -t riemann-influxdb .
```

This image expects to communicate with the InfluxDB host using the hostname
"influxdb". If InfluxDB is running as another container, you could link Riemann
as so:

```shell
$ docker run -d --link influxdb:influxdb --name riemann-influxdb riemann-influxdb
```

## Networking

The Riemann image exposes port 5555 to accept events from clients and port 5556
for the websocket server.

## Entrypoints

The Riemann image defines an entrypoint which runs `/usr/bin/riemann`.
