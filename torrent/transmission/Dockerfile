FROM resin/rpi-raspbian:stretch

LABEL maintainer="Thiago Ortiz"

# Update packages and install software
RUN     apt-get update \
    &&  apt-get -y upgrade \
    &&  apt-get -y install transmission-daemon \
    &&  dir="/var/lib/transmission-daemon" \
    &&  file="$dir/info/settings.json" \
    &&  addgroup --uid 1000 transmission \
    #&&  adduser --uid 1000 transmission transmission\
    #&&  usermod -d $dir transmission \
    #&&  chown -Rh transmission. $dir \
    &&  echo '{' >$file \
    &&  echo '  "alt-speed-enabled": true,' >>$file \
    &&  echo '  "alt-speed-down": 50,' >>$file \
    &&  echo '  "alt-speed-time-enabled": false,' >>$file \
    &&  echo '  "alt-speed-time-begin": 540,' >>$file \
    &&  echo '  "alt-speed-time-day": 127,' >>$file \
    &&  echo '  "alt-speed-time-end": 1020,' >>$file \
    &&  echo '  "speed-limit-down": 1200,' >>$file \
    &&  echo '  "speed-limit-down-enabled": false,' >>$file \
    &&  echo '  "speed-limit-up": 50,' >>$file \
    &&  echo '  "speed-limit-up-enabled": false,' >>$file \
    &&  echo '  "upload-limit": 100,' >>$file \
    &&  echo '  "upload-limit-enabled": 0,' >>$file \
    &&  echo '  "alt-speed-up": 50,' >>$file \
    &&  echo '  "rpc-url": "/transmission/",' >>$file \
    &&  echo '  "rpc-whitelist": "127.0.0.1",' >>$file \
    &&  echo '  "rpc-whitelist-enabled": false,' >>$file \
    &&  echo '  "incomplete-dir-enabled": true,' >>$file \
    &&  echo '  "peer-port": 5141,' >>$file \
    &&  echo '  "port-forwarding-enabled": true,' >>$file \
    &&  echo '  "rpc-username": "ortiz",' >>$file \
    &&  echo '  "rpc-password": "{971437632e7bfb5a632210b4f8ccc4a8bd81b2d4164IQ8Jz",' >>$file \
    &&  echo '  "download-dir": "/media/homeflix/movies",' >>$file \
    &&  echo '  "incomplete-dir": "/media/homeflix/_torrents/_in_progress"' >>$file \
    &&  echo '}' >>$file


RUN service transmission-daemon start

COPY transmission.sh /usr/bin/transmission.sh
RUN chmod 777 /usr/bin/transmission.sh

HEALTHCHECK --interval=60s --timeout=15s \
            CMD netstat -lntp | grep -q '0\.0\.0\.0:9091'

EXPOSE 9091 5141/tcp 5141/udp

ENTRYPOINT [ "/usr/bin/transmission.sh" ]
