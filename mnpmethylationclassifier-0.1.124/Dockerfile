FROM ubuntu:16.04

RUN apt-get update && \
apt-get install -y wget \
bzip2 \
unzip

RUN wget https://repo.continuum.io/miniconda/Miniconda3-4.3.31-Linux-x86_64.sh && \
    bash Miniconda3-4.3.31-Linux-x86_64.sh -b -p /conda && \
    rm -f Miniconda3-4.3.31-Linux-x86_64.sh
ENV PATH="/conda/bin:${PATH}"
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --add channels r
RUN conda install -c r -c conda-forge -c bioconda \
    conda=4.3.31 \
    r=3.5.1 \
    r-base=3.5.1 \
    r-devtools=1.13.6 \
    r-biocmanager=1.30.4 \
    r-randomforest=4.6_14 \
    r-glmnet=2.0_16 \
    r-ggplot2=3.0.0 \
    r-gridextra=2.3 \
    r-knitr=1.20 \
    r-rtsne=0.13 \
    r-pander=0.6.3 \
    r-plotly=4.8.0 \
    r-reshape2=1.4.3 \
    r-readxl=1.1.0 \
    r-dt=0.4 \
    r-scales=0.5.0 \
    r-rcolorbrewer=1.1_2 \
    r-ggfortify=0.4.6 \
    r-qdaptools=1.3.3 \
    r-gplots=3.0.1 \
    r-stringr=1.3.1 \
    r-rmarkdown=1.10 \
    bioconductor-limma=3.38.3 \
    bioconductor-methylaid=1.16.0 \
    bioconductor-lumi=2.34.0 \
    bioconductor-methylumi=2.28.0 \
    bioconductor-minfi=1.28.0 \
    bioconductor-illuminahumanmethylation450kmanifest=0.4.0 \
    bioconductor-illuminahumanmethylation450kanno.ilmn12.hg19=0.6.0 \
    bioconductor-illuminahumanmethylationepicanno.ilm10b2.hg19=0.6.0 \
    bioconductor-illuminahumanmethylationepicanno.ilm10b4.hg19=0.6.0 \
    bioconductor-illuminahumanmethylationepicmanifest=0.3.0 \
    bioconductor-dnacopy=1.56.0 \
    bioconductor-biocinstaller=1.32.1 \
    r-dplyr=0.7.6 \
    r-assertthat=0.2.0 \
    r-glue=1.3.0 \
    r-pkgconfig=2.0.1 \
    r-r6=2.2.2 \
    r-rcpp=0.12.18 \
    r-rlang=0.2.1 \
    r-tibble=1.4.2 \
    r-cli=1.0.0 \
    r-fansi=0.2.3 \
    r-pillar=1.3.0 \
    r-tidyselect=0.2.4 \
    r-purrr=0.2.5 \
    r-httr=1.3.1 \
    r-curl=3.2 \
    r-jsonlite=1.5 \
    r-mime=0.5 \
    r-openssl=1.0.2 \
    r-askpass=1.1 \
    r-sys=3.1 \
    r-readr=1.3.1 \
    r-clipr=0.4.1 \
    r-ade4=1.7_13 \
    r-mass=7.3_50 \
    r-bh=1.66.0_1 \
    r-data.table=1.11.4 \
    r-rcurl=1.95_4.11 \
    bioconductor-genomeinfodb=1.18.1



RUN echo 'BiocManager::install("conumee", version="3.8", update=FALSE)' | R --vanilla

# # https://github.com/r-lib/devtools/issues/1722
ENV TAR=/bin/tar
RUN echo 'library(devtools); install_github("mwsill/IlluminaHumanMethylationEPICmanifest",upgrade_dependencies=FALSE)' | R --vanilla
RUN echo 'library(devtools); install_github("mwsill/mgmtstp27",subdir="/trunk/Rpackage/mgmtstp27/",upgrade_dependencies=FALSE)' | R --vanilla

COPY mnp.v11b4_0.1.124.tar.gz /mnp.v11b4_0.1.124.tar.gz
RUN R CMD INSTALL mnp.v11b4_0.1.124.tar.gz
COPY mnpqc_0.1.0.tar.gz /mnpqc_0.1.0.tar.gz
RUN R CMD INSTALL mnpqc_0.1.0.tar.gz

RUN rm -f /mnp.v11b4_0.1.124.tar.gz
RUN rm -f /mnpqc_0.1.0.tar.gz


# wget https://bioconductor.org/packages/3.8/data/annotation/src/contrib/IlluminaHumanMethylation450kanno.ilmn12.hg19_0.6.0.tar.gz
# wget https://bioconductor.org/packages/3.8/data/annotation/src/contrib/IlluminaHumanMethylation450kmanifest_0.4.0.tar.gz
# wget https://bioconductor.org/packages/3.8/data/annotation/src/contrib/IlluminaHumanMethylationEPICmanifest_0.3.0.tar.gz
# wget https://bioconductor.org/packages/3.8/data/annotation/src/contrib/IlluminaHumanMethylationEPICanno.ilm10b2.hg19_0.6.0.tar.gz
# wget https://www.bioconductor.org/packages/3.8/bioc/src/contrib/conumee_1.16.0.tar.gz
# # https://bioconductor.org/packages/release/bioc/html/conumee.html
# # https://bioconductor.org/packages/3.7/bioc/html/conumee.html
# COPY source/IlluminaHumanMethylation450kmanifest_0.4.0.tar.gz /IlluminaHumanMethylation450kmanifest_0.4.0.tar.gz
# RUN R CMD INSTALL IlluminaHumanMethylation450kmanifest_0.4.0.tar.gz
# # RUN R CMD INSTALL IlluminaHumanMethylation450kanno.ilmn12.hg19_0.6.0.tar.gz
# RUN R CMD INSTALL IlluminaHumanMethylationEPICanno.ilm10b2.hg19_0.6.0.tar.gz
# RUN R CMD INSTALL IlluminaHumanMethylationEPICmanifest_0.3.0.tar.gz
