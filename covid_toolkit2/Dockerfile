FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai

#install STAR
FROM ubuntu:20.04
MAINTAINER Qiushujing<qiushujing1@gmail.com>
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai

#install STAR
ENV STAR_VERSION 2.7.10a
WORKDIR /usr/local
RUN set -ex

RUN apt-get update && \
    apt-get clean && \
    g++ --version && \
    cd /usr/local && \
    unzip ${STAR_VERSION}.zip && \
    cp STAR /usr/local/bin && \
    cd /usr/local && \
    'rm' -rf STAR-${STAR_VERSION}
ENV PATH /usr/local/bin:${PATH}

#install hisat2
#install STAR
ENV STAR_VERSION 2.7.10a
WORKDIR /usr/local
RUN set -ex

RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc g++ make  wget zlib1g-dev unzip && \
    apt-get clean && \
    g++ --version && \
    cd /usr/local && \
    wget --no-check-certificate https://github.com/alexdobin/STAR/archive/${STAR_VERSION}.zip && \
    unzip ${STAR_VERSION}.zip && \
    cd STAR-${STAR_VERSION}/source && \
    make STARstatic && \
    cp STAR /usr/local/bin && \
    cd /usr/local && \
    'rm' -rf STAR-${STAR_VERSION}
ENV PATH /usr/local/bin:${PATH}
RUN echo "export PATH=$PATH" > /etc/environment
RUN echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH" > /etc/environment

#install bowtie2
RUN apt-get update && apt-get install -y tzdata
    build-essential \
    wget \
    tar \
    unzip \
    bzip2 \
    cmake \
    zlib1g-dev  \
    bzip2 \
    libncurses5-dev \
    libhts-dev \
    libtbb-dev \
    autoconf

# Tool versions:
ENV BOWTIE2_VERSION 2.4.4
ENV SAMTOOLS_VERSION 1.13

#Install Bowtie2:
RUN cd /usr/local/ \
    && wget -O bowtie2.zip \
    https://github.com/BenLangmead/bowtie2/releases/download/v${BOWTIE2_VERSION}/bowtie2-${BOWTIE2_VERSION}-linux-x86_64.zip \
        && unzip bowtie2.zip \
        && rm bowtie2.zip \
        && mv bowtie2* bowtie2
ENV PATH="/usr/local/bowtie2/:${PATH}"

# Install samtools:
RUN cd /usr/local/ \
    && wget -O samtools.tar.bz2 \
    https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 \
        && tar -jxf samtools.tar.bz2 \
        && rm samtools.tar.bz2 \
        && mv samtools* samtools \
        && cd samtools \
        && autoheader \
        && autoconf -Wno-syntax \
        && ./configure \
        && make \
        && make install
ENV PATH="/usr/local/samtools/:${PATH}"

# install subread
ENV SUBREAD_VERSION 2.0.2
RUN DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
 build-essential \
 gcc-multilib \
 apt-utils \
 wget

WORKDIR /usr/local
RUN wget https://sourceforge.net/projects/subread/files/subread-${SUBREAD_VERSION}/subread-${SUBREAD_VERSION}-Linux-x86_64.tar.gz
RUN tar xvzf subread-${SUBREAD_VERSION}-Linux-x86_64.tar.gz
RUN rm subread-${SUBREAD_VERSION}-Linux-x86_64.tar.gz
RUN ln -sf /usr/local/subread-${SUBREAD_VERSION}-Linux-x86_64/bin/* /usr/local/bin
