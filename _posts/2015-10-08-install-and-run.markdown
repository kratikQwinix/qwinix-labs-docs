---
layout: post
title:  "Installing Jenkins"
date:   2015-10-07 12:30:00
categories: jenkins
topic: jenkins
permalink: jenkins/2015/10/08/plugins.markdown
---

## Install and Run

<hr>

#### Installation


	wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key |sudo apt-key add -
	sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'sudo apt-get update
	sudo apt-get install jenkins



#### To run  jenkins

	cd /usr/share/jenkins
	$java -jar jenkins.war

##### To change port
	$java -jar jenkins.war --httpPort=$HTTP_PORT


<a style="float:right" href="/:jenkins/:2015/:10/:08/:plugins.markdown"> Plugins </a>

