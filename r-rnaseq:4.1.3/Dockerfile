FROM r-base:4.1.3
MAINTAINER Qiushujing<qiushujing1@gmail.com>

RUN sed -i 's#http://archive.ubuntu.com/#http://mirrors.tuna.tsinghua.edu.cn/#' /etc/apt/sources.list;

RUN apt-get update && apt-get install -y fontconfig

RUN apt-get install -y libxml2-dev  libcurl4-openssl-dev libssl-dev openssl --fix-missing

RUN Rscript -e 'install.packages("tidyverse", repos = "http://mirrors.aliyun.com/CRAN/",dependencies = TRUE)'

RUN Rscript -e 'install.packages("ggrepel", repos = "http://mirrors.aliyun.com/CRAN/",dependencies = TRUE)'

RUN Rscript -e 'install.packages("circlize",repos = "http://mirrors.aliyun.com/CRAN/", dependencies = TRUE)'

RUN Rscript -e 'install.packages("openxlsx",repos = "http://mirrors.aliyun.com/CRAN/", dependencies = TRUE)'


RUN Rscript -e 'if (!requireNamespace("BiocManager", quietly = TRUE))install.packages("BiocManager")' \
&& Rscript -e 'BiocManager::install(c("limma","edgeR","DESeq2","ComplexHeatmap",""))'
