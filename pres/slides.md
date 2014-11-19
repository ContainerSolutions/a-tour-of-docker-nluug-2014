# A Tour of Docker
<br/>
### The Application Container Engine
<br/>

ir. Frank Scholten
<br/>
<br/>
NLUUG Fall Conference 2014

-

### Bio
<br/>
#### ir. Frank Scholten
<br/>
#### Container Solutions
#### http://www.containersol.com

<br/>

- Easier, faster software delivery
- Automation
- Using Docker and related tech
 
-

### Agenda
<br/>
#### What is Docker?
<br/>
#### The Docker container
<br/>
#### Use cases
<br/>
#### Docker Architecture
<br/>
#### Ecosystem

-

## What is Docker?

-

### What is Docker?
<br/>
#### Engine for creating application containers
<br/>
#### Originally based on Linux Containers (LXC)
<br/>
#### Container = Linux image + process + virtual devices
<br/>
#### Docker command line interface + server

-

### Docker background
<br />
#### Released by Solomon Hykes in March 2013
<br />
#### Written in Golang + a little C
<br />
#### Github hall of fame: 16,666 stars, 3,301 forks
<br />
#### 75% commits from community contributors
<br />
#### Backed by Docker inc. (formerly dotCloud)
<br />
#### Catalyst for a lot of related OSS projects
<br />

-

## The Docker container

-

### Create a Docker container
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/10?size=medium&scrolling=no" async></iframe>

-

### A `/bin/bash` container on the host
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/16?size=medium&scrolling=no" async></iframe>

-

### Inside the `/bin/bash` container...
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/48?size=medium&scrolling=no" async></iframe>

-

### Linux kernel namespaces
<br/>
#### Provides process isolation 
<br/>
#### Container ethernet devices, hostname + more 
<br/>
##### See http://blog.dotcloud.com/under-the-hood-linux-kernels-on-dotcloud-part
<br/>
#### Docker & Golang do not yet support user namespaces
<br/>
##### See https://code.google.com/p/go/issues/detail?id=8447

-

### What about container file I/O?
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/8?size=medium&scrolling=no" async></iframe>

-

### Docker uses AUFS 

<br />

#### Advanced multilayered Unification FileSystem

<br />

#### Docker container filesystem is collection of layers

<br />

#### Layers can be cached!

<br/>

-

### Save changes to an image
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/11?size=medium&scrolling=no" async></iframe>

-

### Share your image

<br/>
#### Create an account on the Docker hub
<br />
#### `docker push` your image
<br/>
#### Others can now `search` and `pull` your image

-

### Port forwarding
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/12?size=medium&scrolling=no" async></iframe>

-

### Volumes
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/13?size=medium&scrolling=no" async></iframe>

-

### Dockerfiles
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/7?size=medium&scrolling=no" async></iframe>

-

### Docker Use Cases

-

### Share your entire application

<br/>
#### Code + Libraries + Config files + Data
<br/>
#### Portable end-user environments
<br/>
#### This presentation runs in Docker too! 

-

### Enable a DevOps culture

<br/>
#### CAMS: Culture, Automation, Measurement, Sharing
<br/>
#### Dev + Ops can standardize on a shared artifact
<br/>
#### Deploy same container to dev, test, acc & prod
<br/>
#### Prevent 'configuration drift'

-

## Docker Architecture

-

### Docker server

<br/>

#### Listens on `/var/run/docker.sock` by default
<br/>

<iframe style="width: 840px; height: 600px;" src="http://localhost:3000/api/asciicasts/14?size=medium&scrolling=no" async></iframe>

-

### Listen on TCP port 
<br/>
#### DOCKER_OPTS="-H 0:5555"
<br/>
#### CAUTION: Very insecure!
<br/>
#### Add TLS!
#####See http://docs.docker.com/articles/https/

-

### Libcontainer
<br/>
#### Replacement of LXC userspace tools
<br/>
#### Low-level: namespaces, eth devices, etc
<br/>
#### Goal: standardize container API

-

### Golang
<br />
#### "C for the 21st century"
<br />
#### Produces single binary
<br />
#### Fast compilation time
<br />
#### Simple syntax
<br />
#### Garbage collection
<br />
#### Concurrency
<br />

-

### Golang & Docker
<br/>
#### Blog post Docker client code walkthrough
<br/>
#### See http://www.containersol.com/docker-code-walkthrough-what-happens-during-a-docker-run?

-

## Ecosystem

-

### Ecosystem
<br/>

- Cloud services

- Orchestration tools

- User environment managers

<br/>

#### And more!

<br/>

##### http://www.mindmeister.com/389671722/docker-ecosystem

-
 
### Docker Cloud Services
<br/>
#### Google Container Engine
<br/>
#### Amazon EC2 Container Service
<br/>
#### Both services offer:
- Self healing
- Replication
- Load balancing
 
-

### Orchestration Tools
<br />
#### Apache Mesos
<br />
#### Kubernetes
<br />
#### Consul

-

### User Environment Managers
<br/>
#### Vagrant, Fig
<br/>
#### Store runtime config in file
<br/>
#### Useful for end-users, devs and maintainers
<br/>

-

### Which tools to use?
<br/>
#### A lot of overlap in features
</br>
#### Time will tell which ones gain most adoption
</br>
#### Cloud services help experimentation

-

## Conclusions
 
-

### Conclusions
<br/>
#### Docker allows easy app sharing
<br/>
#### Vibrant and fast-moving ecosystem
<br/>
#### Try it yourself, it's fun!

-

## Thanks for listening!

-

## Questions?