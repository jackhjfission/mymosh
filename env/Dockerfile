# reference: https://hub.docker.com/_/ubuntu/
FROM ubuntu:20.04

LABEL maintainer="jackhjfission <jackhjfission@gmail.com>"

# Set environment variables
# this will allow some code I'm going to write to know where it is running
ENV CONTAINER_NAME=mymosh

# set the environment variable and volume to share ssh keys
# set the image SSH_AUTH_SOCK to a specific directory
ENV SSH_AUTH_SOCK=/ssh-agent/ssh
# make the necessary volume within the agent
VOLUME /ssh-agent

# set the timezone, otherwise the installer goes into interactive mode
ARG TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install minimal python3.9 reqs
RUN apt-get update --fix-missing \ 
    && apt-get install -y \
        git \
        python3.9 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#Setup File System
ENV HOME=/home
ENV SHELL=/bin/bash
RUN mkdir /home/repo
VOLUME /home/repo
WORKDIR /home/repo
