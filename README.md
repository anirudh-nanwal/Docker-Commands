### Docker initial
1. `docker run -p <host_port>:<container_port> <repo_name>/<project_name>:<tag>` - We have to bridge the container port and the local host port in order to access docker container.
2. `docker run -t -i -p <host_port>:<container_port> <repo_name>/<project_name>:<tag>` - Using this command, we can you Ctrl + C to terminate a process. Ctrl+C will not work for above command.
3. `docker run -t -i -p <host_port>:<container_port> -d <repo_name>/<project_name>:<tag>` - The -d flag will run the container in the detach mode in which the powershell will not be bound to the docker container. This command will return a container Id which we can use to track the logs.
4. `docker logs <container_id>` - Using this command, we can see the logs while still being in the detached mode. Container_Id can be the first 5 characters or the full id.
5. `docker logs -f <container_id>` - The -f flag will now track the logs but upon pressing Ctrl+C will stop tracing the logs instead of terminating/stopping the container.
6. `docker container stop <container_id>` - Stops a particular running container with container_id being first few characters.

### Docker images

1. `docker images` - To check all the downloaded images.
2. `docker tag <repo_name>/<project_name>:<tag_name> <repo_name>/<project_name>:<new_tag>` - To create a new tag (more like a branch of existing branch in Git) out of existing tag.
3. `docker pull <image_name>:<tag_name (optional)>` - To download a particular image. If no tag is provided then default tag name "latest" will be downloaded however, "latest" tag name may not be the actual latest version. To download the actual latest version, check the image versions on the docker registry.
4. `docker search <immage_name>` - To search a particular image on docker registry.
5. `docker image history <image_id>` - To look into all the steps performed to create a particular image with image_id as specified. You can get the image id from the command 12.
6. `docker image remove <image_id>` - Removes the image from local only.
7. `docker image inspect <image_id>`  - Provides all the details about an image.

### Docker containers

1. `docker container run -t -i -p <host_port>:<container_port> -d <repo_name>/<project_name>:<tag>` - This is the actual command that we run.
2. `docker container pause <container_id>` - Pauses the running container. If we run the logs command, we can see the application is still running but when we hit the URL, we won't get any response.
3. `docker container unpause <container_id>` - Resumes the paused container.
4. `docker container inspect <container_id>` - Returns the metadata about a specific container.
5. `docker container ls` - Returns a list of all the containers currently running containing the first few parts of container_id and the name of the container.
6. `docker container ls -a` - Returns a list of all the containers irrespective of their status.
7. `docker container prune` - Removes all the stopped containers.
8. `docker container logs -f <container_id>` - Provides the logs of the application running in the container.
9. `docker container stop <container_id>` - Gives some time to container and perform some last steps before terminating the application. (SIGTERM or graceful shutdown).
10. `docker container kill <container_id>` - Terminates the container immmediately. (SiGKILL or forcefull shutdown).
11. `docker container run -t -i -p <host_port>:<container_port> -d --restart=always <repo_name>/<project_name>:<tag>` - When we restart the docker, the restart flag will make sure that the container ( if it was not stopped before restarting the docker) will be restarted as well. The default value of this flag is no

### Docker stats and systems

1. `docker events` - Binds the command line to track all the events that are fired whenever we run a command in a separate command line window. For example, if we stop or start a container, then this event will be tracked in the command line which was bound to the `docker events` command.
2. `docker stats` - Binds the command line to show statistics of all the running containers.
3. `docker container run -t -i -p <host_port>:<container_port> -m 512m --cpu-quota 5000 -d <repo_name>/<project_name>:<tag>` - This new container can use maximum of 512 mb of memory because of the -m flag. Using --cpu-quota flag, this container will use 5% of the CPU. The maximum value for this is 100000.
4. `docker system df` - Tells about the docker daemon, like, how many containers, volums, images exist and what is the total sie of each type.
5. `docker top <container_id>` - All the processes that are running in a specific vontainer.


### Docker compose

1. `docker-compose up` - Uses the docker-compose.yaml file to start the containers on a specific network mentioned in the yaml file. The yaml also contains certain configurations like dependency of a service and on what will be the bridge port.
