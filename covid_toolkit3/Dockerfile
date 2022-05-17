FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai

#设置环境package 为所需依赖包
ENV PACKAGES python curl bzip2 wget make gcc zlib1g zlib1g-dev libnss-sss \
    openjdk-8-jre curl less vim

# install minimap2
WORKDIR /usr/local
ENV MINIMAP2_VERSION 2.24
RUN apt-get update && apt-get install -y --no-install-recommends ${PACKAGES} && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /usr/local/minimap2 && cd /usr/local/minimap2  \
    && wget --no-check-certificate https://github.com/lh3/minimap2/releases/download/v${MINIMAP2_VERSION}/minimap2-${MINIMAP2_VERSION}.tar.bz2 \
    && tar -xjvf minimap2-${MINIMAP2_VERSION}.tar.bz2 \
    && cd minimap2-2.24 \
    && make \
    && mv  minimap2 /usr/local/bin
ENV PATH=/usr/local/minimap2-${MINIMAP2_VERSION}_x64-linux:${PATH}

#samtools
WORKDIR /usr/local
RUN apt-get update && apt-get install -y samtools \
    && apt-get clean

# vcftools
WORKDIR /usr/local
RUN apt-get update && apt-get install -y vcftools


# picard
WORKDIR /usr/local
RUN apt-get update && apt-get install -y --no-install-recommends wget openjdk-8-jre \
    && cd /usr/local \
    && wget https://github.com/broadinstitute/picard/releases/download/2.27.0/picard.jar \
  # && chmod +x /usr/local/picard \
    && apt-get remove -y wget \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /pasteur

# IGV

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime &  echo $TZ > /etc/timezone  && apt-get -y update
WORKDIR /usr/local
RUN apt-get -y dist-upgrade && \
 apt-get -y install --no-install-recommends --no-install-suggests build-essential wget unzip openjdk-8-jdk && \
 apt-get -y autoremove && apt-get clean
RUN rm -rf /var/lib/apt/lists/*
WORKDIR /usr/local
RUN wget https://data.broadinstitute.org/igv/projects/downloads/2.4/IGV_2.4.14.zip && \
 unzip IGV_2.4.14.zip && \
 cd IGV_2.4.14 && \
 chmod +x *.sh

ENV PATH=/usr/local/IGV_2.4.14/:$PATH
