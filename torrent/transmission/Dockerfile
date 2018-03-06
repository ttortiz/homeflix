FROM resin/rpi-raspbian:stretch

LABEL maintainer="Thiago Ortiz"

ARG DIR="/root/.config/transmission-daemon"
ARG FILE="$DIR/settings.json"

# Update packages and install software
RUN     apt-get update \
    &&  apt-get -y upgrade \
    &&  apt-get -y install transmission-daemon \
    &&  addgroup --uid 1000 transmission
    #&&  adduser --uid 1000 transmission transmission\
    #&&  usermod -d $dir transmission \
    #&&  chown -Rh transmission. $dir \

COPY settings.json $FILE

COPY transmission.sh /usr/bin/transmission.sh
RUN chmod 777 /usr/bin/transmission.sh


HEALTHCHECK --interval=60s --timeout=15s \
            CMD netstat -lntp | grep -q '0\.0\.0\.0:9091'

EXPOSE 9091 5141/tcp 5141/udp

ENTRYPOINT [ "/usr/bin/transmission.sh" ]
