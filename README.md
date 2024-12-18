# Dock

$~$

<p align="center">
<img src="https://github.com/Bomays/holbertonschool-softy-pinko-docker/blob/d888abfc28c6ef6b691c467990f10462a0c633bb/logo/docker-logo-blue.png" alt="Docker" width="700"/>
</p>

$~$

<p align="center">
<svg xmlns="http://www.w3.org/2000/svg" width="120" height="60" viewBox="0 0 24.576 12.296" preserveAspectRatio="xMinYMin meet"><path d="M6.01 8.247c-.114 0-.225-.044-.31-.128L3.114 5.533V7.8c0 .24-.196.437-.437.437S2.24 8.052 2.24 7.8V4.48c0-.177.107-.336.27-.404s.35-.03.476.095l2.586 2.586V4.48c0-.24.196-.437.437-.437s.437.196.437.437V7.8c0 .24-.196.437-.437.437m2.023-4.2l-.12.224-.93 1.688-.12.213.12.213.93 1.633.125.224h2.43l.12-.246.694-1.398.31-.634h-.704l-1.775.005c-.23-.003-.443.206-.443.437s.212.44.443.437l1.07-.005-.262.53H8.546l-.683-1.202.688-1.245h1.464l.34.7h.88l-.554-1.328-.12-.246h-2.53m4.426-.005c-.23.003-.434.214-.43.442v1.14h.874v-1.14c.003-.232-.2-.445-.442-.442m1.4 4.215c-.24 0-.437-.196-.437-.437V4.487c0-.24.196-.437.437-.437s.437.196.437.437v2.277l2.586-2.586c.125-.125.313-.162.476-.095s.27.227.27.404V7.82c0 .24-.196.437-.437.437s-.437-.196-.437-.437V5.542l-2.586 2.586c-.082.082-.193.128-.31.128m7.005-2.106l1.36-1.354c.17-.17.17-.447.001-.618s-.447-.17-.618-.001l-1.36 1.357-1.36-1.357c-.17-.17-.448-.17-.618.001s-.17.448.001.618l1.36 1.354L18.27 7.5c-.17.17-.17.447-.001.618.082.083.193.13.3.13s.223-.042.308-.128l1.357-1.353 1.357 1.353c.082.082.193.128.308.128s.224-.043.3-.13c.17-.17.17-.447-.001-.618l-1.355-1.35m-8.406 2.094c-.23-.003-.434-.214-.43-.442v-1.83h.874V7.8c.003.232-.2.445-.442.442" fill="#090"/></svg>
</p>


$~$


## Context


Docker is a platform that allows you to containerize your applications,
meaning that you can package them into portable, self-contained environments
which can run anywhere.
This means that you can quickly move your application from one environment to another,
such as from your local computer to a server, without worrying about dependencies or configuration issues.
Docker achieves this by using containers, which are isolated environments that contain
everything an application needs to run, such as libraries, dependencies,
and configurations. Docker containers are lightweight and can be started and stopped quickly,
making them ideal for modern software development and deployment.
With Docker, you can also quickly scale your application by running multiple containers
of the same application on different hosts (or the same host, as we will do in this project),
and manage them using Docker Compose or other orchestration tools.

Ultimately, what you will create in this project is an infrastructure for an application
that utilizes a reverse proxy, a load balancer, two application servers, and one front-end server.

Let’s consider the following design:



$~$

## High-level Design


In this design, there is a single server that acts as the entry point for your application.
That server acts as a reverse proxy server, which routes traffic to either the API servers
or the front-end static-content server ; it also acts as a load balancer to balance traffic between the two API servers. 
When traffic comes in, the server will determine which service it needs to go to
(either the front-end static-content server or the API server) and:
$~$

```
- If the request is to be routed to the front-end static-content server,
it will do so and any static content that is returned from the front-end static-content server
to the proxy server will then be sent to the client. The client isn’t directly communicating
with the front-end static-content server.

- If the request is to be routed to the API server, then it will first go through
a load-balancing algorithm to determine which API server to send the request to.
We will be using the basic Round Robin load-balancing algorithm for our site.
Once the request is routed to an API server and the response is sent back to the proxy server,
it will then be sent to the client.
The client isn’t directly communicating with either of the API servers.

```

$~$

$~$

> 🟦 **INFO**
> 
> **What is Round Robin load balancing?**
> 
> Round Robin load balancing is a method of distributing traffic across multiple servers or nodes in a network. 
> In this approach, the load balancer assigns requests to each server in a rotating manner, meaning that each server takes turns serving the requests.
> 
> **Example:**
> - The first request will be sent to server A.
> - The second to server B.
> - The third to server C.
> - The fourth to A, and so on.
> 
> This ensures that each server receives an equal share of the traffic and prevents any one server from being overwhelmed.  
> 
> For our learning purposes in this project, it is a sufficient algorithm to implement for our load-balancing needs.
