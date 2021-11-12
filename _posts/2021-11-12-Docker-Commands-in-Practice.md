---
layout: post
title: Docker Commands in Practice
category: 
    - "Data Science"
    - "MLOps"
---

## General Usage

### Start a container in background
{% highlight shell %}
docker run -d IMAGE_NAME
{% endhighlight %}

### Start an interactive container
{% highlight shell %}
docker run -it IMAGE_NAME bash
{% endhighlight %}

### Export port from a container
{% highlight shell %}
docker run -p 80:80 -d IMAGE_NAME
{% endhighlight %}

### Start a named container
{% highlight shell %}
docker run --name CONTAINER_ID IMAGE_NAME
{% endhighlight %}

### Restart a stopped container
{% highlight shell %}
docker start CONTAINER_ID
{% endhighlight %}

### Stop a container
{% highlight shell %}
docker stop CONTAINER_ID
{% endhighlight %}


## Build Images

### Build an image from Dockerfile in current directory
{% highlight shell %}
docker build --tag IMAGE_NAME .
{% endhighlight %}

### Force rebuild of Docker image
{% highlight shell %}
docker build --no-cache .
{% endhighlight %}

### Convert a container to image
{% highlight shell %}
docker commit CONTAINER_ID IMAGE_NAME
{% endhighlight %}

### Remove all unused images
{% highlight shell %}
docker image prune --all
{% endhighlight %}



## Manage Containers

### List running containers
{% highlight shell %}
docker ps
{% endhighlight %}

### List all containers (running & stopped)
{% highlight shell %}
docker ps -a
{% endhighlight %}

### Inspect containers metadata
{% highlight shell %}
docker inspect CONTAINER_ID
{% endhighlight %}

### List local available images
{% highlight shell %}
docker images
{% endhighlight %}

### Delete all stopped containers
{% highlight shell %}
docker container prune
{% endhighlight %}

### List all containers with a specific label
{% highlight shell %}
docker ps --ﬁlter label=LABEL
{% endhighlight %}


## Debug

### Run another process in running container
{% highlight shell %}
docker exec -it CONTAINER_ID bash
{% endhighlight %}

### Show live logs of running daemon container
{% highlight shell %}
docker logs -f CONTAINER_ID
{% endhighlight %}

### Show exposed ports of a container
{% highlight shell %}
docker port CONTAINER_ID
{% endhighlight %}


## Volumes

### Create a local volume
{% highlight shell %}
docker volume create --name VOLUME_NAME
{% endhighlight %}

### Mounting a volume on container start
{% highlight shell %}
docker run -v VOLUME_NAME:/data IMAGE_NAME
{% endhighlight %}

### Destroy a volume
{% highlight shell %}
docker volume rm VOLUME_NAME
{% endhighlight %}

### List volumes
{% highlight shell %}
docker volume ls
{% endhighlight %}


## Networking

### Create a local network
{% highlight shell %}
docker network create NETWORK_NAME
{% endhighlight %}

### Attach a container to a network on start
{% highlight shell %}
docker network create NETWORK_NAME IMAGE_NAME
{% endhighlight %}

### Connect a running container from a network
{% highlight shell %}
docker network connect NETWORK_NAME CONTAINER_ID
{% endhighlight %}

### Disconnect container to a network
{% highlight shell %}
docker network disconnect NETWORK_NAME CONTAINER_ID
{% endhighlight %}
