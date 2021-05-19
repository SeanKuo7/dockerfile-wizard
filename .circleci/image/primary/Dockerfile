FROM golang:1.8.0

#install and source
RUN set -ex                                                         && \
    apt-get update && apt-get dist-upgrade -y && apt-get upgrade -y && \
    apt-get install -y \
    bash \
    netcat \
    git \
    tar \
    gzip \
    ca-certificaties \
    # aboves are requested by circleci
    libssh2345

RUN set -ex                                                         && \
    apt-get update && apt-get dist-upgrade -y && apt-get upgrade -y && \
    apt-get install -y \
    purge \
    docker-ce \
    docker-ce-cli \
    containerd.io \
    # build-essential is for make
    build-essential \
    pkg-config \
    binutils \
    openssl \
    curl




RUN go get github.com/jstemmer/go-junit-report

RUN echo "Finished building docker!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!"

