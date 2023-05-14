1. FROM ubuntu:22.04

It is a dockerfile instruction that specifies the base image for buildiung a "new Docker image" where base image is ubuntu version 22.04

A Docker image is a lightweight standalone and executable package which contain all necessary dependencies, libraries and code to BUILD, PACKAGE, DEPLOY, RUN an application
Here, ubuntu 22.04 is a base operating system


2. RUN apt-get update
This will update package list for a linux operating system using Advanced Package Tool (APT). This actually do not install/upgrade package instead it ensure that it should be having latest information about the available package.

3. RUN apt-get install -y nginx zip curl
It install three s/w packages (nginx, zip, curl) on linux operating system.
Not directly running but instead "Docker" makes a containerized Linux environment that can run Linux command and application.

Nginx used to server static and dynamic content over https and http protocols.
Zip is tool used to compress and decompress file and directories.
Curl is cmd tool for tranfering data to and from server using protocols (http, ftp, smtp-simple mail tranfer protocol)

"-y" used to answer any propt required in between installation to say "yes"


4. RUN echo "daemon off;" >>/etc/nginx/nginx.conf

"/etc/nginx/nginx.conf" is the confirguration file for "nginx" web server software which is installed in docker container.

"daemon off;"  tells to run the Nginx in foreground (means interacted by used i.e., single process) which is important otherwise it will be having confict with containers design.


5. RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master

SO this downloads .zip file containing source code of 2048 game (here) and saves it to "/var/www/html" directory as docker-container is having own file system inwhich nginx is running rightnow. By saving this now nginx web server would be able to get the dynamic content.

Curl is cmd tool for tranfering data to and from server using protocols (http, ftp, smtp-simple mail tranfer protocol) and HERE USED FOR DOWNLOADING.

"-o" specifies output file name and path fro downloaded file

"/var/www/html/master.zip" is the path and filename where downloaded file have been saved.

'L' option says to follow the url suppose 'L' is not their and url have redirected to some other url then it will stop their so it is good to use "-L" use


now as code is now in our container so we will be doing operation on that code.

6. RUN cd /var/www/html && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

NOTE: multiple instruction are using "&&"

"cd /var/www/html/" will move our working directory to "/var/www/html/" where our code from github is residing.

"unzip master.zip" it will extract the contents of "master.zip" file which was downloaded earlier using "curl" command

"mv 2048-master/*" is moving all files and directories with in "2048-master/" to up by one level to "/var/www/html"
one level up is shows by "."


"rm -rf 2048-master master.zip" now after moving all content to one level up so we are removing the master.zip file from "/var/www/html/".


7. EXPOSE 80
By default Docker container run in a isolated environment and network ports are not exposed to host machine so we are using EXPOSE to listen to port 80 which is also a default port of nginx web server.


8. CMD ["/usr/sbin/nginx","-c","/etc/nginx/nginx.conf"]

It is a default docker command used to launch a docker container.
CMD is default set command to run the container when it is started where command should be an array of strings.

'/usr/sbin/nginx -c /etc/nginx/nginx.conf' is command launches nginx web server which is located at "/etc/nginx/nginx.conf"




-----------------------------------
docker run -d -p 80:80 image-id


Now after docker container launch we will create docker image

1. "docker build -t image-name ." 
This will be used to build docker image using docker file located at "."

"docker build" used to create new docker image.
"-t" to specify name/TITLE

"." this specify the context having dockerfile and any other file needed for creating docker image



2. docker images
now it will list all the image currently available in the local system.
Docker image stored in local registry but can be shared to remote using docker hub or amazon ecr.

output will show "repository name, tag, image ID, and size"


3. docker run -d -p 80:80 image-id
"docker run" used to create a new docker container from specified docker image.

"-d" to run in detached mode as it is lightweight and can be exceuted in background not like as "nginx" which run in foreground.

"-p 80:80" it indicate to connect host machine's port 80 to docker container port 80, required if docker container running in a server like "nginx"


"image-id" is the ID of the docker image that container will be created from.




-----------------
We can summarise this as-
dockerfile setps us a dokcer container with ubuntu operating system, install nginx web server and download the 2048 game from github.
it then extract aand set up the game in web server's root directly. Docker container is made to exposed at 80 which is default by nginx server.
Finally docker container is set up to run nginx web server in foreground when container is started.