FROM ubuntu:lunar-slim
LABEL author="The Realm 18 Studios" maintainer="The Realm 18 Studios <docker@therealm18studios.com>"

RUN /bin/sh -c
 apt update &&
 apt upgrade -y &&
 apt update -y &&
 apt install -y curl ca-certificates openssl git tar fontconfig tzdata iproute2 apt-transport-https &&
 apt mariadb-server-core-10.5 mariadb-server-10.5 -y &&
 useradd -d /home/container -m container &&
 rm -rf /usr/bin/fallocate &&
 apt install clean -y
 
USER container
ENV user=container home=/home/container
WORKDIR /home/container
COPY ./entrypoint.sh /

CMD [ "/bin/bash", "/entrypoint.sh" ]