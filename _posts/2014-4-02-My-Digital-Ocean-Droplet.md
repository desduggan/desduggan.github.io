---

layout: post
title: My Digital Ocean Droplet
excerpt: Going from nothing to a Django capable server. 
link: http://drduggan.github.io/Cloud_Server_Setup
linkname: How To

---

# {{page.title}}

Having a server to use as a sandbox for my side projects has been on my todo list for a while, but school work kept it a low priority until this weekend when I had some time to get one up and running. 

Specifically, I wanted one that was capable of serving Django applications because it's my modern framework of choice. Surprisingly though, I couldn't find a solid end to end guide to follow, so I pieced together a few different sources and figured some stuff out on my own. 

Below is a link to a step by step guide I wrote for anyone trying to do the same thing. I tested as much as I could during development, but I haven't gone through it with a new machine (feedback is appreciated!). 


	apt-get update
	apt-get upgrade

	sudo apt-get install apache2

	sudo apt-get install mysql-server
	sudo apt-get install libmysqlclient-dev
	apt-get install python-dev
	sudo apt-get install libapache2-mod-wsgi

	apt-get install python-pip
	pip install virtualenv
	pip install virtualenvwrapper

	pip install mysql-python
