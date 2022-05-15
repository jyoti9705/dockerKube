1. What is container?
    1. Containerization is a way to package the application with all the necessary dependencies and configurations
    2. It is portable artifact and can be moved around
    3. It makes deployment and development more efficient
2. Where are containers stored?
    1. Containers are stored in Container repository
    2. Where is this repository?
        1. Some companies have their own repositories
        2. There is also a public repository for docker i.e. Docker Image where 1000 to 10,000 containers are present ,
           some containers have official image and some are non-official
3. Life before containers?
    1. We will have to install each software for different OS Environments
    2. Installation can be Tedious and time-consuming
    3. Chances of going wrong are also higher
    4. Deployment
        1. Developers create a jar with list of steps to install it
        2. Developers provide a Database and list of steps for there installation
        3. These textual installation steps are given to operations team
        4. Operation team sets up environment to install these jars
        5. Problem with this type of approach is that it can lead to confusion between operations person and developer
           at times
4. Life after containers?
    1. We need not directly install anything on the OS Environment
    2. We can instead check the repository and import the images
    3. Container has its own environment with all required dependencies
    4. There is only command to install the application
    5. We can also run 2 versions of same applications without any conflict
    6. Deployment
        1. There will be only shared environment where everything will be uploaded
        2. Both Developer and operations person can use the same shared environments
5. What is technically containers made up off?
    1. Containers are layers of images
    2. In the base we have linux image because small
    3. We have application image on the top
6. What is docker?
    1. Docker is an open source containerization platform. It enables developers to package applications into
       containers—standardized executable components combining application source code with the operating system (OS)
       libraries and dependencies required to run that code in any environment.
7. Open terminal and run command docker run hello-world
    1. When we run this command docker cli gets activated , docker cli is responsible for taking commands from user and
       execute them by sending the commands to the docker server
    2. Docker server searches for image in the image cache , since we are running this command for the first time on the
       local , docker image would not be found on local so the request now goes to the free repository i.e. Docker Hub
    3. DockerHub downloads the image and the image are then stored in the local image cache
    4. Once the image is available docker creates container for image to run the program in it
    5. Image is a single file with all the dependencies and container is an instance of the Image which is used to run
       the program
    6. Image Cache present on local since now has the image that we asked for it will execute the run command next time
       easily without any delays
    7. We can override the default run command with some action at the end like docker run busybox ls or docker run
       busybox echo
        1. Point to remember over here is that you can run ls or echo only if this command is somewhere present in the
           image only then it will be available in the container for execution
8. Command to see all the running containers
    1. docker ps
9. To see list of all containers ever created on machine
    1. docker ps --all
10. Container lifecycle
    1. docker run = docker create + docker start
    2. Docker create actually means creating the filesystem or an image and docker start means running that image
    3. Creation of Container is separate from starting of container.
    4. Two containers do not auto share there disk space
11. Building own image
    1. To build your own image we need our docker file with a couple of configurations , these configurations are
       behaviour of how our container will behave or what are list of programs it will run once it is started up
    2. Docker file is then passed to docker client i.e. terminal , docker client sets it to docker server for doing the
       heaving lifting for creating image
    3. Creating Docker file is almost similar for all types of applications
        1. We need to specify base image for our container
        2. Run commands and add additional programs requires as dependency
        3. Provide command to run the container on start up
    4. Specifying base image for container is like installing operating system which is essential for the further
       process to run
    5. Run commands and programs are everything required to for container to work on starting
    6. Once we have docker file ready we will give it from docker cli to server using command docker build .
        1. Docker will check if the base image is present
        2. If not it will reach to docker hub to download the image
        3. then It will create a container out of it with commands added and file snapshot
        4. It will further go for execution and create a new container on top of old one and delete the temporary
           containers
        5. If we try to rebuild containers with same commands then it will use data from cache to build new containers
    7. If we try to change our docker file docker will only rebuild from the command that it has changed rather than
       creating new containers again
    8. We can also tag a docker image so that it becomes easy for identification
        1. Tagging can be done using command
        2. docker build -t dockerUserName/imageName:version .
        3. Now to run this image once it is built we can use command docker run dockerUserName/imageName
        4. There is no need to explicitly mention version to run docker once image is built
        5. Ideally just the version is the tag rest all the known items
    9. Container port mapping
        1. When we start the application all the request comes to the port specified
        2. Now there is no mapping provided tp route the request coming on the local port to the container port
        3. To route the request coming from the server to the container port we need to the mapping of the port to the
           container
    10. Docker takes snapshots of file in the working directory that we have build so if we have modified anything
        inside the file it will not auto reflect , we will have to rebuild the application to see our changes