---
title: "Container Manipulation: The Basics 📌"
seoTitle: "Container Basics: Essential Manipulation Guide 📌"
seoDescription: "Master Docker commands for container management! Efficiently run, list, name, stop, restart, create, and remove. Enhance your Docker skills!"
datePublished: Wed Jan 31 2024 05:34:21 GMT+0000 (Coordinated Universal Time)
cuid: cls1crlzy00000ajr9lln0b28
slug: container-manipulation-the-basics
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/tjX_sniNzgQ/upload/07bc8c1ed9e3f7489493f40324d525a8.jpeg
tags: docker, devops, beginners, containers

---

Get ready to master the art of manipulating containers!

After understanding the building blocks of Docker, we have to understand container manipulation in detail. This is crucial since we are going to be manipulating containers very often.

The full list of the container commands can be found in the official documentation here: [Container All Commands](https://docs.docker.com/engine/reference/commandline/container/). The ones we are going to discuss are the most important ones, or the ones I think are most useful.

## Running Containers ⚡

There are many options for running containers using Docker. There are many options to pass and arguments to add, which is why we are going to look at a few but important ones.

First, the syntax is:  
`docker run <image name>`

But there is a better and more descriptive way of running Docker containers ✨:  
`docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`

* `docker container run`**:** This is the basic syntax of the command. It informs Docker that you want to run a container, pulling the image if needed, and starting the container.
    
* `[OPTIONS]`**:** These are additional settings and configurations you can provide to customize the behavior of the container. Options can include specifying ports, volumes, environment variables, etc.
    
* `IMAGE`**:** This is the name or ID of the Docker image from which the container will be created. An image is a snapshot or template that includes the application code, runtime, libraries, and other settings required for the software to run.
    
* `[COMMAND] [ARG...]`**:** This optional part allows you to override the default command specified in the Docker image. It lets you define a specific command that should be executed when the container starts, along with any arguments that command may need.
    

The image could be from the online registry or local system. For the sake of practice, we are going to use the nginx image. This image contains contains the necessary files and configurations to run the Nginx web server in a Docker container

`docker container run -p 8080:80 -d --name my_web_app nginx`

The command is self-explanatory, except for a few things that are going to be explained in the coming sub-sections🧩. This command runs a nginx image on port 8080 in detachment mode with the name of my\_web\_app (don't worry, we shall explain everything in the coming section 😜). The output will look like this if it is the first time running it:

```bash
docker container run -p 8080:80 -d --name my_web_app nginx

Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
2f44b7a888fa: Pull complete
8b7dd3ed1dc3: Pull complete
35497dd96569: Pull complete
36664b6ce66b: Pull complete
2d455521f76c: Pull complete
dc9c4fdb83d6: Pull complete
8056d2bcf3b6: Pull complete
Digest: sha256:4c0fdaa8b6341bfdeca5f18f7837462c80cff90527ee35ef185571e1c327beac
Status: Downloaded newer image for nginx:latest
d45f6667ef3f4d1efdbf3a11cd4c91228216e3e8de6b3f5d5f5841459f7511e7
docker: Error response from daemon: Ports are not available: exposing port TCP 0.0.0.0:8080 -> 0.0.0.0:0: listen tcp 0.0.0.0:8080: bind: An attempt was made to access a socket in a way forbidden by its access permissions.
```

### Publishing Ports 📢

Since we are in an isolated environment, we don't have a clue as to what is going on in the container. In order to access it, we have to map or publish the port on which the container is running the program to that of the host environment.

We use the `--publish <host port>:<container port>` or it alias, `-p <host port>:<container port>`

Now to access the web server on your browser, visit [http://localhost:4444/](http://localhost:4444/) address.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706639459923/4016baa7-ceca-49e9-a54c-51b52a3822f9.png align="center")

### Detached Mode 🔓

To prevent the container from stopping along with the terminal instance by simply hitting `ctrl + c` , we can use the detached mode to run it in the background by using `--detach` or it's alias `-d`.

In the previous example, we used `-d` to keep the container running in the background, but unfortunately, I faced an issue with the port mapping as the `8080` port was already in use.

I had to map it to another port `4444` to make it run.

The order of options doesn't matter; whether you put `--publish` or `--detach` before in any order, Docker won't mind, but when using the `run` command, the name of the image should be last because anything after it is passed as an argument to the container entry point. This will be covered later.

## Listing Containers 📋

When you list containers in Docker, you're essentially asking Docker to show you the containers that are currently on your system. The command for this is usually`docker ps`.

**Note** 🚨: `docker ps` is an alias for d`ocker container ls` and can be used interchangeably

**Command to list containers:**

```bash
docker ps
```

**Options that are commonly used:**

* `-a` or `--all`: Lists all containers, including those that are stopped or exited.
    
* **List running containers** 🚀\*\*:\*\*
    
    * When you run `docker ps` without any options, it shows you a list of containers that are currently running. These are the containers that are actively doing something, like running a web server or a database.
        
* **List All Containers (Including Stopped Ones)** ♾️\*\*:\*\*
    
    * If you add the `-a` option (`docker ps -a`), it will show you all containers, whether they are currently running or stopped. This is useful to see the history of containers, including those that have completed their tasks.
        

```bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS                        PORTS                  NAMES
ab80c5531a80   nginx                    "/docker-entrypoint.…"   40 minutes ago   Up 40 minutes                 0.0.0.0:4444->80/tcp   my_web_app
e1bfb8300155   kalilinux/kali-rolling   "bash"                   2 hours ago      Exited (100) 56 minutes ago                          practical_mestorf
877bc670b9c5   ubuntu                   "/bin/bash"              2 hours ago      Exited (0) 2 hours ago                               magical_chatterjee
84d902798359   busybox                  "sh"                     5 hours ago      Exited (130) 4 hours ago                             boring_lumiere
```

In this example,

* `CONTAINER ID`: A unique identifier for each container. The first 12 characters are the ones shown. The ID has 64 characters.
    
* `IMAGE`: The Docker image used to create the container.
    
* `COMMAND`: The command that the container is running.
    
* `CREATED`: The time when the container was created.
    
* `STATUS`: Indicates whether the container is currently running or has exited.
    
* `PORTS`: Shows the port mappings between the host and the container.
    
* `NAMES`: The name assigned to the container could be random or determined.
    

*PS: The Exited(0) shows that it exited with no errors.*

## Naming and Renaming Containers 🔤

### **Naming a Docker Container** 🏷️\*\*:\*\*

1. **During Container Creation:**
    

* You can provide a name to your container when you run the `docker run` command using the `--name` option.
    

```bash
docker run --name my_web_app -d -p 4444:80 nginx
```

* This command creates a container named "*my\_web\_app*" from the Nginx image.
    
    1. **Automatic Naming:**
        
    
    * If you don't specify a name during container creation, Docker will generate a random name for the container.
        

### **Renaming a Docker Container** ✍️

1. **Using the**`docker rename`**Command:**
    

* After a container is created, you can use the `docker rename` command to give it a new name.
    

```bash
docker rename my_web_app new_web_app
```

* This command renames the container from "*my\_web\_app*" to "*new\_web\_app*."
    
    1. **Using the**`--name`**Option with**`docker run`:
        
    
    * You can also use the `--name` option when running a container to rename it.
        
    
    **Example:**
    

```bash
docker run --name new_web_app -d -p 8080:80 nginx
```

This command not only creates a container from the Nginx image but also gives it the name "*new\_web\_app.*"

## Stopping and Killing Running Containers ⛔

We can stop running containers in two different ways:

1. Using the `docker stop` command:
    
    * The `docker stop` command is used to gracefully stop a running container.
        
    * It sends a **SIGTERM (Signal Terminate)** signal to the main process inside the container, allowing it to perform a graceful shutdown.
        
    
    ```bash
    docker stop [OPTIONS] CONTAINER [CONTAINER...]
    ```
    
    Usage:
    
    ```bash
    docker stop my_web_app
    ```
    

**Using**`docker kill` Command:

* The `docker kill` command forcefully stops a running container.
    
* It sends a **SIGKILL** signal to the main process, immediately terminating the container without allowing it to perform any cleanup.
    

Usage:

```bash
docker kill my_web_app
```

## Restarting and Starting Containers ♻️

Let's talk about restarting and starting Docker containers.

### **Restarting a Container 🔄:**

**1\. Using**`docker restart`**Command:**

* The `docker restart` command is used to restart a running container.
    
* It's like giving the container a fresh start without changing any configuration.
    

**Example:**

```bash
docker restart my_web_app
```

* This command restarts the container named "*my\_web\_app.*"
    

**2\. Restart Policies:**

* Docker also allows you to set restart policies when running a container. For example, you can specify the `--restart always` option to ensure that the container automatically restarts if it stops unexpectedly.
    
* After a system reboot, containers that were set to restart automatically (`--restart always`) will restart along with the system
    

**Example with Restart Policy:**

```bash
docker run --name my_web_app --restart always -d -p 4444:80 nginx
```

* This creates a container named "*my\_web\_app*" with an always restart policy.
    

### **Starting a Container** ▶️\*\*:\*\*

**1\. Using**`docker start`**Command:**

* The `docker start` command is used to start a stopped container.
    
* It's like turning on a computer that was previously shut down.
    

**Example:**

```bash
docker start my_web_app
```

This command starts the previously stopped container named "*my\_web\_app.*"

## **Creating Containers Without Running** ➕

1. **Using**`docker create`**Command:**
    

* The `docker create` command creates a container but doesn't start it. It returns the container ID.
    

**Example:**

```bash
docker create --name my_container -p 8080:80 nginx
```

This command creates a container named "*my\_container*" from the Nginx image but does not start it.

1. **Inspecting the Created Container:**
    

* After creating a container, you can inspect its details using `docker inspect`.
    

**Example:**

```bash
docker inspect my_container
```

This provides detailed information about the container, including its configuration.

If you are too lazy to run this 😅 or don't have a way the output look like this:

```bash
[
    {
        "Id": "ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd",
        "Created": "2024-01-30T18:15:37.414478695Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 3697,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-01-30T18:15:37.782785297Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:a8758716bb6aa4d90071160d27028fe4eaee7ce8166221a97d30440c8eac2be6",
        "ResolvConfPath": "/var/lib/docker/containers/ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd/hostname",
        "HostsPath": "/var/lib/docker/containers/ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd/hosts",
        "LogPath": "/var/lib/docker/containers/ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd/ab80c5531a80787699fc6c98572796959fc0c330a992619d6d698b90b10492dd-json.log",
        "Name": "/my_web_app",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "4444"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                42,
                156
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b15ed1497ee800f03042bd35dada5c99cd2de2a90da7206ea9621ceea7429161-init/diff:/var/lib/docker/overlay2/1a82b9959b1bb8f54ef4c8450829bc8797d59dd40ce746fe8b9806ad529ea2ee/diff:/var/lib/docker/overlay2/853fb155ddbaae3de176c6fcdb86b53914a3eeba4bb1e68a58114d8a4aa8c092/diff:/var/lib/docker/overlay2/b38e47010898a402a1cc9a78dac57a81e7bc2c7ab6e9e3a541056d705f011fc6/diff:/var/lib/docker/overlay2/3c472c4a5ecd937a76b0a13daaa971fa54e58873dc234c5478abfcbb8c6e6b76/diff:/var/lib/docker/overlay2/39845d79f35d1336256c1fa938137f89ead8a807310c9c3f1d5dc41689bfbb7a/diff:/var/lib/docker/overlay2/85ae196f1cb45440b1b2fafdaa1ff4c76b85087527c9e9ebc9074c73bf4b11bc/diff:/var/lib/docker/overlay2/ebd1d282dc7b22c0cddc6340c798ad63076ae0bdb613088adce8c5ae5e37e7bb/diff",
                "MergedDir": "/var/lib/docker/overlay2/b15ed1497ee800f03042bd35dada5c99cd2de2a90da7206ea9621ceea7429161/merged",
                "UpperDir": "/var/lib/docker/overlay2/b15ed1497ee800f03042bd35dada5c99cd2de2a90da7206ea9621ceea7429161/diff",
                "WorkDir": "/var/lib/docker/overlay2/b15ed1497ee800f03042bd35dada5c99cd2de2a90da7206ea9621ceea7429161/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "ab80c5531a80",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.25.3",
                "NJS_VERSION=0.8.2",
                "PKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers \u003cdocker-maint@nginx.com\u003e"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "f0fcc8186e94c2c4df9dd887fe51d9d513a772ff1b76dfb5f0972ab7c51dec33",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "4444"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/f0fcc8186e94",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "be78a709cb55c2b762b8c9872a700c813ad9e7bed1000abbdd36288c9ab14ed1",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "MacAddress": "02:42:ac:11:00:02",
                    "NetworkID": "361aa8b6588c5e503ad190c970fb5336aa895157a017f9e02228663d6e4cff0c",
                    "EndpointID": "be78a709cb55c2b762b8c9872a700c813ad9e7bed1000abbdd36288c9ab14ed1",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DriverOpts": null
                }
            }
        }
    }
]
```

1. **Starting the Created Container:**
    

* Once the container is created, you can start it using the `docker start` command.
    

**Example:**

```bash
docker start my_container
```

This command starts the container named "*my\_container*."

* The `docker run` command is essentially a combination of `docker create` and `docker start`.
    
* When you run `docker run`, it creates a new container and then starts it.
    

### **Benefits of Creating Without Running** 🎖️\*\*:\*\*

* **Configuration Inspection:**
    
    * You can inspect the container's configuration before starting it, making sure everything is set up as expected.
        
* **Customization Before Start:**
    
    * You have the opportunity to customize container options before starting it, such as network settings, volumes, etc.
        
* **Efficient Container Management:**
    
    * By separating creation and start steps, you have more control over when and how containers are initiated.
        

## **Removing Dangling Containers** 🧹

1. **Dangling Containers:**
    

* Dangling containers are containers that were created but are no longer running. They can accumulate over time and occupy disk space.
    

1. **Using**`docker run --rm`**:**
    

* The `--rm` option in the `docker run` command automatically removes the container once it stops. This is useful for temporary containers.
    

**Example:**

```bash
docker run --rm -d -p 8080:80 nginx
```

This command creates and starts a container from the Nginx image, and once the container stops, it is automatically removed.

1. **Removing Dangling Containers Manually:**
    

* You can manually remove dangling containers using the `docker rm` command.
    

**Example:**

```bash
docker rm $(docker ps -aq -f status=exited)
```

This command removes all containers with a status of "exited."

* `docker ps`**:**
    
    * This is the basic command to list Docker containers. It displays a list of currently running containers.
        
* `-a`**:**
    
    * This flag stands for "all" and is used to show all containers, not just the running ones. It includes both running and stopped containers.
        
* `-q`**:**
    
    * This flag stands for "quiet" and is used to display only the container IDs, making the output more concise. It's often used in combination with other commands to get specific information.
        
* `-f status=exited`**:**
    
    * This filter (`-f`) is used to narrow down the list of containers based on a specific criterion. In this case, it filters containers based on their exit status.
        
    * `status=exited` means that only containers with an "exited" status are shown.
        

1. **Using**`docker system prune`**:**
    

* The `docker system prune` command is a powerful tool for cleaning up your Docker environment. It removes all stopped containers, unused networks, dangling images, and more.
    

**Example:**

```bash
docker system prune
```

* This command interactively removes all dangling resources.
    

We can also use the `docker container prune` for a safer way!

### **Why Removing Dangling Containers is Necessary** 🤔\*\*:\*\*

* **Disk Space Optimization:**
    
    * Dangling containers consume disk space. Regularly removing them helps optimize disk usage.
        
* **Resource Management:**
    
    * Unused containers can clutter your environment, making it harder to manage and troubleshoot.
        
* **Security and Privacy:**
    
    * Clearing out unnecessary containers reduces the risk of exposing sensitive information unintentionally.
        
* **Efficiency:**
    
    * Cleaning up unused containers ensures a more efficient and responsive Docker experience.
        

## Running Container in Interactive Mode 🖇

Running containers in interactive mode is a way to directly interact with a container's shell or command prompt. This mode allows you to execute commands inside a running container in real-time. The `-i` (interactive) and `-t` (tty or terminal) options are commonly used to enable this interactive mode.

1. **Using**`-i`**(Interactive):**
    
    * The `-i` option stands for interactive. It keeps the standard input (stdin) open even if it is not attached, allowing you to interact with the container's shell.
        
    
    **Example:**
    
    ```bash
    docker run -i ubuntu
    ```
    
    * This command starts an Ubuntu container in interactive mode.
        
2. **Using**`-t`**(TTY or Terminal):**
    
    * The `-t` option allocates a pseudo-TTY, essentially giving you a terminal connection to the container.
        
    
    **Example:**
    
    ```bash
    docker run -i -t ubuntu
    ```
    
    * This command starts an Ubuntu container in interactive mode with a terminal connection.
        
3. **Combining**`-i`**and**`-t`:
    
    * It's common to combine both options (`-it`) when you want to run a container interactively with a terminal.
        
    
    **Example:**
    
    ```bash
    docker run -it python
    ```
    
    * This command starts a Python container in interactive mode with a terminal.
        

Certainly! Executing commands inside a container is a fundamental aspect of working with Docker. It allows you to run specific commands or interact with the container's environment. Here's a simple explanation:

### **Executing Commands Inside a Container** 🛠️\*\*:\*\*

1. **Using**`docker exec`**Command:**
    
    * The `docker exec` command is used to execute commands inside a running container.
        
    
    **Syntax:**
    
    ```bash
    docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
    ```
    
2. **Example:**
    
    * Let's say you have a running container named "*my\_web\_app*," and you want to execute a command inside it. For instance, you want to list files in the `/app` directory.
        
    
    ```bash
    docker exec my_web_app ls /app
    ```
    
    * This command runs `ls /app` inside the "*my\_web\_app*" container, listing files in the `/app` directory.
        
3. **Understanding the Parts:**
    
    * `docker exec`: The command itself.
        
    * `my_web_app`: The name or ID of the running container.
        
    * `ls /app`: The command to be executed inside the container.
        

### **Why execute commands inside a container** 🤔\*\*?\*\*

* **Application Management:**
    
    * It allows you to manage applications running inside containers by executing specific commands or scripts.
        
* **Debugging:**
    
    * It is useful for troubleshooting and debugging, allowing you to inspect the container's environment.
        
* **Configuration:**
    
    * Execute commands to configure or customize settings within the container.
        

### **Practical Example** 🔧\*\*:\*\*

1. **Start a container** 🚀\*\*:\*\*
    
    * Start a container named "*my\_web\_app*."
        
    
    ```bash
    docker run -d --name my_web_app nginx
    ```
    
2. **Execute a command inside the container** ⚙️\*\*:\*\*
    
    * Execute a command (e.g., list files in the Nginx default directory).
        
    
    ```bash
    bashCopy codedocker exec my_web_app ls /usr/share/nginx/html
    ```
    
3. **See the result** 📈\*\*:\*\*
    
    * View the output of the executed command.
        
    
    ```bash
    index.html
    50x.html
    ```
    

### **Quick Tips** 💡\*\*:\*\*

* **Multiple Commands** 🧬\*\*:\*\*
    
    * You can execute multiple commands by separating them with semicolons or using shell syntax.
        
    
    ```bash
    docker exec my_web_app sh -c "echo Hello; ls /usr/share/nginx/html"
    ```
    
* **Interactive Mode** 🕹️ **:**
    
    * For more interactive sessions, you can use the `-it` options with `docker exec`.
        
    
    ```bash
    docker exec -it my_web_app sh
    ```
    
    **Note**❗: T**he**`run`**command will spin up a new container for you to use.The**`exec`**command will allow you to use a container that is already running**.
    

```bash
docker container run --rm busybox sh -c "echo Hello"
```

> This article provides a comprehensive guide on manipulating Docker containers. Topics covered include running containers and their options, publishing ports, running containers in detached mode, and listing containers. It also discusses naming and renaming containers, stopping and killing running containers, and restarting and starting containers. The article details creating containers without running, removing dangling containers, running containers in interactive mode, and executing commands inside a container. The guide aims to help readers understand how to efficiently manage, debug, and customize their Docker containers.

That is it for this part. If you have any suggestions, leave them in the comments.  
Till next time ✌️.

Happy learning and teaching 🎓!