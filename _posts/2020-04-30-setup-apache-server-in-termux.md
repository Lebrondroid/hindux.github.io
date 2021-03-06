---
layout: post
comments: false
title: "How to setup apache server in termux."
toc: true
image: https://cdn.jsdelivr.net/gh/hindux/hindux.github.io/assets/images/apache.jpg
description: "Steps to setup apache webserver in termux environment for hosting as well other purposes"
author: kcubeterm
category: termux
tags: [apache,server]
rating: 4.5
---

#### What is apache server ?
> The Apache HTTP Server, colloquially called Apache, is a free and open-source cross-platform web server software, released under the terms of Apache License 2.0. Apache is developed and maintained by an open community of developers under the auspices of the Apache Software Foundation

it is web server.The job of a web server is to serve websites on the internet. To achieve that goal, it acts as a middleman between the server and client machines. It pulls content from the server on each user request and delivers it to the web.

#### Requirement.
Here i am going to setup apache2, it's second version of apache or you can say enhanched version.


##### Install apache
Before any installion make sure you have updated your terminal packages.
````
pkg upgrade
pkg install apache2

```
##### setup config
if you are using termux then you can find config file in **/data/data/com.termux/files/usr/etc/apache2/**
the name of config file will be httpd.conf
```
cd /data/data/com.termux/files/usr/etc/apache2
ls
```
after execution of above command you should get httpd.conf


Config is the important part of settings anythings, here open the __httpd.conf__ (config) file with your favourite editor.
###### Step 1:configure listen
after opening httpd.conf  , find **Listen 8080** and replace it with **Listen 0.0.0.0:8080** here ip 0.0.0.0 means apache server listen all available ip ,you can list your ip or interface with `ifconfig`.
if you face problem in finding, use grep to find pattern.like this `grep -n 'Listen ' httpd.conf`

```
grep -n 'Listen ' httpd.conf
48:# Change this to Listen on specific IP addresses as shown below to
51:#Listen 12.34.56.78:80
52:Listen 8080
```
you can see in my case listen found in line 52.



###### step 2:set ServerName
i hope you did step 1 without any error. now set servername, you can choose any name for your server for now.
like suppose i choose termux then write `ServerName termux` in last line or any blank line
when you got error like following, it means you have to set ServerName
```
$apachectl
AH00558: httpd: Could not reliably determine the server's fully qualified domain name, 
using 127.0.0.1. Set the 'ServerName' directive globally to suppress this message

```
after setup servername run `apachectl ` and go to [http://localhost:8080](http://localhost:8080)
if all things have done nice then your browser should show like following
![ alt it's work ](/https://cdn.jsdelivr.net/gh/hindux/hindux.github.io/assets/images/itswork.jpg)

all the setup have done now ,you would thinking ,how can i change above content into my own content,so dont worry, follow one more steps.

#### Putting content for serving
so now go to **/data/data/com.termux/files/usr/share/apache2/default-site/htdocs** here you find index.html
if you know html then change it. and restart your apache server

```
apachectl stop
apachectl 
```

#### Access server from remote
your server is listen on 0.0.0.0 ,it means all available ip, check available ip by `ifconfig`
if you connect with hotspot and wifi then your server can be access from other device if that device connected on same hotspot or router


for accessing your server from remote is that port forwarding, you can either forward port through router or ftom service like ngrok or serveo.

##### Ngrok port forwarding

you can download ngrok executable by official site , for downloading ngrok in android 
```
cd ~/
wget --no-check-certificate https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.zip
unzip ngrok-stable-linux-arm.zip
```
now execute `./ngrok http 8080`
it prompt and connecting to his server and making tunnel, and it provide you ,link like https://ishsksbsks.ngrok.io but not this one


now copy that link which ngrok gave you , from that link you can access your server from anywhere in world.
ngrok has limitation for free account.

i use this for demo only, you can other service or port forwarding from router and use [freedns](https://freedns.afraid.org/) as dynamic dns server for updating your ips,
[integrate php with apache]({{ site.baseurl}}/setup-php-with-apache-in-termux/)
**i hope you enjoyed this tutorial***

**Enlighten others by sharing it***







