1. List all Containers running on machine
    1. docker ps
2. List all containers every created on machine
    1. docker ps --all
3. docker create hello-world = creates a image with name hello-world
4. docker start -a link = Running image with attached output i.e. output is displayed on the terminal
5. docker start link = Running image without output attached
6. docker system prune =
    1. This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all dangling build cache
    2. It is recommended to execute prune command to clean local containers and memory allocated by them
7. docker logs <containerId> = to see all the logs that executed when the container was started or for other actions
8. docker stop <containerId> or docker kill = to stop the running container
    1. Kill is hard stop
    2. Stop is where signals are given, and it shut-downs at it own time
    3. if we run stop command it gives 10 sec for container to stop however if it is not able to shut down within 10 sec
       then it will issue kill command automatically
9. docker exec -it <containerId> command
    1. docker = reference to docker client
    2. exec = Run another command
    3. -it = Allows us to provide input to the container
    4. containerId = Id of the container
    5. command = command to execute
10. docker exec -it <containerId> sh = Allows us to run terminal or shell inside the executing containers
11. docker build . = to build the docker file and send it to docker client which further sends it to docker server for
    heavy lifting
12. docker build -t <dockerId>/<imageName>:version . = to tag the container with the name
13. docker run -p <localhostport>:<conmtainerport> <imageId> = to mapper localhost port to the container port