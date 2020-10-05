---
title: "Devops:3 DNS Lookup"
date: "2020-10-06"
template: "post"
draft: false
slug: "dns-lookup"
category: "Devops"
tags:
  - "Internet"
  - "Dev Ops"
description: "How does DNS lookup work"
socialImage: "/media/servers.jpeg"
---

## What is DNS?
The Domain Name System (DNS) is the phonebook of the Internet. We access information online through domain names like google.com, even though we need IP Addresses to access anything across the internet.

Each device connected to the Internet has a unique IP address which other machines use to find the device. DNS servers eliminate the need for humans to memorize IP addresses such as 192.168.1.1.

## DNS resolution
The process of DNS resolution involves converting a hostname (such as www.example.com) into a computer-friendly IP address (such as 192.168.1.1).
In order to understand DNS resolution we must understand the different components that are involved in the process.
There are 4 DNS servers involved in loading a webpage:
- DNS recursor 
- Root nameserver
- TLD nameserver
- Authoritative nameserver

### DNS recursor(recursive resolver)
A DNS resolver, also called a recursive resolver, is a server designed to receive DNS queries from web browsers and other applications. The resolver receives a hostname - for example, www.example.com - and is responsible for tracking down the IP address for that hostname.

The DNS resolver might be operated by the local network, an Internet Service Provider (ISP). The resolver starts by looking in its local cache or that of the operating system on the local device - if the hostname is found, it is resolved immediately.

If not, the resolver contacts a DNS Root Server and receives details of a TLD Name Server. Via the TLD Name Server, it receives details of an Authoritative Name Server, and asks it for the IP that matches the requested hostname. When it receives the IP, the query is resolved.

### DNS root server(Root nameserver)
The root server is the first step in translating human readable host names into IP addresses. The Top Level Domain (TLD) takes the TLD provided in the user’s query - for example, www.example.com - and provides details for the .com TLD Name Server.

There are 13 logical root servers worldwide, indicated by the letters A through M, operated by different organizations, which you can look into [here](https://www.iana.org/domains/root/servers)

### TLD nameserver
The TLD Name Server takes the domain name provided in the query - for example www.example.com - and provides the IP of an Authoritative Name Server. This is a DNS server that contains DNS records for the specific domain.

There is a Name Server for each Top Level Domain (TLD) - there are currently over 1500 valid top level domains, including the original TLDs like .com and .org, country codes such as co.uk and co.in etc.

### Authoritative nameserver
The Authoritative Name Server takes the domain name and subdomain, and if it has access to the DNS records, it returns the correct IP address to the DNS Resolver.
In some cases, the Authoritative Name Server will route the DNS Resolver to another Name Server that contains specific records for a subdomain, for example, blog.example.com.

## DNS resolution steps

So in short the whole process of DNS resolution takes place in the following steps
1. A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver.
2. The resolver then queries a DNS root nameserver (.).
3. The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD.
4. The resolver then makes a request to the .com TLD.
5. The TLD server then responds with the IP address of the domain’s nameserver, example.com.
6. Lastly, the recursive resolver sends a query to the domain’s nameserver.
7. The IP address for example.com is then returned to the resolver from the nameserver.
8. The DNS resolver then responds to the web browser with the IP address of the domain requested initially.
9. The browser makes a HTTP request to the IP address.
10. The server at that IP returns the webpage to be rendered in the browser

## Further Reading 

There is still a lot going in the background here, there is caching at different levels of this request from browser, to OS level caching to resolver DNS caching to make the lookup faster. 

If you find this interesting [there is this great github page](https://github.com/alex/what-happens-when#the-g-key-is-pressed) which shows how everything from when you press a button on the keyboard to loading the last bits of content on your screen works.
