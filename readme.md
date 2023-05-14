# Common command

FROM - use to specify base image which can be "pulled" from container like docker hub, ECR etc.

RUN - used to exceutes commands during the image building process like as in below
      RUN apt-get install -y nginx

EXPOSE - used to specify the port to be exposed for the "docker container"

CMD - It is used to exceute a command in a running container. There can be only one CMD, if mutiple CMD, then it only applies to the last one. It will be overridden from Docker CLI.

-------------------------------------------------------------------

# command used in terminal

docker build -t image-name . <br>
docker images <br>
docker run -d -p 80:80 image-id

# Check [this](https://github.com/Anshumanshukla46/docker-2048/blob/main/explanation.txt) file for code explanation and more.

