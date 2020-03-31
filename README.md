
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
At this point I am going to assume you have python  installed.

    $ python --version  
    Python 3.6.2
For creating Flask Application you need to install Flask.

    $ pip install flask

Create a new file in your `hello_docker` folder called app.py with some basic flask code in it.

**app.py**

    #app.py file
    
    from flask import Flask
    
	app = Flask(__name__)
	
    @app.route('/')
    def index():
	    return "Hello World API"
	    
    if __name__ == '__main__':
	    app.run(host='0.0.0.0',port=8053)

You will notice the python file imports a few things. Although you might have them right now locally, the next person on the next machine won’t. So we need to create a  `requirements.txt`  file to import them when our docker runs.

**requirements.txt**

    flask

Now we need a `Dockerfile` in the same directory. It is just called `Dockerfile` , no extension, no suffix.

**Docker File**

    # Dockerfile
    FROM python:3

	WORKDIR /usr/src/app

	COPY requirements.txt ./

	RUN pip install --no-cache-dir -r requirements.txt

	COPY . .

	CMD ["python","./hello-api.py"]

This  `Dockerfile`  copies our current folder,  `.`  , into our container folder  `./`  . It sets `/usr/src/app` folder as the working directory, installs all our requirements with  `pip install`  from  `requirements.txt`, and then runs the file using  `python app.py`.

Thats it, these are the 3 files you need to get started. My  `hello_docker` folder looks like this.

    hello_docker  
    │  
    └───requirements.txt  
    │  
    └───Dockerfile  
    │  
    └───app.py

## Docker Build

You should still be in your  `hello_docker`  directory.

Now we can build our docker image.

    $ docker build -t my_docker:latest .

You will get a bunch of fancy output with loading bars, but what are looking for it it to end with the following confirmation.

    Successfully built ddc23d92067e
    Successfully tagged my_docker_flask:latest
    
What does this do? We are building an image with the tag ( `--tag` , `-t` ) `my_docker:latest` that includes everything in the current directory, `.`

Now we can see what we created.

    $ docker images  
    REPOSITORY       TAG     IMAGE ID      CREATED         SIZE  
    my_docker	   latest   dec23792067e  45 seconds ago  687MB

But, is it running?

    $ docker ps  
    CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES

Nope! That is the next step.

## Docker Run
You can run the build you just created with the  `docker run`  command.

    $ docker run -d -p 8000:8053 my_docker:latest

However this has a few pieces I think are important. First thing is  `-d`  which detatches from the run. This means you won’t see any output. You can remove the  `-d`  if you would like to see the run process.

Okay, now we can see it is running!

    $ docker ps  
    CONTAINER ID IMAGE 	  COMMAND  CREATED   STATUS    			PORTS  
    9701 	  my_docker   python   app.py 3  min ago Up 4 min  0.0.0.0:5000

## Push Your Image To Docker Hub

Now you can push your image to docker hub so you can pull it down later and use it, thats why docker is awesome.

Create an account over at docker hub.

[https://hub.docker.com/](https://hub.docker.com/)

Then from your terminal window,

    $ docker login -u 'username'
    Password:Login Succeeded

Replace 'username' with your username

Now we re-tag the image with your username prefix,  `<username>/`.

    $ docker tag my_docker rocktim/my_docker_flask

And then you can push it to your docker hub.

    $ docker push rocktim/my_docker


 
	

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
At this point I am going to assume you have python  installed.

    $ python --version  
    Python 3.6.2
For creating Flask Application you need to install Flask.

    $ pip install flask

Create a new file in your `hello_docker` folder called app.py with some basic flask code in it.

**app.py**

    #app.py file
    
    from flask import Flask
    
	app = Flask(__name__)
	
    @app.route('/')
    def index():
	    return "Hello World API"
	    
    if __name__ == '__main__':
	    app.run(host='0.0.0.0',port=8053)

You will notice the python file imports a few things. Although you might have them right now locally, the next person on the next machine won’t. So we need to create a  `requirements.txt`  file to import them when our docker runs.

**requirements.txt**

    flask

Now we need a `Dockerfile` in the same directory. It is just called `Dockerfile` , no extension, no suffix.

**Docker File**

    # Dockerfile
    FROM python:3

	WORKDIR /usr/src/app

	COPY requirements.txt ./

	RUN pip install --no-cache-dir -r requirements.txt

	COPY . .

	CMD ["python","./hello-api.py"]

This  `Dockerfile`  copies our current folder,  `.`  , into our container folder  `./`  . It sets `/usr/src/app` folder as the working directory, installs all our requirements with  `pip install`  from  `requirements.txt`, and then runs the file using  `python app.py`.

Thats it, these are the 3 files you need to get started. My  `hello_docker` folder looks like this.

    hello_docker  
    │  
    └───requirements.txt  
    │  
    └───Dockerfile  
    │  
    └───app.py

## Docker Build

You should still be in your  `hello_docker`  directory.

Now we can build our docker image.

    $ docker build -t my_docker:latest .

You will get a bunch of fancy output with loading bars, but what are looking for it it to end with the following confirmation.

    Successfully built ddc23d92067e
    Successfully tagged my_docker_flask:latest
    
What does this do? We are building an image with the tag ( `--tag` , `-t` ) `my_docker:latest` that includes everything in the current directory, `.`

Now we can see what we created.

    $ docker images  
    REPOSITORY       TAG     IMAGE ID      CREATED         SIZE  
    my_docker	   latest   dec23792067e  45 seconds ago  687MB

But, is it running?

    $ docker ps  
    CONTAINER ID  IMAGE  COMMAND  CREATED  STATUS  PORTS  NAMES

Nope! That is the next step.

## Docker Run
You can run the build you just created with the  `docker run`  command.

    $ docker run -d -p 8000:8053 my_docker:latest

However this has a few pieces I think are important. First thing is  `-d`  which detatches from the run. This means you won’t see any output. You can remove the  `-d`  if you would like to see the run process.

Okay, now we can see it is running!

    $ docker ps  
    CONTAINER ID IMAGE 	  COMMAND  CREATED   STATUS    			PORTS  
    9701 	  my_docker   python   app.py 3  min ago Up 4 min  0.0.0.0:5000

## Push Your Image To Docker Hub

Now you can push your image to docker hub so you can pull it down later and use it, thats why docker is awesome.

Create an account over at docker hub.

[https://hub.docker.com/](https://hub.docker.com/)

Then from your terminal window,

    $ docker login -u 'username'
    Password:Login Succeeded

Replace 'username' with your username

Now we re-tag the image with your username prefix,  `<username>/`.

    $ docker tag my_docker rocktim/my_docker_flask

And then you can push it to your docker hub.

    $ docker push rocktim/my_docker
