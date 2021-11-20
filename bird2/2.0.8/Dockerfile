FROM ubuntu:20.04 AS builder

ARG BIRD_VERSION=2.0.8

MAINTAINER Florian Fuessl <flo@degnet.de>

EXPOSE 179

RUN apt update && apt upgrade && apt install -y \
        autoconf \
	bison \
	build-essential \
	curl \
	flex \
	libreadline-dev \
	libncurses5-dev \
	m4 \
	unzip \
	git \
	libssh-dev

WORKDIR /build
RUN curl -O -L https://bird.network.cz/download/bird-$BIRD_VERSION.tar.gz
RUN tar -zxvf bird-$BIRD_VERSION.tar.gz

RUN cd bird-2.0.8 && \
        autoconf && \
        autoheader && \
        ./configure --localstatedir=/var --sysconfdir /etc/bird && \
        make && \
        make install


FROM ubuntu:20.04

RUN apt update && apt upgrade && apt install -y --no-install-recommends \
	libreadline8 \
	libssh-4 \
	lsb-base \
	ucf

RUN mkdir /bird
VOLUME ["/bird"]
# Hint: mount your configuration volume to :/bird:rw
#       bird daemon will use /bird/bird.conf as default configuration file

COPY --from=builder /usr/local/sbin/bird* /usr/local/sbin/
COPY --from=builder /etc/bird/bird.conf /bird/bird.default.conf

# expose port(s)
EXPOSE 179
# run baby run
CMD bird -c /bird/bird.conf -d

