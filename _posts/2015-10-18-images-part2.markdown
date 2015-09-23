---
layout: topics
title:  "Working with Docker Images"
date:   2015-09-17 12:53:29
categories: docker part-1
---
#### 1.Listing Docker Images

{% highlight sh %}
$ sudo docker images
{% endhighlight %}
The command lists all the images in the local machine.
 <html>
 <body>
    <img  src="/images/docker/docker-images.png" width="1000" height="300">
 </body></html>

#### 2.Pulling Docker Images from DOCKER-HUB

 Docker Images can also be pulled from [DOCKER_HUB][dh] registry.
 {% highlight sh %}
$ sudo docker pull ubuntu
{% endhighlight %}
This command pulls the **ubuntu** image from dockerhub
<html>
 <body>
    <img  src="/images/docker/pulling-docker-images.png" height="300">
 </body></html>

#### 3.Image tags 
Each image inside the repository is identified by what Docker calls **tags**. Each image is being listed by the tags applied to it, so, for example, **12.04** , **12.10** , **quantal** , or **precise** and so on. Each tag marks together a series of image layers that represent a specific image 
(e.g., the 12.04 tag collects together all the layers
of the **Ubuntu 12.04** image). This allows us to store more than one image inside a repository. 

#### 4.Running the containers
{% highlight sh %}
$ sudo docker run -t -i --name new_container ubuntu /bin/bash
{% endhighlight %}

This command runs the container using ubuntu image and runs the command /bin/bash
<html>
 <body>
    <img  src="/images/docker/running-containers.png" height="300">
 </body></html>

 There are two types of repositories: **user repositories**, which contain images contributed by Docker users, and **top-level repositories**, which are controlled by the people behind Docker.

#### 5.Searching images
{% highlight sh %}
$ sudo docker search puppet
{% endhighlight %}
It’ll search images and return:
  
  * Repository names
  * Image descriptions
  * Stars - these measure the popularity of an image
  * Official - an image managed by the upstream developer (e.g., the fedora image managed by
  the Fedora team)       
  * Automated - an image built by the Docker Hub’s Automated Build process.

#### 6.Pulling a particular image
{% highlight sh %}
$ sudo docker pull jamtur01/puppetmaster
{% endhighlight %}

Pulls jamtur01/puppetmaster image

#### 7.Building Docker Images
We can create our own Docker images using two methods:

  * Via the **docker commit** command (**NOT Recommended**)
  * Via the **docker build** command with [Dockerfile][dfile]

<a href="images.html"><<Introduction to Docker Images</a> 
<a style = "float:right" href="docker-hub.html">Dockerhub>></a>

[dh]: https://hub.docker.com/
[dfile]: dockerfile.html

