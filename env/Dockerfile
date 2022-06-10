# reference: https://hub.docker.com/r/jupyter/minimal-notebook
# Dockerfile: https://github.com/jupyter/docker-stacks/blob/master/minimal-notebook/Dockerfile
FROM jupyter/minimal-notebook:2022-05-13

# need to specify root as in the minimal-notebook image the final
# USER command is non-root
USER root

LABEL maintainer="jackhjfission <jackhjfission@gmail.com>"

# set the environment variable and volume to share ssh keys
# set the image SSH_AUTH_SOCK to a specific file
ENV SSH_AUTH_SOCK=/ssh-agent/ssh
# make the necessary volume within the agent
VOLUME /ssh-agent

# install very minimal reqs
RUN apt-get update --fix-missing \ 
    && apt-get install -y \
        curl \
        git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install docker using their handy script
RUN curl -fsSL https://get.docker.com | sh

#Setup File System
ENV HOME=/home
ENV SHELL=/bin/bash

# # install requirements using mamba
# COPY ./requirements.yml /home/requirements.yml
# RUN mamba env update --file /home/requirements.yml --prune \
#     && rm -rf /home/requirements.yml

USER ${NB_UID}