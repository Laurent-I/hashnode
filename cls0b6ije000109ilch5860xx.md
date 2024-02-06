---
title: "Learn Docker Fundamentals Easily 👌"
seoTitle: "Understanding Docker Basics"
seoDescription: "Master Docker: Enhance app efficiency, remove dependency issues, and grasp containerization, images, and registries"
datePublished: Tue Jan 30 2024 12:02:11 GMT+0000 (Coordinated Universal Time)
cuid: cls0b6ije000109ilch5860xx
slug: learn-docker-fundamentals-easily
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HSACbYjZsqQ/upload/5f1f4a536d2e2379727696b592031928.jpeg
tags: software-development, docker, development, beginner, devops

---

# What is Docker? 🐳

> In easy to understand terms, we can define Docker as:  
> A virtual software that uses lightweight containers so that applications can work efficiently in different environments in isolation

So, the idea behind Docker is containerization, which, in short, eliminates the awful and stressful process of installing dependencies across platforms 🚀.

Imagine trying to build a simple blog website, and you know you need dependencies like Nest.js, Express, and others. You will have to install those dependencies, and in turn, you might find that they depend on other packages, and in turn, those packages have others 😅. This could go on and on, and you might reach a point where installing a certain package or dependency is not so friendly on your current OS. Trust me when I say that it's a headache when you come across something like that.

Well, Docker helps to eliminate this hideous process 💪🏽.

## How Does Docker Work? ⚙️

You might wonder how Docker works, and if you have a simple grasp by now, you might be wondering: Wait, Docker is just another virtual machine?

Technically, you are not wrong, but it works differently from traditional virtual machines.

The traditional virtual machines use a hypervisor to communicate between the host OS and the virtual OS, causing a lot of overhead, hence making them work slowly and be so demanding.  
*Note: This is a very simple overview of how virtual machines work but you get the gist of it 😉*

