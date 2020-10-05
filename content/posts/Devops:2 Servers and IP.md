---
title: "Devops:2 Servers and IP addresses"
date: "2020-09-29"
template: "post"
draft: false
slug: "servers-and-ip"
category: "Devops"
tags:
  - "Internet"
  - "Dev Ops"
description: "Servers, IP Addresses and Ports"
socialImage: "/media/servers.jpeg"
---

![nslookup](/media/servers.jpeg)

## Server

A server in simplest terms is just a computer available over the internet. It might have a better connectivity, power backup etc. but it is just a simple machine at a physical location.

There are many types of servers like

- Webservers
- Email servers
- DNS servers
- Application servers
- FTP servers

We will discuss some of these in future posts.

## IP Addresses

IP Addresses are are used to identify which device are we talking to when making a request. There are 2 types of ip addresses:

- Public ip address
- Private ip address

**Private ip address** has no value outside of the current network it is in. If we have different devices connected to the wifi at out home in our network they might have different private ip address like 192.0.1.1, 192.0.1.2 etc. Within the network we can access the other device using these private ips.

**Public ip address** is used to access something over the internet. To access google.com from anywhere in the world it needs to have a public ip address. Let's go ahead and see the ip of google.com using _nslookup_ command in our terminal.

![nslookup](/media/nslookup.png)

As we can see it gives us the ip 172.217.26.196, if we go ahead and enter this in our browser it will redirect us to www.google.com.

## Port Numbers

A port number is required to access defferent applications running on a server. If there is a server available on the internet there might be multiple services we might want to connect to on that server. This is acheived via port numbers. If this server has the ip let's say 192.89.0.43, we can assign our applications to listen on different ports example 8083 and 8084. Now if we hit 192.89.0.43:8083 the application listening on 8083 will get the request.
There are 0 - 65535 available ports. Some of these have assigned protocols for example:

- 80: HTTP
- 443: HTTPS
- 22: SSH

Now, let's say there is a server with an ip 172.217.26.196 which hosts multiple applications like nginx, redis, mysql etc. Now if this server wants to expose all these services to the outside world it can do it by running these on different ports. For example using the default ports for these services:
- 172.217.26.196:80 will connect you to nginx.
- 172.217.26.196:3306 will connect you to mysql 
- 172.217.26.196:6379 will connect you to redis

That's it for this post. In the next part of this series we will look at how DNS lookup works.
