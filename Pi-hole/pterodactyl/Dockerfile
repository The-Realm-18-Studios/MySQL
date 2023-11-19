ARG PIHOLE_BASE
FROM "${PIHOLE_BASE:-pihole/docker-pi-hole-base:bullseye-slim}"

ARG PIHOLE_DOCKER_TAG
RUN echo "${PIHOLE_DOCKER_TAG}" > /pihole.docker.tag

COPY s6/debian-root /
COPY s6/service /usr/local/bin/service

RUN bash -ex install.sh 2>&1 && \
    rm -rf /var/cache/apt/archives /var/lib/apt/lists/*

ARG PHP_ERROR_LOG
ENV PHP_ERROR_LOG ./home/container/var/log/lighttpd/error-pihole.log

# Add PADD to the container, too.
ADD https://install.padd.sh /usr/local/bin/padd
RUN chmod +x /usr/local/bin/padd

RUN useradd -d /home/container -m container

COPY ./ /home/container/
WORKDIR /home/container/

USER container
ENV user=container home=/home/container

ENTRYPOINT [ "/home/container/s6-init" ]

# IPv6 disable flag for networks/devices that do not support it
ENV IPv6 True

EXPOSE 53 53/udp
EXPOSE 67/udp
EXPOSE 80

ENV S6_KEEP_ENV 1
ENV S6_BEHAVIOUR_IF_STAGE2_FAILS 2
ENV S6_CMD_WAIT_FOR_SERVICES_MAXTIME 0

ENV FTLCONF_LOCAL_IPV4 0.0.0.0
ENV FTL_CMD no-daemon
ENV DNSMASQ_USER pihole

ENV PATH /opt/pihole:${PATH}

HEALTHCHECK CMD dig +short +norecurse +retry=0 @127.0.0.1 pi.hole || exit 1

SHELL ["/bin/bash", "-c"]