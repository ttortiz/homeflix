FROM lsiobase/mono.armhf

LABEL maintainer="Thiago Ortiz"

# set environment variables
ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_CONFIG_HOME="/config/xdg"

RUN \
 apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA5DFFC && \
 echo "deb http://apt.sonarr.tv/ master main" > /etc/apt/sources.list.d/sonarr.list && \
 apt-get update && \
 apt-get install -y nzbdrone && \
 apt-get clean && \
 rm -rf /tmp/* \
 rm -rf /var/lib/apt/lists/* \
 rm -rf /var/tmp/*

# add local files
#COPY root/ /

COPY sonarr.sh /usr/bin/sonarr.sh
RUN chmod 777 /usr/bin/sonarr.sh

HEALTHCHECK --interval=60s --timeout=15s \
            CMD netstat -lntp | grep -q '0\.0\.0\.0:8989'

EXPOSE 8989

VOLUME /config /downloads /tv

CMD ["tail", "-f", "/dev/stdout"]
#CMD ["mono", "--debug", "/opt/NzbDrone/NzbDrone.exe"]
#ENTRYPOINT [ "/usr/bin/sonarr.sh" ]

