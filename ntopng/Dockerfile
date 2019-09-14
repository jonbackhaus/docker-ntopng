FROM debian:9
MAINTAINER ntop.org

RUN apt-get update && \
    apt-get -y -q install sudo apt-utils

RUN apt-get update && \
    apt-get -y -q install curl lsb-release gnupg net-tools libterm-readline-gnu-perl netcat

RUN curl -L http://packages.ntop.org/apt/ntop.key | apt-key add -

RUN echo "deb http://apt.ntop.org/stretch_pi armhf/" > /etc/apt/sources.list.d/ntop.list && \
    echo "deb http://apt.ntop.org/stretch_pi all/" >> /etc/apt/sources.list.d/ntop.list

RUN apt-get update && \
    apt-get -y install ntopng

RUN chown -R ntopng:ntopng /var/lib/ntopng

RUN echo '#!/bin/bash\n/etc/init.d/redis-server start\nntopng "$@"' > /run.sh && \
    chmod +x /run.sh

EXPOSE 3000

ENTRYPOINT ["/run.sh"]
