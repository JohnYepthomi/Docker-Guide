#A Guide to using Docker and Docker-Compose

**Docker** is used to run individual containers managed by the user, whereas **Docker-compose** does all the container _orchestration_ as specified in the _dockerfile_. For example, you can configure a container wait for another container to be ready in the dockerfile by using 
```
  depends_on:
    - <container_name>
```

##Run a Docker-compose Package
```
  docker-compose up -d
```

##Stop all Running Containers
```
  docker-compose down
```
##Start containers after making changes to the dockerfile to remove used containers
```
  docker-compose up -d --remove-orphans
```

##View all running Containers
```
  docker-compose ps
```

##Execute a command inside a particular container
```
  docker exec -it <container_name_or_id> <command>
  //it stands for interactive mode
  
  //get access to the bash sheel of the container to work with the mysql installed inside the container
  docker exec -it mysqlDB /bin/bash
```

##View logs of a container
```
  docker logs
  docker logs --tail <no of lines> --follow --timestamps <container_name>
```

#Volumes Mounting
  You can specify in the docker file if you need to mount any directory or file to a container.
  
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
  This will mount the directory specified in the <path outside container> to the <path inside container> in the container.
  
  So, if you have a directory that contains files that you want to use inside a particular container, you can specify an **absolute path** to the directory that you want in the <path outside cotnainer> and then specify where you want it to be mounted in the directory inside the container in <path inside container>.
  
