FROM ubuntu:22.04

ARG HOME=/home/user
ARG USER=devuser
ARG GROUP=devgroup
ARG ARG_UID=1000
ARG ARG_GID=1000

ARG DEBIAN_FRONTEND=noninteractive

ENV UID=${ARG_UID}
ENV GID=${ARG_GID}
ENV SHELL=/bin/bash

# Installing basic tools
RUN apt update && apt upgrade -y && \
    apt install -y \
    build-essential \
    gdb \
    git \
    nano \
    vim \
    bash \
    bash-completion \
    locales \
    && apt clean

# Future commands are run via bash (instead of sh)
SHELL ["/bin/bash", "-c"]

# Create locales
RUN sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && locale-gen

# Create a group and user
RUN addgroup --gid ${GID} ${GROUP} && \
    useradd -r -l -u ${UID} -g ${GID} -m -d ${HOME} -s /bin/bash ${USER} && \
    chown -R ${USER}:${GROUP} ${HOME}

USER ${USER}

# Enable proper rendering of unicode
RUN git config --global core.quotePath false

# Create folders
RUN mkdir -p ${HOME}/workspace

# Setting workspace
WORKDIR ${HOME}/workspace