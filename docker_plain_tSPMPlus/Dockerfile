FROM rocker/rstudio:4.2.3

RUN apt-get update -qq &&\
    apt-get install -y\
    libssl-dev \
    libxml2-dev \
    libfontconfig1-dev\
    libharfbuzz-dev\
    libfribidi-dev\
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    libglpk40&&\
    rm -rf /var/lib/apt/lists/*

RUN Rscript -e "install.packages('devtools', repos='https://cran.rstudio.com', clean = TRUE)"

RUN Rscript -e "install.packages('Rcpp', repos='https://cran.rstudio.com', clean = TRUE)" &&\
    Rscript -e "install.packages('RcppParallel', repos='https://cran.rstudio.com', clean = TRUE)"

RUN Rscript -e "require(devtools); devtools::install_github('clai-group/mlho'); install.packages('pacman', clean = TRUE); pacman::p_load(magrittr,rf,igraph, data.table, devtools, backports, Hmisc, tidyr,dplyr,ggplot2,plyr,scales,readr, httr, DT, lubridate, tidyverse,reshape2,foreach,doParallel,caret,gbm,lubridate,praznik, epitools, memuse, utils, MatchIt,profmem,tictoc,microbenchmark)"

RUN  mkdir -p /home/rstudio/data/ /home/rstudio/output /home/rstudio/vignettes
RUN git clone https://github.com/JonasHuegel/tSPMPlus_R.git &&\
    cp tSPMPlus_R/vignettes/* /home/rstudio/vignettes/ &&\
    rm -rf tSPMPlus_R   

RUN Rscript -e "devtools::install_github('jonashuegel/tSPMPlus_R')" 

RUN echo "setwd('/home/rstudio')" >> /home/rstudio/.Rprofile

RUN chown -R rstudio:rstudio /home/rstudio/ 

LABEL org.opencontainers.image.source=https://github.com/JonasHuegel/tSPMPlusDocker
LABEL org.opencontainers.image.description="Docker container providng an rstudio instance with an preinstalled tSPM+ and MLHO. The container is based on the rocker/rstudio container (https://rocker-project.org/)."
LABEL org.opencontainers.image.licenses=GPLv3