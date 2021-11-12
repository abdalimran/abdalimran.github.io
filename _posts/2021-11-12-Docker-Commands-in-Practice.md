---
layout: post
title: Docker Commands in Practice
category: 
    - "Data Science"
    - "MLOps"
---

## General Usage

### Start a container in background
{% highlight python %}
$> docker run -d jenkins
{% endhighlight %}

### Start an interactive container
{% highlight python %}
$> docker run -it ubuntu bash
{% endhighlight %}

### Export port from a container
{% highlight python %}
$> docker run -p 80:80 -d nginx
{% endhighlight %}

### Start a named container
{% highlight python %}
$> docker run --name mydb redis
{% endhighlight %}

### Restart a stopped container
{% highlight python %}
$> docker start mydb
{% endhighlight %}

### Stop a container
{% highlight python %}
$> docker stop mydb
{% endhighlight %}

### Add metadata to container
{% highlight python %}
$> docker run -d label=traefik.backend=jenkins jenkins
{% endhighlight %}