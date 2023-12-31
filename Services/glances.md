# Glances - An eye on your system

**Glances** is an open-source system cross-platform monitoring tool. It allows real-time monitoring of various aspects of your system such as CPU, memory, disk, network usage etc. It also allows monitoring of running processes, logged in users, temperatures, voltages, fan speeds etc. It also supports container monitoring, it supports different container management systems such as Docker, LXC. The information is presented in an easy to read dashboard and can also be used for remote monitoring of systems via a web interface or command line interface. It is easy to install and use and can be customized to show only the information that you are interested in.

Github: [nicolargo/glances](https://github.com/nicolargo/glances)

![](https://raw.githubusercontent.com/nicolargo/glances/develop/docs/_static/glances-summary.png)

Glances is written in Python and uses libraries to grab information from your system. It is based on an open architecture where developers can add new plugins or exports modules.

## Gateway to other services

Glances can export stats to: `CSV` file, `JSON` file, `InfluxDB`, `Cassandra`, `CouchDB`, `OpenTSDB`, `Prometheus`, `StatsD`, `ElasticSearch`, `RabbitMQ/ActiveMQ`, `ZeroMQ`, `Kafka`, `Riemann`, `Graphite` and `RESTful` server.

In client/server mode, remote monitoring could be done via terminal, Web interface or API (XML-RPC and RESTful). Stats can also be exported to files or external time/value databases, CSV or direct output to STDOUT.

To run any of these command below you'll have to enter continers console.
which is not covered under the scope of this guide (atleast for now)

```bash
glances --stdout cpu.user,mem.used,load
```

or in a CSV format thanks to the stdout-csv option:

```shell
glances --stdout-csv now,cpu.user,mem.used,load
```

or in a JSON format thanks to the stdout-json option (attribute not supported in this mode in order to have a real JSON object in output):

```shell
glances --stdout-json cpu,mem
```

## Documentation

For complete documentation have a look at the [readthedocs](https://glances.readthedocs.io/en/latest/quickstart.html) website.

## Installation with Docker-compose

Start by creating docker compose file

We'll make a directory named glances under home/username/docker/

```bash
mkdir -p /home/username/docker/glances
cd /home/username/docker/glances
```

Create a docker-compose.yml file in this directory

```bash
nano docker-compose.yml
```

```yml
version: '3'

services:
  monitoring:
    image: nicolargo/glances:latest-full
    pid: host
    network_mode: host #this enables this container to be on host network hence be able to monitor host network metrics
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock #enables docker client inside container communicate to docker daemon on host machine
      - /run/user/1000/podman/podman.sock:/run/user/1000/podman/podman.sock
    environment:
      - "GLANCES_OPT=-w" #enables glances to run in -w aka webserver mode by default
    # For nvidia GPUs (if you nvidia gpu(s) use this below)
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]      
```

## Can I change port number ?

When you use the host network mode (`--network=host`), the Docker container does not have its own IP address, and it shares the network namespace with the host.
As a result, port mapping does not take effect, and the -p or --publish options are ignored. If we want to use a different port with host network mode, we would need to configure our application to listen on the desired port before starting the container. This means changing the application’s configuration so that it listens on the new port, and then starting the container with --network=host. 

In conclusion, the only way to use host mode and a specific port number is by modifying the application code itself, which is beyond the scope of this guide.

Build the Docker container

```bash
docker compose up -d
```

Expected outcome

```
[+] Running 1/1
 ✔ Container glances-monitoring-1  Started
```

Verify Docker container is up and running and is healthy if yes then move forward

```
docker ps
```

## Accessing the WEB GUI

Simply navigate to `127.0.0.1:61208`

and be greeted with UI as shown below

![](https://i.imgur.com/nwDlMfT.png)

Now you can monitor your Linux system resources from this URL

## Accessing from Outside Network

These are few ways how we can go about doing that

1. If you have a domain name such as example.com
   then you might wanna setup a reverse proxy using
   
   - Nginx Proxy Manager
   
   - [Cloudflare Tunnel](https://github.com/godarayudhvir/shownotes/blob/main/Cloudflare/cf_tunnel.md)
   
   - Traefik
   
   - & More

2. If you don't have a domain name or don't want public accessing it
   setup VPN one of the following services
   
   - Tailscale
   
   - Twingate
   
   - & More
