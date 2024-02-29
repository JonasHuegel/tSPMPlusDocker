# transitve Sequential Pattern Mining Plus (tSPM+) docker container
 The dockerbuild file fot the tSPM+ R-package. The image is bases on rocker:rstudio. For a more detailed information regarding start options check the original [documentation](https://hub.docker.com/r/rocker/rstudio). The benchmark scripts are in the folder `/home/rstudio/benchmark`. The sythnetic data for the benchmark is in the `/home/rstudio/data` directory. Two example uses cases are presented in the `/home/rstudio/vignette folder`.


## Build with:
Replace the tag with the current date.

``TAG=2023-09-05
docker build -t "tspmplus:${TAG}" . ``


## Run with
`docker run --rm -ti -e DISABLE_AUTH=true -e PASSWORD=<YOUR_PASS> -e RSTUDIO_WHICH_R=/usr/local/bin/R  -p 127.0.0.1:8787:8787  -v .<path/to/data>:/home/rstudio/data -v <path/to/output>:/home/rstudio/output ghcr.io/jonashuegel/tspmplusdocker:2024-02-29`


