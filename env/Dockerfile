# reference: https://hub.docker.com/r/jupyter/minimal-notebook
FROM jupyter/minimal-notebook:2022-05-13

LABEL maintainer="jackhjfission <jackhjfission@gmail.com>"

# set the environment variable and volume to share ssh keys
# set the image SSH_AUTH_SOCK to a specific file
ENV SSH_AUTH_SOCK=/ssh-agent/ssh
# make the necessary volume within the agent
VOLUME /ssh-agent

# set the timezone, otherwise the installer goes into interactive mode
ARG TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# install very minimal reqs
RUN apt-get update --fix-missing \ 
    && apt-get install -y \
        curl \
        git \
        wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install docker using their handy script
RUN curl -fsSL https://get.docker.com | sh

#Setup File System
ENV HOME=/home
ENV SHELL=/bin/bash
RUN mkdir /home/repo
VOLUME /home/repo
WORKDIR /home/repo

# install miniconda python distribution
COPY ./miniconda-install /home/miniconda-install
COPY ./requirements.yml /home/requirements.yml
RUN chmod +x ~/miniconda-install \
    && ~/miniconda-install \
    && rm -rf ~/miniconda-install \
    && /miniconda3/bin/conda env update --file /home/requirements.yml --prune \
    && rm -rf /home/requirements.yml
