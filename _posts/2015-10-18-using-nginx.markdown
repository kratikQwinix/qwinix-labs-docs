---
layout: topics
title:  "Using Nginx"
date:   2015-09-17 12:53:32
categories: docker part-4
---

### Dockerizing a static web page using  NGINX

Dockerizing a static web page involves 

* Writing a Dockerfile. 
* Building an image using DOckerfile.
* Running the image in a container.

<hr>

### Writing a Dockerfile

1.The Dockerfile helps in building images,which is basically sequence of instructions consisting of various types of instructiions like CMD , ENTRYPOINT , ADD , COPY , VOLUME , WORKDIR , USER , ONBUILD and ENV.

2.The building of images using Dockerfile involves building it on base images which are present in the dockerhub.

3.In the current example we have written a very simple dockerfile involving FROM and CMD

4.The Dockerfile should be placed in the same folder which contains the webpage.

	FROM nginx
	EXPOSE 80
	RUN mkdir -p /usr/share/nginx/html
	ADD . /usr/share/nginx/html
	CMD ["nginx","-g","daemon off;"]
<hr>

### Building an image using Dockerfile

	1. $ sudo docker build -t manamohan/webapp .

<img src="{{site.baseurl}}/images/docker/static_webpage/docker_build.png">

  This commands builds the image using the dockerfile. All the instructions are exexuted step by step and finally the ID of the image will be created and returned on successfull building of image. 

 <b>NOTE:-</b> "manamohan/webapp" is the name of the image("username/imagename", just a convention).

  This process can be verified by listing the images using

    $sudo docker images

<img src="{{site.baseurl}}/images/docker/static_webpage/docker_images.png">

<hr>

### Running the image in a conatiner

1)Run the following command in you terminal

	$ sudo docker run -p 80:80 -d -v $PWD/static_webapp:/usr/share/nginx/html  manamohan/webapp 
  
     -p flag manages which network ports Docker exposes at runtime.</b>
      (maps port 80 of host machine to port 80 of the container).
     -d makes the container to run in detached mode.**
     -v is the flag used to mount volumes to a container.**

<img src="{{site.baseurl}}/images/docker/static_webpage/docker_run.png">

2.Run the localhost:80 in the web browser to see the containerized webpage which is present	in static_web folder.

<img src="{{site.baseurl}}/images/docker/static_webpage/docker_nginx_output.png">
