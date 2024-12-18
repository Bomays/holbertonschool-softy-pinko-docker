# Dock

$~$

<p align="center">
<img src="https://github.com/Bomays/holbertonschool-softy-pinko-docker/blob/d888abfc28c6ef6b691c467990f10462a0c633bb/logo/docker-logo-blue.png" alt="Docker" width="700"/>
</p>

$~$

<p align="center">
  <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHZpZXdCb3g9IjAgMCAyNC41NzYgMTIuMjk2IiBwcmVzZXJ2ZUFzcGVjdFJhdGlvPSJ4TWluWU1pbiBtZWV0Ij48cGF0aCBkPSJNNi4wMSA4LjI0N2MtLjExNCAwLS4yMjUtLjA0NC0uMzEtLjEyOEwzLjExNCA1LjUzM1Y3LjhjMCAuMjQtLjE5Ni40MzctLjQzNy40MzdTMi4yNCA4LjA1MiAyLjI0IDcuOFY0LjQ4YzAtLjE3Ny4xMDctLjMzNi4yNy0uNDA0cy4zNS0uMDMuNDc2LjA5NWwyLjU4NiAyLjU4NlY0LjQ4YzAtLjI0LjE5Ni0uNDM3LjQzNy0uNDM3cy40MzcuMTk2LjQzNy40MzdWNy44YzAgLjI0LS4xOTYuNDM3LS40MzcuNDM3bTIuMDIzLTQuMmwtLjEyLjIyNC0uOTMgMS42ODgtLjEyLjIxMy4xMi4yMTMuOTMgMS42MzMuMTI1LjIyNGgyLjQzbC4xMi0uMjQ2LjY5NC0xLjM5OC4zMS0uNjM0aC0uNzA0bC0xLjc3NS4wMDVjLS4yMy0uMDAzLS40NDMuMjA2LS40NDMuNDM3cy4yMTIuNDQuNDQzLjQzN2wxLjA3LS4wMDUtLjI2Mi41M0g4LjU0NmwtLjY4My0xLjIwMi42ODgtMS4yNDVoMS40NjRsLjM0LjdoLjg4bC0uNTU0LTEuMzI4LS4xMi0uMjQ2aC0yLjUzbTQuNDI2LS4wMDVjLS4yMy4wMDMtLjQzNC4yMTQtLjQzLjQ0MnYxLjE0aC44NzR2LTEuMTRjLjAwMy0uMjMyLS4yLS40NDUtLjQ0Mi0uNDQybTEuNCA0LjIxNWMtLjI0IDAtLjQzNy0uMTk2LS40MzctLjQzN1Y0LjQ4N2MwLS4yNC4xOTYtLjQzNy40MzctLjQzN3MuNDM3LjE5Ni40MzcuNDM3djIuMjc3bDIuNTg2LTIuNTg2Yy4xMjUtLjEyNS4zMTMtLjE2Mi40NzYtLjA5NXMuMjcuMjI3LjI3LjQwNFY3LjgyYzAgLjI0LS4xOTYuNDM3LS40MzcuNDM3cy0uNDM3LS4xOTYtLjQzNy0uNDM3VjUuNTQybC0yLjU4NiAyLjU4NmMtLjA4Mi4wODItLjE5My4xMjgtLjMxLj12ODEuMzcsMzYsMzgsMzgsNjUsOCw5...==" alt="Docker Logo" width="500"/>
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
