---
layout: topics
title:  "Rails"
date:   2015-09-17 11:05:32
categories: docker part-3
---

A **RoR** app generally involves a database running at the backend which will be accessed by a
rails application for various **CRUD operations**. So dockerizing a rails app can be done by
linking 2 containers ie., rails app and database running in two separate containers.
	Dockerizing the RoR app involves the following steps

#### 1.Writing the dockerfile

#### 2.Configuring using Docker-compose

#### 3.Running the dockerized app

<hr>

#### 1.The DockerFile
Dockerfile for containerizing a **RoR*** app can be written as the following:

<html>
 <body>
    <img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/ROR_Dockerfile.png" width="1000" height="300">
 </body></html>


**line1**: Uses the ruby:latest image as the base image

**line2**:Updates the ubuntu packages(-qq  :logs only when there is an error, -y : selects yes for confirmation)

**line3**:Installs rails

**line4**:Installs nodejs

**line5**:creates a directory app/v1

**line6**: setting environment variable LOC to app/v1

**line7**:sets LOC as Working directory

**line8**:Adds all the gemfiles to LOC

**line9**:Runs bundle install

**line10**: Adds everything to LOC

<hr>

#### 2.Configuring using Docker-compose

Compose is a tool for defining and running multi-container applications with Docker. With Compose, you define a multi-container application in a single file, then spin your application up in a single command which does everything that needs to be done to get it running.

Using Compose is basically a three-step process.

**(a)**Define your app’s environment with a [Dockerfile][dofi] so it can be reproduced anywhere.

**(b)**Define the services that make up your app in **docker-compose.yml** so they can be run together in an isolated environment:

**(c)**Lastly, run **docker-compose up** and Compose will start and run your entire app.

A **docker-compose.yml** file looks like this:

<html>
 <body>
    <img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/docker-compose.png" width="1000" height="300">
 </body></html>

In the **docker_compose.yml** file we specify the configuration of database(**db**)
### **This file follows strict indentation** 

The database used for this app is **postgres** which we specify as the base image and also on which port it should run.

In the next section( **web**) we specify what all actions to take place when the container is launched.

**build:** builds image

**command:** specifies the command to be executed on running the conatiner

**ports:** specify the ports

**volume:** loads host directory as a volume on to the container

**links:** links the container

<hr>

####3.Running the dockerized app
This is done by using the command 

{% highlight sh %}
$ docker-compose up
{% endhighlight %}

This command builds the images and launches the container 

<html>
 <body>
    <img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/docker-compose_up.png" width="1000" height="800">
 </body></html>

We can see that all the instructions specified in the [Dockerfile][d] getting executed in an order.
<hr>

The **Dockerized Rails App** can be viewed in the browser by typing **localhost:3000** in the browser window.
<html>
 <body>
    <img  src="{{site.baseurl}}/images/docker/ruby_app/ROR/dockerized.png" width="500" height="300">
 </body></html>

<hr>
Since we have done data mounting using volumes, the changes in the app can be viewed the localhost by just **refresh**ing the page on the browser.














[dofi]: dockerfile.html
[d]: dockerfile.html