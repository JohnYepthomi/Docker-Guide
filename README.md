# A Guide to using Docker and Docker-Compose

**Docker** is used to run individual containers managed manually by a user. Whereas, **Docker-compose** does all the _**container orchestration**_ as specified in the ```docker-compose.yml```. For example, you can configure a container wait for another container to be ready in the dockerfile by specifying 

```docker-compose.yml```

```
  depends_on:
    - <container_name>
```

**Note**: you need to implement your own retry logic in your applications running inside containers. A container being ```UP``` doesn't gurantee that the applications inside its container is ready to respond to requests.

## Run a Docker-compose Package
```
  docker-compose up -d
```

## Stop all Running Containers
```
  docker-compose down
```
## Start containers after making changes to the dockerfile to remove used containers
```
  docker-compose up -d --remove-orphans
```

## View all running Containers
```
  docker-compose ps
```

## Execute a command inside a particular container
   We will use ```docker``` as we are targeting only a single Container. Remember, ```docker-compose``` is used for orchestration of multiple containers.
```
  docker exec -it <container_name_or_id> <command>
  //it stands for interactive mode
  
  //get access to the bash shell of the container to work with the mysql instance inside the container
  docker exec -it mysqlDB /bin/bash
```

## View logs of a container
```
  docker logs <container_name_or_id>
  docker logs --tail <no of lines> --follow --timestamps <container_name_or_id>
```

# Volumes Mounting in ```docker-compose```:

  ### You can specify directories in the ```docker-compose.yml``` file if you need to mount any directory or file to a container.
  
  ```
     volumes:
      - ./var/log/gorse:/var/log/gorse
      - ./var/lib/gorse:/var/lib/gorse
  ```
  The syntax is:
  ```
    volumes:
      - <path outside container>:<path inside container>
    //can be abolute path or relative paths. 
    //If you specify a relative path, docker will create directories for it in the current directory 
  ```
  This will mount the directory specified in the ```<path outside container>``` to the ```<path inside container>``` in the container.
  
  So, if you have a directory that contains files that you want to use inside a particular container, you can specify an **absolute path** to the directory that you want in the ```<path outside cotnainer>``` and then specify where you want it to be mounted in the directory inside the container in ```<path inside container>```.

##LIST CONTAINERS
 `sudo docker container ls -a`

##LIST IMAGES
  `sudo docker image ls -a`

##LIST ALL CONTAINERS (running/stopped):
  `sudo docker ps -a`

### CLEAN UP:
  REMOVE A CONTAINER: 
  `sudo docker container rm <container-name>`
  
 REMOVE A DOCKER IMAGE:
  `sudo docker image rm <container-name>`
