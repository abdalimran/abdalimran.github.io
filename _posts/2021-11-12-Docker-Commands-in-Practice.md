---
layout: post
title: Docker Commands in Practice
category: 
    - "Data Science"
    - "MLOps"
---

## General Usage

### Start a container in background
{% highlight console %}
docker run -d <IMAGE_NAME>
{% endhighlight %}

### Start an interactive container
{% highlight console %}
docker run -it <IMAGE_NAME> bash
{% endhighlight %}

### Export port from a container
{% highlight console %}
docker run -p 80:80 -d <IMAGE_NAME>
{% endhighlight %}

### Start a named container
{% highlight console %}
docker run --name <CONTAINER_ID> <IMAGE_NAME>
{% endhighlight %}

### Restart a stopped container
{% highlight console %}
docker start <CONTAINER_ID>
{% endhighlight %}

### Stop a container
{% highlight console %}
docker stop <CONTAINER_ID>
{% endhighlight %}

### Add metadata to container
{% highlight console %}
docker run -d label=traefik.backend=<IMAGE_NAME> <IMAGE_NAME>
{% endhighlight %}

## Build Images

### Build an image from Dockerfile in current directory
{% highlight console %}
docker build --tag <IMAGE_NAME> .
{% endhighlight %}

### Force rebuild of Docker image
{% highlight console %}
docker build --no-cache .
{% endhighlight %}

### Convert a container to image
{% highlight console %}
docker commit <CONTAINER_ID> <IMAGE_NAME>
{% endhighlight %}

### Remove all unused images
{% highlight console %}
docker image prune --all
{% endhighlight %}

## Manage Containers

### List running containers
{% highlight console %}
docker ps
{% endhighlight %}

### List all containers (running & stopped)
{% highlight console %}
docker ps -a
{% endhighlight %}

### Inspect containers metadata
{% highlight console %}
docker inspect <CONTAINER_ID>
{% endhighlight %}

### List local available images
{% highlight console %}
docker images
{% endhighlight %}

### Delete all stopped containers
{% highlight console %}
docker container prune
{% endhighlight %}

### List all containers with a specific label
{% highlight console %}
docker ps --ﬁlter label=<LABEL>
{% endhighlight %}

### Query a specific metadata of a running container
{% highlight console %}
docker inspect -f '{{ .NetworkSettings.IPAddress }}' <CONTAINER_ID>
{% endhighlight %}

## Debug

### Run another process in running container
{% highlight console %}
docker exec -it <CONTAINER_ID> bash
{% endhighlight %}

### Show live logs of running daemon container
{% highlight console %}
docker logs -f <CONTAINER_ID>
{% endhighlight %}

### Show exposed ports of a container
{% highlight console %}
docker port <CONTAINER_ID>
{% endhighlight %}

## Volumes

### Create a local volume
{% highlight console %}
docker volume create --name <VOLUME_NAME>
{% endhighlight %}

### Mounting a volume on container start
{% highlight console %}
docker run -v <VOLUME_NAME>:/data <IMAGE_NAME>
{% endhighlight %}

### Destroy a volume
{% highlight console %}
docker volume rm <VOLUME_NAME>
{% endhighlight %}

### List volumes
{% highlight console %}
docker volume ls
{% endhighlight %}

## Networking

### Create a local network
{% highlight console %}
docker network create <NETWORK_NAME>
{% endhighlight %}

### Attach a container to a network on start
{% highlight console %}
docker network create <NETWORK_NAME> <IMAGE_NAME>
{% endhighlight %}

### Connect a running container from a network
{% highlight console %}
docker network connect <NETWORK_NAME> <CONTAINER_ID>
{% endhighlight %}

### Disconnect container to a network
{% highlight console %}
docker network disconnect <NETWORK_NAME> <CONTAINER_ID>
{% endhighlight %}
