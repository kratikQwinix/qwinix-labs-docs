---
layout: topics
title:  "Dockerfile"
date:   2015-09-17 12:53:28
categories: docker part-1
---

### Dockerfile

Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.
Dockerfiles begin with defining an image FROM which the build process starts. Followed by various other methods, commands and arguments (or conditions), in return, provide a new image which is to be used for creating docker containers.

<hr>

### Docker file instructions

#### 1)FROM

FROM directive is probably the most crucial amongst all others for Dockerfiles. It defines the base image to use to start the build process. It can be any image, including the ones you have created previously. If a FROM image is not found on the host, docker will try to find it (and download) from the docker image index. It needs to be the first command declared inside a Dockerfile.

Example:
	
	FROM [image name]
	FROM ubuntu

<hr>

#### 2)RUN

The RUN instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.

RUN has 2 forms:
  
  a) RUN <command>  (the command is run in a shell - /bin/sh -c is shellform) <br>
  b) RUN ["executable", "param1", "param2"](exec form)
eg:-	


	RUN apt-get update
	RUN apt-get install -y nginx

<hr>

#### 3) CMD :-		
 The CMD instruction specifies the command to run when a container is launched. It is similar to the RUN instruction, but  rather than running the command when the container is being built, it will specify the command to run when the container is launched

	$ sudo docker run -i -t ubuntu /bin/bash
  
  here:-

* **sudo:- gives Super User permission**

* **run :- will run the image in our container**
* **-i,--interactive=false :-Keep STDIN open even if not 										attached**
* **-t , --tty=false :- Allocate a pseudo-TTY**
* **ubuntu:-  is our image name**
* **/bin/bash :- will run bash shell in the container 						which has ubuntu image**

This would be articulated in the Dockerfile as:

<b>CMD ["/bin/bash"] </b>

Passing parameters to the CMD instruction

<b>CMD ["/bin/bash", "-l"] </b>


Lastly, it’s important to understand that we can override the CMD instruction using the docker run command. If we specify a CMD in our Dockerfile and one on the docker run command line, then the command line will override the Dockerfile’s CMD instruction.You can only specify one CMD instruction in a Dockerfile. If more than one is specified, then the last CMD instruction will be used


<hr>

#### 4)ENTRYPOINT :-

Closely related to the CMD instruction.The ENTRYPOINT instruction provides a command that isn’t as easily overridden. Instead, any arguments we specify on the docker run command line will be passed as arguments to the command specified in the ENTRYPOINT.

Specifying an ENTRYPOINT in Dockerfile

    ENTRYPOINT ["/usr/sbin/nginx" ]
 
Using docker run with ENTRYPOINT

	$ sudo docker run -t -i myimage -g "daemon off;"

This argument will be passed to the command specified in the ENTRYPOINT instruction, which will thus become /usr/sbin/nginx -g "daemon off;". This command would then launch the Nginx daemon in the foreground and leave the container running as a web server.

<b>TIP </b>:- If required at runtime, you can override the ENTRYPOINT instruction using the docker run command with --entrypoint flag.

<hr>

#### 5)WORKDIR :-

The WORKDIR instruction provides a way to set the working directory for the container and the ENTRYPOINT and/or CMD to be executed when a container is launchedfrom the image.

Using the WORKDIR instruction

	WORKDIR /v1/app/db
	RUN bundle install
	WORKDIR /v1/webapp
	ENTRYPOINT [ "rackup" ]

Here we’ve changed into the /v1/app/db directory to run bundle install and then changed into the /v1/webapp  directory prior to specifying our ENTRYPOINT instruction of rackup.

Overridding the working directory

	$ sudo docker run -t -i -w /var/www   ubuntu

<hr>

#### 6)ENV

The ENV instruction is used to set environment variables during the image build process. For example:

Setting an environment variable in Dockerfile

	ENV RVM_PATH /home/docker/
	RUN gem install unicorn
		
	would be executed as: 
	
		 RVM_PATH=/home/docker/ gem install unicorn


 Setting multiple environment variables using ENV

	ENV RVM_PATH=/home/rvm  RVM_ARCHFLAGS="-arch i386"





