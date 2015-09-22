---
layout: topics
title:  "Introduction to Docker"
next: "Containers"
date:   2015-09-17 12:53:32
categories: docker part-1
---
##Getting started with docker

### 1. Installation on Ubunutu

There are no prerequistes for ubuntu 14.04 and higher.

1. Log into ubuntu as a user with **sudo** priveleges.

2. Verify if you have curl installed on your system.

	{% highlight sh %}
	$ which curl
	{% endhighlight %}

If curl isn't installed, install it wiht the following commands

	{% highlight sh %}
	$ sudo apt-get update
$ sudo apt-get install curl
	{% endhighlight %}

3. Get the latest Docker package.

	{% highlight sh %}
	$ curl -sSL https://get.docker.com/gpg | sudo apt-key add -
	{% endhighlight %}

4. Verify docker is installed correctly

	{% highlight sh %}
	$ sudo docker run hello-world
	{% endhighlight %}



<a href="containers.html" style = "float:right">Containers>></a> 


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
