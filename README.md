# Docker Notes

### Installation
* Head over to docker.com and download suitable docker for your operating system.
* Run the installer and install Docker

### Image vs Container
* Image is like a CD having an operating system
* Container is like a machine which runs an operating system or more simply an image

### Commands
--> docker run -it ubuntu
__ Above command will first check if you have an image ubuntu on your system,
__ if yes then it will run a completely new container  else it will download the ubuntu image from hub.docker.com
__ and then run the new container

--> docker container ls
__ List all the running containers

--> docker image ls / docker images
__ List all the existing images


--> docker container ls -a
__ List all the containers even if it is not running

--> docker start {container_name}
__ Runs the stopped container with the specified name

--> docker stop {container_name}
__ Stops the container with the specified name


--> docker exec {container_name} {command}
__ Runs the specified command in the specified container
__ and fetches the result in the current context itself
__ i.e. without changing the container itself

--> docker exec -it {container_name} {command}
__ Same as above command but the context is changed to the
__ specified container


--> docker run -it -p {physical_machine_port}:{container_port}
__ By default the application running in a container is not accessible outside
__ so what the above command does is it exposes the specified container port to 
__ specified physical machine port

--> docker run -it -p {physical_machine_port}:{container_port} -e {key1}={value1} -e {key2}={value2}
__ To pass the environment variables to a docker container you can use -e and then 
__ key=value pair to pass the environment variables to a docker container

### Docker Containerize the application
* Create Dockerfile in the root folder of the application
* Write the steps to be followed as per conventions
* docker run build
* You have the builded image in the docker desktop/ directory


### Docker File (Example code)
FROM ubuntu

RUN apt-get update
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash -
RUN apt-get upgrade -y
RUN apt-get install -y nodejs

COPY package.json package.json
COPY package-lock.json package-lock.json
COPY main.js main.js

RUN npm install

ENTRYPOINT [ "node", "main.js" ]

### Push docker image to docker hub
--> docker push {image_name_as_per_docker_hub}
__ You may need to login before you push the image to the docker hub
