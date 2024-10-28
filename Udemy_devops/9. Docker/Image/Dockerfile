FROM ubuntu:latest AS BUILD_IMAGE
RUN apt-get update && apt-get install -y apt-transport-https
RUN apt install wget unzip -y
RUN wget https://www.tooplate.com/zip-templates/2117_infinite_loop.zip
RUN unzip 2117_infinite_loop.zip && cd 2117_infinite_loop && tar -czf infinite.tgz * && mv infinite.tgz /root/infinite.tgz

FROM ubuntu:latest
LABEL "project" = "Marketing"
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install apache2 git wget -y
COPY --from=BUILD_IMAGE /root/infinite.tgz /var/www/html
RUN cd /var/www/html && tar xzf infinite.tgz
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
VOLUME /var/log/apache2
WORKDIR /var/www/html
EXPOSE  8090
