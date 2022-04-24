FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
#下载所需包
ENV PACKAGES git gcc make g++ libboost-all-dev liblzma-dev libbz2-dev \
    ca-certificates zlib1g-dev libcurl4-openssl-dev curl unzip autoconf \
    apt-transport-https ca-certificates gnupg software-properties-common \
    wget openjdk-11-jre openjdk-11-jre-headless curl unzip python3-pip pigz

ARG VERSION=current
ENV PATH=/usr/local/ncbi/sra-tools/bin:${PATH}
RUN mkdir -p /root/.ncbi && \



#install fastqc
ENV FASTQC_VERSION 0.11.9
WORKDIR /usr/local
RUN apt-get update && \
    apt remove -y libcurl4 && \
RUN apt-get update
RUN unzip fastqc_v${FASTQC_VERSION}.zip
WORKDIR /usr/local/FastQC
RUN chmod 755 ./fastqc
RUN ln -s /usr/local/FastQC/fastqc /usr/local/bin/fastqc

ENV PATH /usr/local/FastQC/:${PATH}
ENV LD_LIBRARY_PATH "/usr/local/lib:${LD_LIBRARY_PATH}"


# Install cutadapt
ENV CUTADAPT_VERSION 3.3
RUN pip3 install cutadapt==${CUTADAPT_VERSION}

# Install trim_galore
WORKDIR /usr/local
ENV TRIM_GALORE_VERSION 0.6.7

RUN curl -fsSL https://github.com/FelixKrueger/TrimGalore/archive/${TRIM_GALORE_VERSION}.tar.gz -o trim_galore.tar.gz
RUN tar xvzf trim_galore.tar.gz

ENV PATH /usr/local/TrimGalore-${TRIM_GALORE_VERSION}/:${PATH}
ENV LD_LIBRARY_PATH "/usr/local/lib:${LD_LIBRARY_PATH}"

RUN echo "export PATH=$PATH" > /etc/environment
RUN echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH" > /etc/environment
# install fastx-toolkit
RUN apt update && apt install -y wget python3 python3-pip

RUN mkdir /usr/local/fastx-toolkit && cd /usr/local/fastx-toolkit && \
wget --quiet http://hannonlab.cshl.edu/fastx_toolkit/fastx_toolkit_0.0.13_binaries_Linux_2.6_amd64.tar.bz2 && \
tar xvf fastx_toolkit_0.0.13_binaries_Linux_2.6_amd64.tar.bz2 && \
mv bin/* /usr/local/bin/

