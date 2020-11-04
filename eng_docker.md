### Docker


##### common commands

List docker images: `docker image ls`
list docker containers: `docker ps -a`
remove docker container: `docker rm ` 

start a container from an image `sudo docker run -d -p 8090:8080 [imagename]]`

[start tutorial](https://docs.docker.com/get-started/)

##### Basic usages on ubuntu

Basic docker configuration:
```
sudo service docker start
export DOCKER_HOST=127.0.0.1:2375
```

compose a docker from a dockerfile:

```
sudo docker-compose up
```


[Create a new image](https://www.mirantis.com/blog/how-do-i-create-a-new-docker-image-for-my-application/)


##### FAQ on MAC:
- Host is not running.
```
bogon:tensorflow haojian$ eval "$(docker-machine env default)"
Error checking TLS connection: Host is not running
```
Solutions: 
```
it seems need to start docker-machine again.

$ docker-machine start default
$ docker-machine env default
$ eval $(docker-machine env default)
works for me
```

- [Save vs Export in Docker](https://my.oschina.net/zjzhai/blog/225112)

- [Docker port mapping](https://opskumu.gitbooks.io/docker/content/chapter5.html)
- Website hosting
	- `docker run -p 8080:8080` -> django: "python manage.py runserver 0.0.0.0:8080" -> can be visit at: {docker-machine ip default} = 192.168.99.100` -> http://192.168.99.100:8080/

- for projects with dockerfile already:
	- `docker build -t  pyannote-video .`  #pyannote-video is the docker image name
	- `sudo docker run -d -p 8090:8080 pyannote-video`
	- After few seconds, open http://<host>:8090 to see the welcome page.
		
		
		
- install docker on aws ubuntu 
	- [Docker install on EC2 Ubuntu 14.04](http://www.bogotobogo.com/DevOps/Docker/Docker_Install_On_EC2_Ubuntu.php)
	- [Official guidance](https://docs.docker.com/linux/step_one/) **works better**
	
	
- To start Docker in Mac
	- open quick start terminal from spotsearch
	- eval "$(docker-machine env default)"
	
	
- failed: port is already allocated.
	- `sudo service docker restart`
	
- Is the docker daemon running on this host
	- `sudo usermod -aG docker ubuntu` for aws ubuntu. 
	- It's mainly because of the user permission issue. need to check if "sudo" access works well. [Reference][https://docs.docker.com/v1.5/installation/ubuntulinux/]
	
	
- AWS run a python3 docker:
	- benefits over the virtualenv: no worries about lxml libraries & python-dev.
	- `docker run -i -t micktwomey/python3.4 ` [reference](https://github.com/micktwomey/docker-python3.4)
	
	
- To delete all the docker containers: `docker rm $(docker ps -a -q)`
- To delete all the images: `docker rmi $(docker images)`
	
- [cheat sheet](https://github.com/wsargent/docker-cheat-sheet/blob/master/README.md)

- To keep the docker running at the background in the server 
	- use screen before start a container and then start a container with an interactive bash.
	
- Enter a running docker container:
	- 
	$ sudo docker exec -i -t 665b4a1e17b6 /bin/bash #by ID
	or
	$ sudo docker exec -i -t loving_heisenberg /bin/bash #by Name
	$ root@665b4a1e17b6:/#
	

# Commands short cut

### Frequent commands

- `docker run -v /Users/haojian/:/data -t -i pyannote-video /bin/bash`
- `docker run -v /Users/haojian/projects/:/data -t -i pyannote-video /bin/bash `
- ` docker run -t  -v  /Users/haojian/projects/testvideo/:/data -i pyannote-video /bin/bash ` create a new container and start it with a bash and a mounted directory.

## Containers

[Your basic isolated Docker process](http://etherealmind.com/basics-docker-containers-hypervisors-coreos/).  Containers are to Virtual Machines as threads are to processes.  Or you can think of them as chroots on steroids.

### Lifecycle

* [`docker create`](https://docs.docker.com/reference/commandline/create) creates a container but does not start it.
* [`docker rename`](https://docs.docker.com/engine/reference/commandline/rename/) allows the container to be renamed.
* [`docker run`](https://docs.docker.com/reference/commandline/run) creates and starts a container in one operation.
* [`docker rm`](https://docs.docker.com/reference/commandline/rm) deletes a container.
* [`docker update`](https://docs.docker.com/engine/reference/commandline/update/) updates a container's resource limits.

If you want a transient container, `docker run --rm` will remove the container after it stops.

If you want to map a directory on the host to a docker container, `docker run -v $HOSTDIR:$DOCKERDIR`.  Also see [Volumes](https://github.com/wsargent/docker-cheat-sheet/#volumes).

If you want to remove also the volumes associated with the container, the deletion of the container must include the -v switch like in `docker rm -v`.

There's also a [logging driver](https://docs.docker.com/engine/admin/logging/overview/) available for individual containers in docker 1.10.  To run docker with a custom log driver (i.e. to syslog), use `docker run --log-driver=syslog`

### Starting and Stopping

* [`docker start`](https://docs.docker.com/reference/commandline/start) starts a container so it is running.
* [`docker stop`](https://docs.docker.com/reference/commandline/stop) stops a running container.
* [`docker restart`](https://docs.docker.com/reference/commandline/restart) stops and starts a container.
* [`docker pause`](https://docs.docker.com/engine/reference/commandline/pause/) pauses a running container, "freezing" it in place.
* [`docker unpause`](https://docs.docker.com/engine/reference/commandline/unpause/) will unpause a running container.
* [`docker wait`](https://docs.docker.com/reference/commandline/wait) blocks until running container stops.
* [`docker kill`](https://docs.docker.com/reference/commandline/kill) sends a SIGKILL to a running container.
* [`docker attach`](https://docs.docker.com/reference/commandline/attach) will connect to a running container.

If you want to integrate a container with a [host process manager](https://docs.docker.com/articles/host_integration/), start the daemon with `-r=false` then use `docker start -a`.

If you want to expose container ports through the host, see the [exposing ports](#exposing-ports) section.

Restart policies on crashed docker instances are [covered here](http://container42.com/2014/09/30/docker-restart-policies/).

### Info

* [`docker ps`](https://docs.docker.com/reference/commandline/ps) shows running containers.
* [`docker logs`](https://docs.docker.com/reference/commandline/logs) gets logs from container.  (You can use a custom log driver, but logs is only available for `json-file` and `journald` in 1.10)
* [`docker inspect`](https://docs.docker.com/reference/commandline/inspect) looks at all the info on a container (including IP address).
* [`docker events`](https://docs.docker.com/reference/commandline/events) gets events from container.
* [`docker port`](https://docs.docker.com/reference/commandline/port) shows public facing port of container.
* [`docker top`](https://docs.docker.com/reference/commandline/top) shows running processes in container.
* [`docker stats`](https://docs.docker.com/reference/commandline/stats) shows containers' resource usage statistics.
* [`docker diff`](https://docs.docker.com/reference/commandline/diff) shows changed files in the container's FS.

`docker ps -a` shows running and stopped containers.

`docker stats --all` shows a running list of containers.

### Import / Export

* [`docker cp`](https://docs.docker.com/reference/commandline/cp) copies files or folders between a container and the local filesystem..
* [`docker export`](https://docs.docker.com/reference/commandline/export) turns container filesystem into tarball archive stream to STDOUT.

### Executing Commands

* [`docker exec`](https://docs.docker.com/reference/commandline/exec) to execute a command in container.

To enter a running container, attach a new shell process to a running container called foo, use: `docker exec -it foo /bin/bash`.

## Images

Images are just [templates for docker containers](https://docs.docker.com/engine/understanding-docker/#how-does-a-docker-image-work).

### Lifecycle

* [`docker images`](https://docs.docker.com/reference/commandline/images) shows all images.
* [`docker import`](https://docs.docker.com/reference/commandline/import) creates an image from a tarball.
* [`docker build`](https://docs.docker.com/reference/commandline/build) creates image from Dockerfile.
* [`docker commit`](https://docs.docker.com/reference/commandline/commit) creates image from a container, pausing it temporarily if it is running.
* [`docker rmi`](https://docs.docker.com/reference/commandline/rmi) removes an image.
* [`docker load`](https://docs.docker.com/reference/commandline/load) loads an image from a tar archive as STDIN, including images and tags (as of 0.7).
* [`docker save`](https://docs.docker.com/reference/commandline/save) saves an image to a tar archive stream to STDOUT with all parent layers, tags & versions (as of 0.7).

### Info

* [`docker history`](https://docs.docker.com/reference/commandline/history) shows history of image.
* [`docker tag`](https://docs.docker.com/reference/commandline/tag) tags an image to a name (local or registry).

### Cleaning up

While you can use the `docker rmi` command to remove specific images, there's a tool called [docker-gc](https://github.com/spotify/docker-gc) that will clean up images that are no longer used by any containers in a safe manner.

## Networks

Docker has a [networks](https://docs.docker.com/engine/userguide/networking/dockernetworks/) feature.  Not much is known about it, so this is a good place to expand the cheat sheet.  There is a note saying that it's a good way to configure docker containers to talk to each other without using ports.  See [working with networks](https://docs.docker.com/engine/userguide/networking/work-with-networks/) for more details.

### Lifecycle

* [`docker network create`](https://docs.docker.com/engine/reference/commandline/network_create/)
* [`docker network rm`](https://docs.docker.com/engine/reference/commandline/network_rm/)

### Info

* [`docker network ls`](https://docs.docker.com/engine/reference/commandline/network_ls/)
* [`docker network inspect`](https://docs.docker.com/engine/reference/commandline/network_inspect/)

### Connection

* [`docker network connect`](https://docs.docker.com/engine/reference/commandline/network_connect/)
* [`docker network disconnect`](https://docs.docker.com/engine/reference/commandline/network_disconnect/)

You can specify a [specific IP address for a container](https://blog.jessfraz.com/post/ips-for-all-the-things/):

### TensorFlow relevant
- [Configure TensorFlow on Mac](https://github.com/stujo/tensorflow-what-is-it)
- FAQ docker command: 
	- `docker run -t -i gcr.io/tensorflow/tensorflow /bin/bash`
	- `docker run -p 8080:8080 -t -v   /Users/haojian/projects/bugbash_ml:/bugbash_ml -i   gcr.io/tensorflow/tensorflow  /bin/bash`
	-  ```-p 8080:8080``` maps the docker port to the local machine port.
	- `docker run -p 8080:8080 -t -v  /Users/haojian/projects/bugbash_ml:/bugbash_ml -i   bugbash_space  /bin/bash`
- Location of TensorFlow:
	- ```
		import site; site.getsitepackages()
			['/usr/local/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages']
	  ````