# DOCKER - using NGINX for deployment

$~$

<p align="center">
<img src="https://github.com/Bomays/holbertonschool-softy-pinko-docker/blob/d888abfc28c6ef6b691c467990f10462a0c633bb/logo/docker-logo-blue.png" alt="Docker Logo" width="700"/>
</p>

$~$

<p align="center">
<img src="https://github.com/Bomays/holbertonschool-softy-pinko-docker/blob/9523774adc62ddc772bf3a263a27cdfbc8a5dce1/logo/nginx.svg" alt="NGINX logo" width="500"/>
</p>

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
>
> - The first request will be sent to server A.
> - The second to server B.
> - The third to server C.
> - The fourth to A, and so on.
>
> This ensures that each server receives an equal share of the traffic and prevents any one server from being overwhelmed.
>
> For our learning purposes in this project, it is a sufficient algorithm to implement for our load-balancing needs.

## About NGINX in this Docker project

    1.Reverse Proxy

Nginx is commonly used as a reverse proxy. This means it receives requests from users and forwards them to other services or Docker containers (for example, an application server or a database server). In a Docker environment, Nginx can be configured to redirect requests to specific containers running your web application, which helps manage traffic flow.
$~$

    2.Load Balancer

Nginx can also act as a load balancer. When used with Docker, it can distribute incoming traffic across multiple instances of an application container (for example, multiple instances of a Node.js or Python application), allowing for better handling of traffic spikes and ensuring high availability of your site.
$~$

    3.SSL Management (HTTPS)

Nginx is often used to manage SSL (HTTPS certificates), enabling secure communication between the user and the server. When deploying a site with Docker, Nginx can be configured to handle SSL termination, meaning it decrypts the HTTPS requests and forwards them internally as HTTP to your application's Docker container.
$~$

    4.Static Content Delivery

Nginx is also very efficient at serving static content such as images, JavaScript files, CSS files, etc. In a Docker environment, Nginx can be configured to serve these files directly, reducing the load on application containers that no longer need to handle these requests.
