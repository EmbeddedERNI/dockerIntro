# dockerIntro
files for the embedded community docker intro session

These files taken from the tutorial in the docker site: https://docs.docker.com/get-started/


# get docker

How to install and setup docker on linux (including raspbian). Very easy.

```bash

curl -sSL https://get.docker.com | sh

sudo usermod -aG docker pi
sudo reboot

```

# hello world

```bash
# Display Docker version and info
docker --version
docker version
docker info

# Execute Docker image
docker run hello-world

# List Docker images
docker image ls
docker images

# List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq

```

# example demo1

Example for building, running and storing a docker app from scratch.

Get the example files:

```bash

# get all the files

mkdir docker
cd docker

git clone -o github https://github.com/EmbeddedERNI/dockerIntro

cd dockerIntro/demo1
```

Build and run the image:

```bash
# build the image

docker build -t friendlyhello .

# run the image

docker run -p 4001:80 friendlyhello

# run the image as a service
docker run -d -p 4002:80 friendlyhello
```

Managing the containers and images:

```bash
# List all running containers
docker container ls

# List all containers, even those not running
docker container ls -a

# Gracefully stop the specified container
docker container stop <hash>

# Force shutdown of the specified container
docker container kill <hash>

# Remove specified container from this machine
docker container rm <hash>

# List all images on this machine
docker image ls -a

# Remove specified image from this machine
docker image rm <image id>
docker rmi <image id>
```

Uploading an image and running it (perhaps downloading it)

```bash
# Log in this CLI session using your Docker credentials (use them)
docker login


# Tag <image> for upload to registry
docker tag <image> username/repository:tag

# Upload tagged image to registry
docker push username/repository:tag

# Run image from a registry
docker run username/repository:tag

```


# example demo1swarm

Example that uses image created in previous example to form a swarm.


```bash

# initialize the swarm

docker swarm init

# deploy / start

docker stack deploy -c docker-compose.yml erniswarm


# see how it's running

docker service ls

docker service ps erniswarm_web


# connect the browser or curl, check the host names

docker container ls -q

curl -4 http://localhost:4000



# rescaling : edit the file and deploy again

docker stack deploy -c docker-compose.yml erniswarm


# turn off the swarm

docker stack rm erniswarm

docker swarm leave --force


```

