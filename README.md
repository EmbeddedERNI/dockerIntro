# dockerIntro
files for the embedded community docker intro session

These files taken from the tutorial in the docker site: https://docs.docker.com/get-started/

# example demo1

Example for building, running and storing a docker app from scratch.


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

