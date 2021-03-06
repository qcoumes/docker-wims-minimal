# Docker Wims
**Docker Wims** allows you to install Wims inside a Docker container with the full set of tools used by Wims.

## Getting Started
With this installation you will be able to run **several Wims instances**, each one in a docker container, by **sharing files** between containers and your local host. The **changes are refleted in real time** on **all instances**, **host machine** include.

## Prerequisites
Your system must have, at least, 3GB of free space.

## First Installation

### 1. Install Docker CE
First of all you have to install Docker, please follow these instructions : 
+ [Debian](https://docs.docker.com/install/linux/docker-ce/debian/#uninstall-old-versions)
+ [OSX](https://docs.docker.com/docker-for-mac/install/)
+ [Windows](https://docs.docker.com/docker-for-windows/install/)

### 2. Clone this repository
```
git clone https://github.com/ElaadF/docker-wims <directory's path>
```   
>**Note:** The directory must be empty if you use this command line to clone the project.

### 3. Build an image
Use this command to build an image from the Dockerfile in this repository. This will take several minutes.   
```
docker build -t <image's name> <Dockerfile's directory>
```

### 4. Run the container
If the previous step has succed, you have to run the container by creating and starting it with this following command :   
```
docker run -itd -p <host port>:80 -v <host directory's path>:<container target's path> --name <container's name> <image's name>
```   

+ ```<host port>``` is the port number which will serve to acces the Wims plateform in your web browser. An error will occur if the port number is alreaby taken.   
+ ```<image's name>``` should correspond to the previous name you have chosen.   
You have to choose the name of the container, otherwise a random name will be assigned.   
+ ```<host directory's path>``` is the directory's path containing all your files that you want to share with the container.   
+ ```<container target's path>``` is the directory's path in the container where your files will be available.    

You can create several containers with the same command, but the port and the name have to be different. If you want to share the same files you will need to put the same directory's path to these files as the other containers.   

At the end of this step you, you have created a container and it is running on your system. You can start and stop it by using these commands :   
```
docker container start <container's name>
docker container stop <container's name>
```   

### 5. Restart services
Run these commands :   
```
docker exec -it <container's name> ./bin/apache-config
docker exec -it <container's name> service apache2 restart
```   

>**Note:** Always run these commands **after** you start the container. Otherwise it will not work.

### 6. Acces from a web browser
If you have run the container on your own device, you can access to Wims by using this URL :   
**http://localhost:port_number_here/wims**   
You have to **specify the port number** you have chosen previously.

## Some useful commands
+ delete container :
```
docker container rm <name>
```
The container must be stopped before deleting it. 
>**Note:** You can specify several containers at one time, separating each name by a space.

+ List running container :
```
docker container ps 
```

+ List stopped container :
```
docker container ps -a
```

+ List image :
```
docker images
```

+ Delete image :
```
docker image rm <name>
```
>**Note:** if a container is using this image to run, you have to stop it first, and then, delete the image.

+ Open a shell into a container
```
docker exec -it <name> bash
```


