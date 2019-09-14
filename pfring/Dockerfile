FROM ubuntu
# FROM arm32v7/debian:stretch
MAINTAINER ntop.org

RUN apt-get update && \
    apt-get -y -q install sudo apt-utils

RUN apt-get -y -q install git wget lsb-release gnupg net-tools libterm-readline-gnu-perl apt-transport-https

RUN apt-get -y -q install build-essential kmod bison flex

# RUN echo 'deb http://oph.mdrjr.net/meveric all xu' >> /etc/apt/sources.list
# COPY etc/apt/sources.list.d /etc/apt/sources.list.d/

################### HACK ###################
# COPY lib/modules /lib/modules/
# RUN cd /lib/modules && tar xf 4.14.102-156.tar

# COPY usr/src /usr/src/
# RUN cd /usr/src && tar xf linux-4.14.102-156.tar
################### HACK ###################

# RUN apt-get upgrade -y -q

RUN mkdir -p /opt/PF_RING

RUN git clone --branch "dev" https://github.com/ntop/PF_RING.git /opt/PF_RING

RUN cd /opt/PF_RING/kernel; make && make install

RUN insmod /opt/PF_RING/kernel/pf_ring.ko

RUN cd /opt/PF_RING/userland; make

CMD ["insmod", "/opt/PF_RING/kernel/pf_ring.ko"]
