FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
#设置环境package 为所需依赖包
ENV PACKAGES python curl bzip2 wget make gcc zlib1g zlib1g-dev libnss-sss \
# install minimap2
WORKDIR /usr/local
ENV MINIMAP2_VERSION 2.24
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /usr/local/minimap2 && cd /usr/local/minimap2  \
    && tar -xjvf minimap2-${MINIMAP2_VERSION}.tar.bz2 \
    && mv  minimap2 /usr/local/bin
ENV PATH=/usr/local/minimap2-${MINIMAP2_VERSION}_x64-linux:${PATH}

#install picard
RUN apt-get update -y && apt-get install -y ${PACKAGES} \
    && apt-get clean
RUN mkdir -p /usr/local/picard \
FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
#设置环境package 为所需依赖包
ENV PACKAGES python curl bzip2 wget make gcc zlib1g zlib1g-dev libnss-sss \
# install minimap2
WORKDIR /usr/local
ENV MINIMAP2_VERSION 2.24
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /usr/local/minimap2 && cd /usr/local/minimap2  \
    && tar -xjvf minimap2-${MINIMAP2_VERSION}.tar.bz2 \
    && mv  minimap2 /usr/local/bin
ENV PATH=/usr/local/minimap2-${MINIMAP2_VERSION}_x64-linux:${PATH}

#install picard
RUN apt-get update -y && apt-get install -y ${PACKAGES} \
    && apt-get clean
RUN mkdir -p /usr/local/picard \
> /usr/local/picard/picard.jar

#install samtools
WORKDIR /usr/local
RUN apt-get update -y && apt-get install -y samtools \
    && apt-get clean

#install IGV
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime &  echo $TZ > /etc/timezone  && apt-get -y update
RUN apt-get -y dist-upgrade
RUN apt-get -y install --no-install-recommends --no-install-suggests build-essential wget unzip openjdk-11-jdk
RUN apt-get -y autoremove
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
WORKDIR /usr/local
RUN wget https://data.broadinstitute.org/igv/projects/downloads/2.11/IGV_2.11.9.zip
RUN unzip IGV_2.11.9.zip
RUN cd IGV_2.11.9
ENV PATH=/usr/local/IGV_2.11.9/:$PATH

#install vcftools
RUN apt-get update && apt-get install -y vcftools
