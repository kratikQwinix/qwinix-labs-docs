---
layout: post
title:  "Using Apache"
date:   2015-09-17 12:53:32
categories: docker part-4
topic: docker
---

### Writing a Dockerfile

	FROM linuxconfig/apache
	EXPOSE 80
	RUN mkdir -p /var/www/html
	ADD . /var/www/html
	CMD ["apache2ctl" ,"-D", "FOREGROUND"]


<hr>

### Building an image using Dockerfile

	docker build -t kratiknayak/apache .

<hr>

### Running the image in a conatiner

	docker run -d -p 80 -v $PWD/html:/var/www/html kratiknayak/apache