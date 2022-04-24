FROM r-base:4.1.3
MAINTAINER Qiushujing<qiushujing1@gmail.com>

RUN Rscript -e "install.packages('tidyverse')"

RUN Rscript -e "install.packages('ggrepel')"

RUN Rscript -e "install.packages('circlize')"

RUN Rscript -e "install.packages('openxlsx', dependencies = TRUE)"


RUN Rscript -e 'if (!requireNamespace("BiocManager", quietly = TRUE))install.packages("BiocManager")' \
&& Rscript -e 'BiocManager::install(c("limma","edgeR","DESeq2","ComplexHeatmap",""))'
