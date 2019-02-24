## a blueprint for a dev environment using docker

FROM ubuntu:18.04
MAINTAINER “Hugues Talbot” hugues.talbot @ gmail.com

RUN apt-get update
RUN apt-get install locales

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Install dependencies
ENV DEBIAN_FRONTEND noninteractive

# Do not exclude man pages & other documentation
RUN rm /etc/dpkg/dpkg.cfg.d/excludes

# Reinstall all currently installed packages in order to get the man pages back
RUN apt-get update && \
    dpkg -l | grep ^ii | cut -d' ' -f3 | xargs apt-get install -y --reinstall && \
    rm -r /var/lib/apt/lists/*

RUN apt-get install -qq wget unzip build-essential cmake gcc libcunit1-dev libudev-dev
RUN apt-get install -qq sudo gnome-terminal tmux

# Fix disability access
RUN dbus-uuidgen > /var/lib/dbus/machine-id

# Add user and set password
ARG USERNAME=isbs
ARG PASSWORD=ISBS
ARG LOGINSHELL=/bin/bash
RUN adduser --disabled-password --gecos "" --shell $LOGINSHELL $USERNAME
RUN echo "$USERNAME:$PASSWORD" | chpasswd

# Give super-user permissions to user
RUN echo "$USERNAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Here is he list of packages to install that depend on the application
RUN apt-get install -qq less
RUN apt-get install -qq python3 python3-pip python3-ipython python3-notebook python3-nbconvert python3-matplotlib
RUN apt-get install -qq python3-sklearn python3-skimage python3-skimage-lib python3-sklearn-lib
RUN apt-get install -qq texlive-base texlive-latex-base texlive-latex-recommended texlive-science
RUN apt-get install -qq emacs vim

## This is to compile Pink, major endeavour