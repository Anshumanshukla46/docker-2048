# DockerFile  _____build__>  DockerImage   _____Run__>   DockerContainer



# base image form ubuntu22.22
FROM ubuntu:22.04

# to update all packages in my ubuntu machine
RUN apt-get update

RUN apt-get install -y nginx zip curl
# zip, curl, nginx (web server which will be used to host our game on the browser) are used

RUN echo "daemon off;" >>/etc/nginx/nginx.conf

# cloning the file in the system itself
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master

# unzip and then deleting the folder
RUN cd /var/www/html/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip


# EXPOSE specifies the port to exposed for the docker container

EXPOSE 80

# starting my project using nginx
CMD ["/usr/sbin/nginx","-C","/etc/nginx/nginx.conf"]


# NOW USING THE TERMINAL WE WILL BE BUILDING THE DOKCER-IMAGE
# now "docker ps" will show
# CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES


# DockerImage commands
# before this open docker desktop
# docker build -t 2048-game .

# check image using -> docker images


# now making the docker container
# docker run -d -p 80:80 name/image-id
# now if you are getting a id then it means your conatiner have been created


# now you can check localhost:80

# docker build -t 2048-git . 
# docker images
# docker run -d -p 80:80 above id

-----------------------------------------------------
# now let's deploy it on and host it on cloud elastic Beanstalk aws

elastic Beanstalk is a service in aws which enable us to create application
on different platform like python, gojs, docker.

Now we will be using this to create our game.