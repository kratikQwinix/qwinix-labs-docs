---
layout: topics
title:  "Containers"
date:   2015-09-17 12:53:31
categories: docker part-1
---

#Containers

Containers are basically light weight VM. But unlike traditional virtualization, they do not require an emulation layer to be run on but can use the Operating system's normal system call interface which reduces overhead and allows a large number of containers to be run on a host.

Using docker containers can be built very fast.

1.Containers 
  * have their own process space.
  * have their own network interface.
  * can run as root.
  * share the kernel with the host.

This means that Containers are Isolated processes and for isolation they rely on two major kernel features which are namespaces and controlgroups.


<a href="introduction-to-docker.html"><<Introduction</a> 
<a style = "float:right" href="images.html">Images>></a> 

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
