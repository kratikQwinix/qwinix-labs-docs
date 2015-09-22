---
layout: topics
title:  "Containers"
date:   2015-09-17 12:53:31
categories: docker part-1
---

##Containers

Containers are basically light weight VM. But unlike traditional virtualization, they do not require an emulation layer to be run on but can use the Operating system's normal system call interface which reduces overhead and allows a large number of containers to be run on a host.

Using docker containers can be built very fast.<br>
Containers can have their own process space, can have their own network interface, can run as root and also share the kernel with the host.
This means that Containers are Isolated processes and for isolation they rely on two major kernel features which are namespaces and controlgroups.

#### 1. Namespaces

  * **pid** <br>
   Each container has its own pid number and ps
  * **mnt**<br>
   Mount namespace
  * **net**	<br>
   The network namespace  	
   Each container has its own ip address assigned, own network interface and routing tables.
  * **uts**<br>
   Containers have their own uts namespace , each one has a different hostname.

	
#### 2. ControlGroups<br>
Incharge of accounting and limiting the system resources for containers.

  * **Memory**<br>
   Limits memory for each container.
  * **Cpu**<br>
   Prioritize containers,keep track of system CPU time
  * **blkIO**<br>
   Block IO to keep track of Ios for each block device (limit the amount of data that can be written by the container) 
  * **Devices**<br>
   Controls read/write/mknod permissions

{% highlight sh %}
$ docker run -it --name container ubuntu bin/bash 
{% endhighlight %}

Containers can be run using the following command
  

{% highlight sh %}
  $ docker run --name my_container -i -t ubuntu /bin/bash
{% endhighlight %}

where,<br>
	my_container  -> name of the container<br>
	ubuntu -> the image<br>
    /bin/bash -> the command to be executed

Few Command line flags that can be used with run command are:
  
  * **-i** for STDIN
  * **-d** to detach and run container in background
  * **-t** for pseudo-tty
  * **-u** to specify a user the image should be run as
  * **-e** to set environment variables during runtime
  * **-v** to mount volumes.

Containers can be listed using the 

{% highlight sh %}  
$ sudo docker ps
 {% endhighlight %}
command and -a can be used to list all containers and -q to return container IDs.

{% highlight sh %} 
 $ sudo docker ps -a
 {% endhighlight %}

Containers can be stopped using the command

{% highlight sh %}  
$ sudo docker stop container_id 
{% endhighlight %}
	
or

{% highlight sh %} 
 $ sudo docker kill container_id 
 {% endhighlight %}
  
 They can be started again using 
 
 {% highlight sh %} 
 $ sudo docker start container_id 
 {% endhighlight %}
 
 and can re-attach to the previous session using

 {% highlight sh %} 
 $ sudo docker attach container_id 
 {% endhighlight %}

Container details 
 
 {% highlight sh %} 
 $ sudo docker inspect container_id 
 {% endhighlight %}
 
 {% highlight sh %} 
 $ sudo docker stats container_name1,container_name2 
 {% endhighlight %}

Deleting a container
 
 {% highlight sh %} 
 $ sudo docker rm container_id 
 {% endhighlight %}


<a href="introduction-to-docker.html"><<Introduction</a> 
<a style = "float:right" href="images.html">Images>></a> 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
