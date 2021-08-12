# docker-commands
A list of basic docker commands that you would most probably end up using.

## Lets get it started

### Docker - Version
Gives docker client and the server version

```bash
docker version
```

## Docker - Run

### Run - Attached Mode
Docker run command Pull / download the image and runs the container. **If the docker is unable to find the mentioned image, it tries to fetch it from [Docker Hub](https://hub.docker.com/) which is the default docker repository**. 

By default docker runs in attached mode. Meaning you're attached to the console where the output is being printed and cant do anything else till the docker has finished running.

```bash
docker run <image-name>
same as
docker run -a <image-name>
```

### Run - Detach Mode
Runs in detached mode. Meaning your docker container is spinning up in the background and you can run other commands on the console. Once the container is up the SHA of the container os outputted.

```bash
docker run -d <image-name>
```

Run docker container in interactive mode and attached terminal

```bash
docker run -it <image-name>
```

## Docker - List Containers

List all running container

```bash
docker ps
```

List all running as well as previously exited containers

```bash
docker ps -a
```

## Docker - Start/Stop Container


Starts container with the matching name.

```bash
docker start <container-name>
```

Stops docker container with the matching name. Dosent delete docker image

```bash
docker stop <container-name>
```

Delete the docker container. Note: All the state and data within the container will be lost on destroying the container.

```bash
docker rm <container-name>
```


## Docker Images

List of images present and their size

```bash
docker images
```

Only pulls / downloads the image and stores it on our host but does not run it. By default docker tries to fetch it from [Docker Hub](https://hub.docker.com/) which is the default docker repository

```bash
docker pull <image-name>
```

Deletes the docker image. Remember to delete all dependent containers (Containers running from that image) firt to remove the image

```bash
docker rmi <image-name>
```


## Docker - Logs

Returns all data about the container in the JSON format

```bash
docker inspect <container-name>
```

View the logs of container

```bash
docker logs <container-name>
```

## Docker - Port Mapping / Port Declaration

Since the container run in an isolated environment, you cannot access the container from outside the host (Machine that is hosting the container). Eg from a web browser. In order to make the container accessible to outside world we need to map the port between host and the container.
On mapping the ports all the traffic on the host machine port is redirected to container port and vise-versa.

```bash
docker run -p <host-port>:<container-port> <image-name>
Eg: docker run -p 3120:8080 node:latest
```

## Docker - Volume Mapping
Maps volume on your host machine with volume on docker container so that the data is not deleted when the docker container is deleted/destroyed.

```bash
docker run -v <host-volume>:<container-volume> <image-name>
Eg: docker run -v /opt/datadir:/var/lib/mysql mysql
```

## Docker - Environment Variables:
You can set/pass environment variables to the application running in the container.

```bash
docker run -e <key=value> <image-name>
Eg: docker run APP_COLOR=Green simple-webapp-color
```

## Docker - How to create your own image? :thinking:
* First decide what needs to be containerized.
* Write down steps that you would take if you do it manually **in the write order**.
* Create Dockerfile in the folder with the instructions decided in step 2.
* Build image with docker build command.

Eg: For creating simple Flask application
1. OS - Ubuntu
2. Update apt repo
3. Install dependencies using apt
4. Install Python dependencies using apt
5. Copy source code to /opt folder
6. Run the web server using flask command

Eg: Dockerfile for simple Flask application

```bash
FROM Ubuntu

RUN apt-get update
RUN apt-get install python

RUN pip install flask
RUN pip install flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```
Build image
```bash
docker build --name simple-python-app 
```

## Contributing and Licence
This repo is only for educational purpose. Feel free to do clone, modify and share this repository.
If you find an error or have questions, feel free to write comments or raise an issue. If you want to contribute, feel free to hand in a
pull-request.
