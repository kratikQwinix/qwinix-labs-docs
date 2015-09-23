---
layout: topics
title:  "Rails"
date:   2015-09-17 11:05:32
categories: docker part-3
---

A **RoR** app generally involves a database running at the backend which will be accessed by a rails application for various **CRUD operations**. So dockerizing a rails app can be done by
linking 2 containers ie., rails app and database running in two separate containers.

Dockerizing the RoR app involves the following steps

#### 1.Writing the dockerfile

#### 2.Configuring using Docker-compose

#### 3.Running the dockerized app

<hr>

#### 1.The DockerFile
Dockerfile for containerizing a **RoR*** app can be written as the following:

		FROM ruby
		RUN apt-get update -qq && apt-get install -y build-essential
		RUN apt-get install -y libpq-dev
		RUN apt-get install -y libxml2-dev libxslt1-dev nodejs
		 
		ENV APP_HOME /app/test_app
		RUN mkdir -p $APP_HOME
		WORKDIR $APP_HOME

		ADD Gemfile* $APP_HOME/
		RUN bundle install

		ADD . $APP_HOME


**line1**: Uses the ruby:latest image as the base image

**line2**:Updates the ubuntu packages(-qq  :logs only when there is an error, -y : selects yes for confirmation)

**line3**:Installs postgres

**line4**:Installs nodejs

**line5**:creates a directory app/test_app

**line6**: setting environment variable APP_HOME to app/test_app

**line7**:sets APP_HOME as Working directory

**line8**:Adds all the gemfiles to APP_HOME

**line9**:Runs bundle install

**line10**: Adds everything to APP_HOME

<hr>

#### 2.Configuring using Docker-compose

Compose is a tool for defining and running multi-container applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.

Using Compose is basically a three-step process.

**(a)**Define your app’s environment with a [Dockerfile][dofi] so it can be reproduced anywhere.

**(b)**Define the services that make up your app in **docker-compose.yml** so they can be run together in an isolated environment:

**(c)**Lastly, run **docker-compose up** and Compose will start and run your entire app.

A **docker-compose.yml** file looks like this:

{% highlight ruby %}
db:
  image: postgres
  ports:
    - "5432:5432"

web:
  build: .
  command: bin/rails server --port 3000 --binding 0.0.0.0
  ports:
    - "3000:3000"
  links:
    - db
  volumes:
    - /home/lucifer/rails_apps/test_app:/app/test_app
{% endhighlight %}

In the **docker-compose.yml** file we specify the containers that need to be running for the whole application.
#### **This file follows strict indentation** 

The first container **db** used for this app uses the **postgres** image and ports are exposed as 5432 in the container bound to 5432 on localhost.

In the next container **web** the image is not specified unlinke db, but the image is built using a *Dockerfile*.

**image:** image used to run in the container.

**build:** build the image.

**command:** specifies the command to be executed on running the conatiner.

**ports:** specifies port binding.

**volume:** mounts host directory as a volume on to the container.

**links:** links the containers.

<hr>

####3. The database.yml file of the rails application to use postfgres db.

{% highlight ruby %}
development:
 adapter: postgresql
 pool: 5
 username: postgres
 password: password
 database: postgres
 host: <%= ENV['DB_PORT_5432_TCP_ADDR'] %>
 port: <%= ENV['DB_PORT_5432_TCP_PORT'] %>
{% endhighlight %}

 **host: <%= ENV['DB_PORT_5432_TCP_ADDR'] %>**
 **port: <%= ENV['DB_PORT_5432_TCP_PORT'] %>**

The apllication must be able to access the postgres running in the container db. We can directly use the ip address of the container and the port on which its running directly, but it isn't a good practice because ip address of the container changes everytime the containers is restarted. Hence, its a good practice to use environment variables.

Docker provides with env variables within the container, this can be viewed using the command 

	$ docker-compose run web env

<img src="{{site.baseurl}}images/docker/ruby_app/ROR/rails-docker-compose.png">

The ENV variables can be copied and listed in the application's database.yml file.

<hr>

####4. Starting the containers.

This is done by using the command 

{% highlight sh %}
$ docker-compose up
{% endhighlight %}

This will build the images and launches the containers in the order of *docker-compose.yml* file as seen below.. 

<img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/docker-compose_up.png" width="1000">

We can see that all the instructions specified in the [Dockerfile][d] getting executed in an order.
<hr>

The **Dockerized Rails App** can be viewed in the browser by typing **localhost:3000** in the browser window.

<img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/dockerized.png" >

Since we have done data mounting using volumes, the changes in the app can be viewed the localhost by just **refresh**ing the page on the browser.


[dofi]: dockerfile.html
[d]: dockerfile.html