
**You will learn how to create, run, build, push, pull, kill, prune and work in docker with flask as an api.**

# How to USE
* Pull the image from docker-hub

	   $ docker pull rocktim/hello-api:hello-world


*  To Check the image you pull

	    $ docker images
    
	    REPOSITORY  		TAG    		IMAGE ID      CREATED         SIZE  
	    rocktim/hello-api  hello-world 	ddc23d92067e  33 minutes ago  942MB

*  To run the image

	`	$ docker run -p 8088:8053 rocktim/hello-api:hello-world`

	where,
	  -p 8088:8053 :- Map TCP port 8053 in the container to port 8088 on the Docker host.


# Create Ur Own
- [Setup Steps](#steup-steps)
- [Creating the Files](#Creating-the-Files)
- [Docker Build](#Docker-Build)
- [Docker Run](#Docker-Run)
- [Push Your Image To Docker Hub](#Push-Your-Image-To-Docker-Hub)

## Setup Steps
Create a folder to hold the project.

    mkdir hello_docker
Navigate to that directory with `cd` .

    cd hello_docker
Make sure you have docker installed

    $ docker -v  
	Docker version 17.12.0-ce, build c97c6d6
if not go to this link [Install Docker](https://docs.docker.com/install/)

Now that docker is ready lets see if you have any running containers.

    $ docker ps  
    CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES  
    <I do not have have any running right now>
If you are just getting started, there shouldn’t be any here. Either way it won’t hurt to have another one running at the same time.

Have some currently running and want to  `kill`  them?

    $ docker kill <CONTAINER ID>

You can also check to see if you have any containers even if they are not running.

## Creating the Files

## Docker Build

## Docker Run

## Push Your Image To Docker Hub


 
	
