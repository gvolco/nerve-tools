FROM ubuntu:14.04
MAINTAINER John Billings <billings@yelp.com>


# Need Python 3.6
RUN apt-get update && \
    apt-get install -y --no-install-recommends software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa

# Older versions of dh-virtualenv are buggy and don't.. work
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 88ADA4A042F8DD13 && \
    echo 'deb http://ppa.launchpad.net/dh-virtualenv/daily/ubuntu trusty main\ndeb-src http://ppa.launchpad.net/dh-virtualenv/daily/ubuntu trusty main' >> /etc/apt/sources.list
RUN apt-get update

RUN apt-get -y install \
    dpkg-dev \
    python3.6-dev \
    libffi-dev \
    libssl-dev \
    debhelper \
    libyaml-dev \
    libcurl4-openssl-dev \
    dh-virtualenv \
    build-essential \
    wget \
    gdebi-core \
    protobuf-compiler

RUN apt-get purge -y python-pip python-virtualenv && sudo easy_install pip
RUN pip install -U tox pip virtualenv

ADD location_types.json /nail/etc/services/
ADD location_mapping.json /nail/etc/services/

RUN cd /tmp && \
    wget http://mirrors.kernel.org/ubuntu/pool/universe/d/dh-virtualenv/dh-virtualenv_1.0-1_all.deb && \
    gdebi -n dh-virtualenv*.deb && \
    rm dh-virtualenv_*.deb

WORKDIR /work
