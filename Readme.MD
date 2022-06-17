# What is Docker?

 Docker is a platform that lets you package, develop, and run applications in containers. A container is a virtual environment on top of the OS kernel to capture all of its software - libraries, dependencies, etc.

## Why does Docker matter?

 A more lightweight approach than virtual machines to isolated coding and project environments. Portability to the major architectures and operating systems. Helps achieve continuous integration and deployment for development operations.

## Who does docker affect most?

 Developers and software engineers. Operators and DevOps engineers. Start ups and enterprises.

## Main features

 Create containers and images. Docker compose for multicontainer applications. Docker swarm to utilize multiple machines running Docker.

 https://github.com/15Dkatz/docker-guides

## The Kernel

 The kernel is the software at the core of an operating system, with complete control. The CPU is the core circuitry which executes program instructions. Docker runs on top of original kernel - making it the host machine.
![image](https://media.discordapp.net/attachments/693899305584558081/984822350270828574/unknown.png)
## The docker engine

 Consists of the docker server, an API, and command line interface. The server is also called the docker daemon. A daemon is a background process on an operating system. Docker daemon is like a construction team on the host machine.
![image](https://cdn.discordapp.com/attachments/693899305584558081/984820986522239037/unknown.png)
## Docker container environments

The processes of one container cannot affect the process of another. A container has limits on resource usage like the CPU and memory. Application-specific code.

## What is a docker container?

A Docker container is a loosely isolated environment running within a host machine's kernel that allows us to run application-specific code.

## Why are containers useful?

Portability to multiple operating system environments.Less time setting up, more time coding. Development, continuous integration, deployment environments.

## Containers vs Virtual machines

Virtual machines abstracts an entire computer system. To run 2GB of software, on a VM it will require 2GBs to run the image, so on 5VMs it will require 10GB. To run it on containers you will need 2GB +0.001^Nn to run it. This is because of the file system and both systems have their advantages and disadvantages.

## Docker Images
Read only templates with instructions for creating docker container. Define the container code,libraries, environment variables, configuration files and more.

## Dockerfile

Outlines instructions for how an image will create a container.
## Image to container relationship
![](images\image%20to%20container.png)
## Dockerhub
Collects images from Docker users and hosts them as online repositories. 

## Run an Ubuntu container and a container Shell 10

`docker --version` # to check if working
Note if you have installed docker correctly and the version command doesn't work you might have to use an allias for windows `alias docker="winpty docker"`
`docker search ubuntu` # searchs through images called ubuntu
`docker create --help`
`docker create --name=foo -it ubuntu bash` #creates a docker container from an ubuntu image, giving it a name foo, -i makes it interactive,the bash gives it a terminal.and the t makes it look like a terminal session. This explains it better https://stackoverflow.com/questions/30137135/confused-about-docker-t-option-to-allocate-a-pseudo-tty
`docker container ls -a`
`docker start foo`
`docker attach` foo #ssh into the container
`ls` #shows that you are no longer on your old machine
`ctrl p+q` # triggers the read escape command this might cause issues on vscode but worked for me on gitbash
`docker logs foo` # shows all of the commands run 
`docker attach` foo
`apt-get update` # makes sure that our packages are up to date
`apt-get install iputils-ping` #installs ping package
`ping google.com` # run the ping command to google.com
Read escape sequence
`docker logs foo` Shows the logs from what has just happened will show the ping command.

## Run an Ubuntu container and a container Shell continued 11
`docker container --help`
`docker rm foo -f` # forced stop of the container foo
or `docker stop foo` and `docker rm foo` safe way of stopping the container
`docker container ls -a` # will show stopped foo container or nothing depending if you have used -f
`docker run --help` # Docker run can be used to combine the create and start
`docker run --name=bar -it ubuntu bash` # creates ubuntu container and starts bash
`docker image --help`
`docker image ls` Used to see the images pulled to the machine

## Docker images and the dockerfile 12
A read only template with instructions for creating a docker container.
A Dockerfile is a text document with various commands that assemble to biuld a container. A docker create image from FROM. Docker create image command CMD. COPY,RUN and more...

## Build a file server image 13
Do this in a docker directory
`mkdir serve`
`mkdir display`
`cat > display/foo.txt` Put some text in here to make sure it works.This allows you to create a txt file in the display directory without having to go there. I prefer to use nano.
`mkdir display/site`
`cat > display/site/index.html` Same as earlier but html
`touch Dockerfile` Creates a dockerfile without having to put anything in it.

The dockerfile can be editted in vscode.
```
FROM node:latest
RUN npm install -g serve
COPY ./display ./display
CMD serve ./display
```
The `FROM` command imports the latest version of an image. In this case it's node.js. You can search different version by putting `docker search node` in as a command.

The `RUN` command uses the inbuilt npm to install serve as a global variable in the container.

The `COPY` command copies the local `display` directory to the container directory, at the `./display` location.

The `CMD` is a command, it will call to run serve on the `./display` directory.

`docker build --help`
`docker build . -t frerf/serve` Builds the image. THis might take some time since the image is big
`docker image ls` shows that it has been created (it's large)
`docker run --name=serve -p=3001:3000 frerf/serve` creates a container using the image we created, and redirects port 3000 to 3001.
## Build an express.js image

`mkdir express`
`touch Dockerfile`
`touch server.js`
`touch package.json`

include the js,json and dockerfile here.

server.js
```
const express = require('express');
const app = express();
const HOST = "0.0.0.0"
const PORT = 80;

app.get('/', (req,res) => {
    res.send('Hello world')
});

app.listen(PORT,HOST);
console.log('Running on http://${HOST}:${PORT}');
```
package.js
```
{
    "dependencies": {
        "express":"^4.16.1"
    }
}
```
Dockerfile
```
FROM node
WORKDIR /home/node
COPY . .
RUN npm install 
CMD ["node","server.js"]
```


`docker build . -t fred/express`
`docker run --name=express  -dp=3002:80 fred/express` uses detached mode 

## Layered image cache and .dockerignore 16

Optimising the build process.

By including a .dockerignore file, it will make the copying portion more effective so the image will become smaller.

Caching will also make the process more effective. In our example if we copy over `package.json` it will be cached and make it more efficient. the `npm install` line will only run if there is something new introduced to the app.

## Build a PHP image 17

Building a docker image but with PHP.

Include the dockerfile and the php file.

## Build a Python Flask image 18

Building a docker image from a flask app.

Create a python file for the app, a txt for for the requirements and a dockerfile. Note this is something I need to come back to and look at, there's an issue here.

## Docker container storage - Mounts 20
Volume mounts - store data in a Docker-managed directory of the host file system.

Bind mounts - directly links directories on the docker host to the container.

Tmpfs mounts -write to the memory of the docker host 

![](images\container%20storage.png)

Use cases

Volume mounts - store data across multiple containers in a guaranteed space.

Bind mounts - allow for editing by the Docker host and Docker containers.

tmpfs mounts - work with data that should disappear as soon as possible.

## Volume mounts 21

`docker volume --help`
`docker volume create shared-vol`
`docker volume ls`
`docker inspect shared-vol`

Volume mount point is in a virtual machine.
`docker run -it --name=foo --mount source=shared-vol,target = /src/shared ubuntu bash`
## Bind Mounts 22
`mkdir bindmountdir`
`nano goo.txt`
`docker run -it --name=foo --mount type=bind,source="pwd/bindmoutdir",target=/src/mountdir ubuntu bash` note the source command doesn't have to be in quotes if there are zero spaces.

You will now find the goo file in the src/mountdir directory on the ubuntu machine.

This can also be done in revers, creating a txt file in the directory on the ubuntu machine and then finding it on the computer dir.

## Tmpfs mounts 23
Used for secret data or keys

## Docker container networking 25
The system fore how containers share resources and send messages to each other.

Default docker networks, bridge-default docker network. none containers without an IP. Host -shares the network with the host machine.

User defined private networks. Set up connections between a handful of docker containers. Embedded a DNS server. Need network drivers, most commonly:bridge

## Create a Docker container network 26

`docker network --help`
`docker network ls`
`docker run -itd --name=foo busybox`
`docker run -itd --name=bar busybox`
`docker network inspect bridge`
Take note of the ipv4
`docker attach foo`
`ping bar-ipv4-address`

private network
`docker network create privatenw`
`docker network ls`
`docker run --network=privatenw -itd --name=baz busybox`
`docker inspect privatenw`
Make a note of the IP
`docker run --network=privatenw -itd --name=goo busybox`
Make a note of the IP
`docker attach baz`
`ping Ipv4-address of goo`
You can't ping foo or bar because it couldn't connect to a container outside of it's own network.
You can also ping the name goo, because it acts like a phonebook.
`docker container ls -q | xargs docker rm -f`

## Docker Compose 27
What is docker compose? A tool for composing and building applications with more than one docker container. Containers in compose are services. Define services with docker-compose.yml.

Why is Docker compose useful? Start multiple containers with one command. Docker-coompose.yml is also great documentation.

Nice features of Docker compose. Private network for the compose application. Caches the services. Multi-container isolated environments.

docker-compose.yml. There are different versions of docker compose (video I'm watching says 3 is most recent so take that with a grain of salt). Format: key-value structure. Similar to xml or json. Compose options,services,build,image and more.

## Compose a two container App 28 and 29

Backend and frontend. For sports attributes.
Make a node-php directory. This should contain a docker-compose file and a players directory(containing a dockerfile,json file and js file).

`docker compose --help`
`docker compose up`

Explain the files later.

Make a new folder containing a php file and a dockerfile.
`docker compose up` should run both containers
