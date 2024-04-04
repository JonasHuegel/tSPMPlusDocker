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


#dpkg -s <packagename> | grep '^Version:'

RUN Rscript -e "install.packages('devtools', repos='https://cran.rstudio.com', clean = TRUE)"

RUN Rscript -e "install.packages('Rcpp', repos='https://cran.rstudio.com', clean = TRUE)" &&\
    Rscript -e "install.packages('RcppParallel', repos='https://cran.rstudio.com', clean = TRUE)"

RUN Rscript -e "require(devtools); devtools::install_github('hestiri/mlho'); install.packages('pacman', clean = TRUE); pacman::p_load(igraph, data.table, devtools, backports, Hmisc, tidyr,dplyr,ggplot2,plyr,scales,readr, httr, DT, lubridate, tidyverse,reshape2,foreach,doParallel,caret,gbm,lubridate,praznik, epitools, memuse, utils, MatchIt,profmem,tictoc,microbenchmark)"

RUN  mkdir -p /home/rstudio/data/ /home/rstudio/output /home/rstudio/vignettes
RUN git clone https://github.com/JonasHuegel/tSPMPlus_R.git &&\
    cp tSPMPlus_R/vignettes/* /home/rstudio/vignettes/ &&\
    rm -rf tSPMPlus_R   

RUN cd /home/rstudio/ &&\
    git clone https://github.com/JonasHuegel/tSPMPlus_benchmarks.git

RUN cd /home/rstudio/data &&\
    wget https://mitre.box.com/shared/static/wk3560f962ozlg7sd2oj1zxk73ayqvm0.zip


RUN cd /home/rstudio/data && ls && \
    unzip wk3560f962ozlg7sd2oj1zxk73ayqvm0.zip -d syntheticData/ &&\
    rm wk3560f962ozlg7sd2oj1zxk73ayqvm0.zip

RUN Rscript -e "devtools::install_github('jonashuegel/tSPMPlus_R', args='--recursive')" 


RUN echo "setwd('/home/rstudio')" >> /home/rstudio/.Rprofile

RUN chown -R rstudio:rstudio /home/rstudio/ 

LABEL org.opencontainers.image.source=https://github.com/JonasHuegel/tSPMPlusDocker
LABEL org.opencontainers.image.description="Docker container providng an rstudio instance with an preinstalled tSPM+ and MLHO and the synthetic patient data and benchmark scripts used in the publication. The container is based on the rocker/rstudio container (https://rocker-project.org/)."
LABEL org.opencontainers.image.licenses=GPLv3