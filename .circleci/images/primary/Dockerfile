FROM debian:buster-slim

#install and source
RUN set -ex && apt-get update && apt-get upgrade && apt-get install -y \
    # installing following libs into docker image
    ## Docker may need this apt-utils
    apt-utils \

    ## Following are requested by circleci
    bash \
    netcat \
    git \
    tar \
    gzip \
    ca-certificates \

    # Following are requested by story 4350
    libssh2-1 \
    ## This build-essential is for make
    build-essential \
    pkg-config \
    binutils \
    openssl \
    curl

# installing docker cli

## Update the apt package index and install packages to allow apt to use
## a repository over HTTPS:
RUN set -ex && apt-get update && apt-get upgrade && apt-get install -y \
    apt-transport-https \
    gnupg \
    lsb-release

## Add Docker’s official GPG key:
RUN set -ex && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | \
    gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

## set up the stable repository
RUN set -ex && \
    echo \
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

## install the latest version of Docker Engine and containerd
RUN set -ex && apt-get update && apt-get upgrade && apt-get install -y \
    docker-ce \
    docker-ce-cli\
    containerd.io

## Remove packages that allow apt to use a repository over HTTPS:
RUN set -ex && apt-get remove -y \
    apt-transport-https \
    gnupg \
    lsb-release

## Verify docker installation
RUN set -ex && \
    docker --version

# installing docker credential helper





RUN echo "Finished building docker!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"