![Virtual machine working. | Download Scientific Diagram](https://www.researchgate.net/publication/317294656/figure/fig1/AS:503522979921920@1497060641641/Virtual-machine-working.png align="center")

Docker has an infrastructure almost similar to that of virtual machines because, after all, it is virtual software, but it works in a different way that helps increase performance and reduce the resources needed.

Docker uses containers instead of virtual machines. Containers do a neat job of virtualization. Instead of having a guest OS, containers use the host OS via its runtime while maintaining complete isolation, just like a traditional virtual machine. 😎

And Docker acts like the hypervisor, but for containers.

![What is a Container? | Docker](https://www.docker.com/wp-content/uploads/2021/11/container-what-is-container.png align="center")

## Running Our First Command using Docker 🏃🏽‍♂️

If you have ever messed around with programming, we know that `hello world` is kind of the de facto or go-to first program to run. Luckily, it is the same in the docker world and we are going to run our favorite command here first also. 😂

A few things before we run our favorite command (at least mine), we need to have a few things:

1. A laptop with internet connection
    
2. Docker is installed on your machine.
    

If you don't have Docker installed, you can just follow the guide in the official documentation. It is pretty straight-forward to do for all OSes. Whether you have Mac, Windows, or Linux OS, Docker supports all operating systems 💻.

Here is the link to the installation guide: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

With that out of the way we can now run our favorite command.  
Open your terminal and run the following command:

```bash
docker run hello-world
```

If this is the first time you run this command, you should see an output like this:

```bash
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
c1ec31eb5944: Pull complete
Digest: sha256:4bd78111b6914a99dbc560e6a20eab57ff6655aea4a80c50b0c5491968cbc2e6
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

The [hello-world](https://hub.docker.com/_/hello-world) image is an example of minimal containerization with Docker. It has a single program compiled from a [hello.c](https://github.com/docker-library/hello-world/blob/master/hello.c) file responsible for printing out the message you're seeing on your terminal.

Now we can check all running and stopped containers with just this command:

```bash
docker ps -a
```

And get an output like this:

```bash
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS                      PORTS     NAMES
bddf58c8c589   hello-world     "/hello"                 14 minutes ago   Exited (0) 5 minutes ago              flamboyant_chatelet
623c28650ac9   postgres:13.4   "docker-entrypoint.s…"   13 days ago      Exited (0) 41 minutes ago             median-postgres-1
```

As you can see, I have two containers that have run so far. The first one is the one we just ran, which is, `hello-world` and the second is for `postgres` . We can see the container ID, the image name, command run, date created, status, ports, and some random generated names.  
*If you feel lost, just don't sweat it. I will explain all those terms in just a minute.*

We have run so far two commands, which are:

1. `docker run hello-world`
    
    * `docker run`: This is the command to run a Docker container.
        
    * `hello-world`: This is the name of the Docker image you want to run.
        
    
    Explanation: When you execute this command, Docker will try to find the "hello-world" image on your system. If it's not already present locally, Docker will automatically download it from the Docker Hub (a repository for Docker images). The "hello-world" image is a simple, lightweight image often used for testing and demonstration purposes.
    

`docker ps -a`:

* `docker ps`: This command lists the currently running Docker containers.
    
* `-a`: This flag shows all containers, including those that are not currently running.
    

Explanation: When you execute `docker ps -a`, Docker will display a list of all containers on your system, whether they are running or stopped. It provides information such as container ID, image used, status, and other details. This command is useful for checking the history of containers, including those that have completed their tasks or encountered issues.

Now for what the columns mean:

1. **Container ID:**
    
    * This is a unique identifier assigned to each Docker container. It's a hexadecimal string that you can use to reference or interact with the container.
        
2. **Image Name:**
    
    * Indicates the name of the Docker image from which the container was created. The image contains the necessary file system and settings for the container to run.
        
3. **Command Run:**
    
    * It shows the specific command that was executed to start the container. It represents the initial process or command that the container is running.
        
4. **Date Created:**
    
    * Displays the timestamp indicating when the container was created. This helps you track when the container was initiated.
        
5. **Status:**
    
    * Indicates the current state of the container. Common states include:
        
        * `Up`: The container is currently running.
            
        * `Exited`: The container has completed its execution or has been manually stopped.
            
        * `Paused`: The container is temporarily paused.
            
        * `Restarting`: The container is in the process of being restarted.
            
6. **Ports:**
    
    * Shows the port mappings between the host and the container. It displays the ports on the host machine that are forwarded to the corresponding ports within the container.
        
7. **Randomly Generated Names:**
    
    * Containers are often given random names if a specific name is not provided during container creation. These names are generated to ensure uniqueness.
        

## Key Terms Used in Docker or Containerization 🔑

In order to understand the Docker architecture, you have to first understand the three basic concepts used in containerization in general.

1. **Container:**
    
    * **What it is:** A container is like a *lightweight, standalone executable* package that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools.
        
    * **Analogy:** Think of a container as a self-contained box that holds all the ingredients and instructions needed to make a specific dish. It ensures that the dish (your application) tastes the same regardless of where it's cooked.
        
2. **Image:**
    
    * **What it is:** An image is a snapshot or template that serves as the blueprint for creating containers. It includes the application code, runtime, libraries, and other settings required for the software to run.
        
    * **Analogy:** Consider an image as a recipe card. It outlines the ingredients and steps to create a dish. Images are used to create containers, just as a recipe card is used to cook a meal.
        
3. **Registry:**
    
    * **What it is:** A registry is like a central storage location where Docker images are stored and can be shared. It's a repository for sharing and distributing container images. An example is [**Docker Hub**](https://hub.docker.com/) and [**Quay**](https://quay.io/)
        
    * **Analogy:** This is like a cookbook library where various recipe cards (images) are stored. This library allows chefs (developers) to access, share, and contribute new recipes. Docker Hub is a popular public registry, but you can also have private registries within organizations.
        
    
    ## **Putting it all together** 🔗:
    
    * **Creating a Container 📦:**
        
        * You start with an image, which is like a recipe.
            
        * You use that image to create a container, like cooking a dish using a recipe.
            
        * The container is an instance of the image and runs as an isolated and portable environment.
            
    * **Sharing and Storing Images 🏬:**
        
        * Images can be shared and stored in registries.
            
        * Registries are like libraries where images (recipe cards) are kept for others to access.
            
    * **Deployment 🛫:**
        
        * Containers (dishes) created from images can be deployed consistently across different environments.
            
        * This consistency ensures that the application behaves the same way regardless of where it's running.
            

## The Docker Architecture 🏗️

1. **Docker Daemon:**
    

* **What it is:** The Docker Daemon is a background process that manages Docker containers on a system. It's responsible for building, running, and monitoring containers.
    
* **Analogy:** Think of the Docker Daemon as the 🍳 chef in a kitchen. It takes care of preparing and managing the dishes (containers) based on the recipes (images).
    

1. **Docker Client:**
    

* **What it is:** The Docker Client is a command-line interface or a graphical tool that allows users to interact with the Docker Daemon. It sends commands to the daemon to build, run, or manage containers.
    
* **Analogy:** The Docker Client is like the 🤵 waiter taking orders from customers (users) and communicating them to the chef (Daemon) in the kitchen.
    

1. **REST API:**
    

* **What it is:** Docker exposes a REST API that provides a set of endpoints for communication between the Docker Client and the Docker Daemon. The API allows for remote interaction with Docker services.
    
* **Analogy:** Consider the REST API as a 📖 menu in a restaurant. The waiter (Docker Client) communicates with the kitchen (Daemon) by referring to the menu (API) to place orders.
    

Note: *I am keeping using the kitchen/food analogies to simplify the explanation (also because I am hungry 😅)*

Here is the diagram depicting the architecture:

[![Architecture of Docker - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/20221205115118/Architecture-of-Docker.png align="center")](https://www.geeksforgeeks.org/architecture-of-docker/)

We can explain the docker run hello-world examples in terms of the docker architecture:

1. The user (you) executes the `docker run hello-world` command using the Docker Client (command-line interface).
    
2. The Docker Daemon receives the command and interprets it. It checks if the "hello-world" image is available locally (default behavior); if not, it downloads it from Docker Hub.
    
    The Daemon creates a new container from the "hello-world" image, runs it, and executes the specified command (in this case, printing a hello message).
    
3. The Docker Client communicates with the Docker Daemon through the REST API, sending instructions to run the "hello-world" container.
    

# Conclusion

> This 📝 article provides an in-depth understanding of Docker, a virtual software that uses lightweight containers for efficient application performance in different environments. The article explains the concept of containerization, which eliminates the process of installing dependencies across platforms. It also elaborates on how Docker works differently from traditional virtual machines by using containers instead. The article then guides you through running your first Docker command and understanding the output. Key terms used in Docker or containerization such as 📦 container, 🖼️ image, and 🗄️ registry are explained with analogies. The article concludes with a detailed explanation of the Docker architecture, including the Docker Daemon, Docker Client, and REST API. 🚀

Feel free to leave suggestions in the comments, and I will get back to you.

Happy Learning and Studying!! ✌️