---
layout: topics
title:  "Introduction to Docker"
date:   2015-09-17 12:53:32
categories: docker part-1
---
### Getting started with docker.

#### 1. Installation on Ubuntu 14.04.

There are no prerequistes for Ubuntu 14.04 or later.

Check if curl is installed.

{% highlight sh %}
 $ which curl
{% endhighlight %}

If curl isn’t installed, install it after updating your manager:

{% highlight sh %}
 $ sudo apt-get update
 $ sudo apt-get install curl
{% endhighlight %}

Download the latest docker package.

{% highlight sh %}
 $ curl -sSL https://get.docker.com/gpg | sudo apt-key add -
{% endhighlight %}

Verify if docker is installed.

{% highlight sh %}
 $ sudo docker run hello-world
{% endhighlight %}
