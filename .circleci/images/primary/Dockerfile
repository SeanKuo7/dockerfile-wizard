FROM debian:buster-slim
ARG DOCKER_CREDENTIAL_HELPER_VERSION=0.6.3

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

## Set up the stable repository
RUN set -ex && \
    echo \
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

## Install the latest version of Docker Engine and containerd
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
RUN set -ex && docker --version

# Installing docker credential helper
RUN set -ex && apt-get update && apt-get upgrade && apt-get install -y \
    wget

RUN set -ex && echo $PATH && \
    cd /usr/local/bin && \
    wget https://github.com/docker/docker-credential-helpers/releases/download/v${DOCKER_CREDENTIAL_HELPER_VERSION}/docker-credential-pass-v${DOCKER_CREDENTIAL_HELPER_VERSION}-amd64.tar.gz && \
    tar -xvf docker-credential-pass-v${DOCKER_CREDENTIAL_HELPER_VERSION}-amd64.tar.gz && \
    chmod +x docker-credential-pass && \
    chown root:root /usr/local/bin/docker-credential-pass && \
    rm docker-credential-pass-v${DOCKER_CREDENTIAL_HELPER_VERSION}-amd64.tar.gz

## Clean up tools
RUN set -ex && apt-get remove -y wget

## Verify docker credential helper installation
RUN set -ex && /usr/local/bin/docker-credential-pass version

## Cleanup
RUN apt-get -y --purge autoremove

RUN echo "Finished building docker!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"

