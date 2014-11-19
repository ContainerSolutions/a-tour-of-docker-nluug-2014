# A Tour of Docker
<br/>
### The Application Container Engine
<br/>

Frank Scholten
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
#### Golang
<br/>
#### Ecosystem

-

## What is Docker?

-

### What is Docker?
<br/>
#### OS-level virtualization for Linux
<br/>
#### Originally based on Linux Containers (LXC)
<br/>
#### An optimized Linux image
<br/>
#### An associated foreground process
<br/>
#### + many more interesting features...

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

<div style="text-align: left">
<br/>
`$ docker run -i -t ubuntu /bin/bash`
<br/>
`root@d0d69709ce29:/#`
<br/>
</div>

-

### A `/bin/bash` container on the host
<br/>

<div style="text-align: left">

`$ ps a -o pid,command | grep /bin/bash`  <br />
` 6081 docker run -i -t ubuntu /bin/bash` <br />
` 6088 /bin/bash` <br />
` 6570 grep /bin/bash` <br />
`$`
<br />
</div>

-

### Inside the `/bin/bash` container...
<br/>

<div style="text-align: left">

`root@d0d69709ce29:/# ps a`<br />
`  PID TTY      STAT   TIME COMMAND` <br />
`    1 ?        Ss     0:00 /bin/bash` <br />
`    8 ?        R+     0:00 ps a` <br />
`root@d0d69709ce29:/#`

</div>

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

<div style="text-align: left">

`root@d0d69709ce29:/# echo 'hello' > message`
<br/>
<br/>
`# cat /var/lib/docker/aufs/diff/d0d69709ce29`
<br/>
`hello`

</div>

-

### Docker uses AUFS 

<br />

#### Advanced multilayered Unification FileSystem

<br />

#### Docker container filesystem is collection of layers

<br />

#### Layers can be cached!

<br/>

#### Max 127 layers

-

### Create an image

<br/>

<div style="text-align: left;">
`$ docker commit -a "Frank Scholten" d0d69709ce29 frankscholten/hello` <br/>
`9c8738b48ce757f6bbaf8e588283...` <br/>
`$ docker images | grep hello` <br/>
`frankscholten/hello              latest              9c8738b48ce7        About a minute ago   199.3 MB`<br/>
</div>

-

### Share your image on the Docker hub!

<br/>

<div style="text-align: left;">
`$ docker push frankscholten/hello`
</div>

-

### Port forwarding

<br/>

<div style="text-align: left;">
`$ docker run -d -p 8080:80 nginx`<br/>
`da3bcc83dcd4092...` </br>
`$ curl -s 0:8080 | html2text | grep Welcome`<br/>
`****** Welcome to nginx! ******`
</div>

<br />

-

### Volumes

<br/>

<div style="text-align: left;">
`$ docker run -v /host:/container -it nginx`
</div>

-

### Dockerfiles

<br/>

<div style="text-align: left;">
`$ cat Dockerfile`</br>
`FROM ubuntu`<br/>
`MAINTAINER frank.scholten@containersol.com`<br/> 
`RUN echo hello > message` </br>
`CMD /bin/bash`<br/>
`$ docker build -t frankscholten/hello .`</br>
`Sending build context to Docker daemon  2.56 kB...`</br>
`Sending build context to Docker daemon`</br>
`Step 0 : FROM ubuntu`</br>
`---> 5506de2b643b`</br>
</div>

-

### Docker Use Cases

-

### Share your entire application
<br/>
#### Code + Libraries + Config files + Data
<br/>
#### All in a single Docker container!
<br/>

-

### Portable end-user environments

<br/>
#### Scientific computing environments
<br/>
#### Development environments
<br/>
#### Software maintenance

-

### Enable a DevOps culture

<br/>
#### CAMS: Culture, Automation, Measurement, Sharing
<br/>
#### Dev + Ops can standardize on a shared artifact
<br/>
#### Prevent 'configuration drift'

-

### Easier Deployment

<br />

#### Create a Jenkins & Docker deployment pipeline

<br />

#### Deploy same container to dev, test, acc & prod

<br/>

#### Host only has to run Docker 

-

## Docker Architecture

-

### Docker server

<br/>

#### Listens on `/var/run/docker.sock` by default

<br/>

<div style="text-align: left;">
`$ echo -e "GET /version HTTP/1.0\r\n" | nc -U /var/run/docker.sock`</br>
`{"ApiVersion":"1.12", "Arch":"amd64", "GitCommit":"990021a",
  "GoVersion":"go1.2.1", "KernelVersion":"3.13.0-39-generic",
  "Os":"linux", "Version":"1.0.1"}`
</div>

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

## Golang

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

### Libswarm
<br/>
#### Docker's own orchestration tool
<br/>
#### Goal: integrate with previously mentioned frameworks
<br/>

-

### Which tools to use?
<br/>
#### A lot of overlap in features
</br>
#### Cloud services help experimentation
</br>
#### Time will tell which ones gain most adoption

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