Using an environment variable in other Dockerfile instructions
	
	ENV TARGET_DIR /v1/app
	WORKDIR $TARGET_DIR

<hr>

#### 7)USER 

The USER instruction specifies a user that the image should be run as.If a service can run without privileges, use USER to change to a non-root user. Start by creating the user and group in the Docker file with something like RUN groupadd -r postgres && useradd -r -g postgres postgres.

In dockerfile add
  
 1)  RUN groupadd -r postgres && useradd -r -g postgres postgres

* **-r = -r low..high...Sets the low and high bounds of UID ranges for  		new users. A new user can only be created if there are UIDs which 		  can be assigned from one of the free ranges.**
		  
* **-g = Sets the default group for new users**

 2) USER postgres
	

<b>TIP</b>:- The default user if you don’t specify the USER instruction is root.

<hr>

#### 8) VOLUME

The VOLUME instruction adds volumes to any container created from the image.

* **Volumes can be shared and reused between containers.**
* **A container doesn’t have to be running to share its volumes.**
* **Changes to a volume are made directly.**
* **Changes to a volume will not be included when you update an image.**
* **Volumes persist until no containers use them.**

This allows us to add data (like source code), a database, or other content into an image without committing it to the image and allows us to share that data between containers.


Using the VOLUME instruction
	
	VOLUME ["/opt/projectss"]
 	
Using multiple VOLUME instructions

	VOLUME ["/opt/projects", "/data" ]

<b>NOTE</b> : It is not possible to use the VOLUME instruction to tell docker what to mount. That would seriously break portability. This instruction tells docker that content in those directories does not go in images and can be accessed from other containers using the --volumes-from command line parameter. You have to run the container using <b>-v /path/on/host:/path/in/container </b>to access directories from the host.


<hr>

#### 9)ADD

The ADD instruction adds files and directories from our build environment into our image; for example, when installing an application. The ADD instruction specifies a source and a destination for the files

	# Usage: ADD [source directory or URL] [destination directory]
		ADD myfile.tar /application/myfile.tar
       

<b>Note</b>:You cannot ADD files from outside the build directory or context.

When ADD’ing files Docker uses the ending character of the destination to determine what the source is. If the destination ends in a /, then it considers the source a directory. If it doesn’t end in a /, it considers the source a file.

The source of the file can also be a URL

	ADD http://wikipedia.com/latest.zip /home/Downloads/wikipedia.zip

<b>Note</b>: ADD instruction can also unpack tar,zip  files.
	ADD wont create directory if not present


<hr>

#### 10)COPY

The COPY instruction is closely related to the ADD instruction. The key difference
is that the COPY instruction is purely focused on copying local files from the build context and does not have any extraction or decompression capabilities.

	COPY index.html/  /var/www/html/

<hr>

#### 11)ONBUILD

The ONBUILD instruction adds triggers to images.A trigger is executed when the image is used as the basis of another image

Eg:

	ONBUILD ADD index.html  /var/www
   	ONBUILD RUN cd  /var/www 
	
This would add an ONBUILD trigger to the image being created using this base image.


<hr>

#### 12)MAINTAINER

	MAINTAINER <name>

The MAINTAINER instruction allows you to set the  field of the
generated images.




<hr>

#### 13)EXPOSE

The EXPOSE command is used to associate a specified port to enable networking between the running process inside the container and the outside world (i.e. the host).
Example:

	#Usage: EXPOSE [port]
	EXPOSE 8080

<hr>
### Sample Docker file

	FROM ruby:2.2.0
	RUN apt-get update -qq && apt-get install -y build-essential
	RUN apt-get install -y libpq-dev
	RUN apt-get install -y libxml2-dev libxslt1-dev nodejs
	ENV APP_HOME /app/blog
	RUN mkdir -p $APP_HOME
	WORKDIR $APP_HOME
	ADD Gemfile* $APP_HOME/
	RUN bundle install
	ADD . $APP_HOME





<a href="{{site.baseurl}}docker/docker-hub.html"><<Dockerhub</a> 

