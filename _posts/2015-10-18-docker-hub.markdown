---
layout: topics
title:  "Docker Hub"
date:   2015-09-17 12:53:29
categories: docker part-1
---

### Docker Hub

The Docker Hub is a cloud-based registry service for building and shipping application or service containers. It provides a centralized resource for container image discovery, distribution and change management, user and team collaboration, and workflow automation throughout the development pipeline.

<img src="{{site.baseurl}}/images/docker/docker_basics/docker_hub.png">

### Specifically, Docker Hub provides the following major features and functions:

  * **Image Repositories**: Find, manage, and push and pull images from community, official, and private image libraries.

  * **Automated Builds**: Automatically create new images when you make changes to a source GitHub or Bitbucket repository.

  * **Webhooks**: A feature of Automated Builds, Webhooks let you trigger actions after a successful push to a repository.

  * **Organizations**: Create work groups to manage user access to image repositories.
	
  * **GitHub and Bitbucket Integration**: Add the Hub and your Docker Images to your current workflows.

### Docker Hub Account
To explore Docker Hub, you’ll need to create an account by following the directions in Hub Accounts

### Docker commands
	
Docker itself provides access to Docker Hub services via the docker search, pull, login, and push commands.


	$ docker search ubuntu
	$ docker pull ubuntu
	$ docker push ubuntu
	$ docker login
	

<a href="images.html"><<Images</a> 
<a style = "float:right" href="dockerfile.html">Dockerfile>></a> 
