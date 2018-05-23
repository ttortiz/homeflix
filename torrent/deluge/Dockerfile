FROM resin/rpi-raspbian:stretch

LABEL maintainer="Rafael Bubach"

# mapeamento de volume dos dados
ARG DIR="$(pwd)"

# Update packages and install software
RUN echo 'deb http://ftp.br.debian.org/debian sid main' >> /etc/apt/sources.list
RUN gpg --keyserver pgpkeys.mit.edu --recv-key 8B48AD6246925553
RUN gpg -a --export 8B48AD6246925553 | sudo apt-key add -
RUN apt-get update
RUN apt-get -y install apt-utils 
RUN apt-get -y upgrade
RUN apt-get install --only-upgrade python-libtorrent
RUN apt-get -y install python-mako deluged deluge-web

VOLUME [DIR, "/root/external"]

COPY web.config/ /root/.config/deluge/
ADD startdeluge /usr/local/bin/startdeluge
RUN chmod 755 /usr/local/bin/startdeluge

CMD ["/usr/local/bin/startdeluge"]

HEALTHCHECK --interval=60s --timeout=15s \
    CMD netstat -lntp | grep -q '0\.0\.0\.0:8112'

EXPOSE 8112

ENTRYPOINT [ "/bin/bash" ]


# build with: sudo docker build -t deluge .
# for iterative mode:
#   run with: sudo docker run -it -p 8112:8112 deluge
# for detached mode:
#   run with: sudo docker run --name deluge -d -p 8112:8112 deluge

# Torrent Directories
#   /root/external/inprogress
#   /root/external/completed
#   /root/external/.torrents
#   /root/external/.listening