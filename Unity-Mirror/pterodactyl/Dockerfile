FROM ubuntu:lunar-slim
LABEL author="The Realm 18 Studios" maintainer="The Realm 18 Studios <docker@therealm18studios.com>"

RUN /bin/sh -c
 apt update &&
 apt upgrade -y &&
 apt update -y &&
 apt install -y curl ca-certificates openssl git tar fontconfig tzdata iproute2 apt-transport-https &&
 dpkg --add-architecture i386 &&
 apt update && apt upgrade -y &&
 apt install libc6:i386 libncurses5:i386 libstdc++6:i386 -y &&
 apt install libsqlite3-0:i386 -y &&
 useradd -d /home/container -m container &&
 rm -rf /usr/bin/fallocate &&
 apt install clean -y
 
USER container
ENV user=container home=/home/container
WORKDIR /home/container
COPY ./entrypoint.sh /

CMD [ "/bin/bash", "/entrypoint.sh" ]