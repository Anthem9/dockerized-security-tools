FROM ubuntu:18.04 

LABEL maintainer="Rory McCune <rorym@mccune.org.uk>"

COPY localtime /etc/localtime

#Avoid getting prompted during builds
ENV DEBIAN_FRONTEND=noninteractive

#Pre-requisites
RUN apt update -qq && \
    apt install -y ruby nodejs git gcc ruby-dev make libmysqlclient-dev libsqlite3-dev g++ tzdata && \
    rm -rf /var/lib/apt/lists/* && rm -rf /var/cache/apt/* 

#Clone the repo
RUN git clone --depth=1 https://github.com/dradis/dradis-ce.git && rm -rf /dradis-ce/.git/*

WORKDIR /dradis-ce

#Complains without the rake gem setup
RUN gem install rake

#Need to run setup twice, which needs doing for reasons unexplainable
RUN ruby bin/setup

#Bind to all interfaces explicitly as the default is localhost only
CMD ["bundle","exec","rails","server","-b","0.0.0.0"]
