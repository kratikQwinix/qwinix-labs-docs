---
layout: topics
title:  "Sinatra"
date:   2015-09-22 12:00:32
categories: docker part-3
---
###Dockerise a Sinatra Application

#### Build a Sinatra Application

Create a directory for your application.

{% highlight sh %}
$ mkdir -p sinatra/my_app
$ cd sinatra/my_app
{% endhighlight %}

Create a dockerfile inside the directory to build the image required to build the sinatra app. 

{% highlight sh %}
$ touch Dockerfile
{% endhighlight %}

	FROM ubuntu
	
	RUN apt-get update
	RUN apt-get -y install ruby ruby-dev build-essential redis-tools
	RUN gem install --no-rdoc --no-ri sinatra json redis
	
	RUN mkdir -p /opt/webapp
	
	EXPOSE 4567
	
	CMD ["/bin/webapp"]

The above dockerfile does the following<br>
1. Uses Ubunutu as the base image.<br>
2. Run apt-get<br>
3. Run command to install ruby and ruby gems.<br>
4. Run gem install to install sinatra, json and redis.<br>
5. Create a directory /opt/webapp.<br>
6. Expose the port 4567 inside the container.<br>
7. Executes the command /opt/webapp/bin/webapp in the container which will launch the application.<br>

<hr>

Build the image using docker build

{% highlight sh %}
$ sudo docker build -t pruthvik/sinatra .
{% endhighlight %}

<img src="/images/ruby-sinatra/docker-sinatra-image-build.png">

Launch the sinatra container.

{% highlight sh %}
$ sudo docker run -d -p 4567 --name webapp -v $PWD:/opt/webapp pruthvik/sinatra
{% endhighlight %}

Check the port binding of the container using

{% highlight sh %}
$ sudo docker ps
{% endhighlight %}

<img src="/images/ruby-sinatra/docker-sinatra-dockerps.png">

{% highlight sh %}
$ curl -i -H 'Accept: application/json' -d 'name=Foo&status=Bar' http://localhost:49160/json
{% endhighlight %}

<img src="/images/ruby-sinatra/sinatra-app-check.png">

<hr>

#### Build a Redis Image Container

To add a redis backend to the app and store incoming url parameters in a redis database a new image and separate container should be run and with the help of docker link, both the containers can be connected.

Create a directory for files associated to build the redis image.

{% highlight sh %}
$ mkdir -p sinatra/redis
$ cd sinatra/redis
{% endhighlight %}

Create a dockerfile inside the directory to build the image required to build the redis image. 

{% highlight sh %}
$ touch Dockerfile
{% endhighlight %}

	FROM ubuntu:14.04

	RUN apt-get -yqq update && apt-get -yqq install redis-server redis-tools

	EXPOSE 6379

	ENTRYPOINT ["/usr/bin/redis-server"]
	CMD []

Build the image using docker build

{% highlight sh %}
$ sudo docker build -t pruthvik/redis .
{% endhighlight %}

<img src="/images/ruby-sinatra/redis-image-build.png">

Launch the redis container

{% highlight sh %}
$ sudo docker run -d -p 6379 --name redis pruthvik/redis
{% endhighlight %}

<hr>

#### 	Link the sinatra container to the redis container using docker link.

{% highlight sh %}
$ sudo docker run -p 4567 --name webapp --link redis:db -t -i -v $PWD/my_app:/opt/webapp pruthvik/sinatra /bin/bash
{% endhighlight %}

Here, first port **4567** is exposed using the **-p** flag so that the application can be accessed externally.

The container is named **webapp** using the **- 	-name** flag.

The web application is mounted using the **-v** flag.

The **- -link** flag creates a parent-child link between containers. The flag takes two arguments: the container name to link and an alias for the link, in this case the container being linked is **redis** with an alias of **db**.
The link gives the parent container the ability to communicate with the child container and shares some connection details with it to help configure applications to make use of the link.

The bin/bash command is executed and instead of running the container as a daemon, the shell is launched.

The env command can be used to check the environment variables, which are used by the application to connect to the container.

{% highlight sh %}
root@4ef9b80f06c9:/# env
{% endhighlight %}

The DB_PORT refers to the IP of the container assigned by docker and the port on which redis is running.

{% highlight sh %}
require 'redis'
	.
	.
redis = Redis.new(:host => 'db', :port => '6379')
	.
	.
{% endhighlight %}

The above should be added to the **app.rb** file to connect the sinatra application to the redis db.

To check if the application is using the redis db. It can be seen below

{% highlight sh %}
$ curl -i -H 'Accept: application/json' -d 'name=Foo&status=Bar' http://localhost:32789/json
{% endhighlight %}

<img src="/images/ruby-sinatra/sinatra-app-test.png">

{% highlight sh %}
$ curl -i http://localhost:32789/json
{% endhighlight %}

<img src="/images/ruby-sinatra/sinatra-redis-check.png">

