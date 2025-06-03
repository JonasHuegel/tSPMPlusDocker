# transitve Sequential Pattern Mining Plus (tSPM+) docker container
The dockerbuild file fot the tSPM+ R-package. The image is bases on rocker:rstudio. For a more detailed information regarding start options check the original [documentation](https://hub.docker.com/r/rocker/rstudio). There are two different versions of the docker container, a larger one containing the benchmark scripts and synthetic data, as well a lightweight one, which does not cointains then benchmark scripts and data. The benchmark scripts are in the folder `/home/rstudio/benchmark` and the sythnetic data for the benchmark is in the `/home/rstudio/data` directory. The two example uses cases provided in both variants are presented in the `/home/rstudio/vignette` folder.


## Build with:
Replace the tag with the current date or corresponding tag.

`TAG=2023-09-05`

`docker build -t "ghcr.io/jonashuegel/tspmplusdocker:${TAG}" . `


## Run with
If you build it on your own make sure that the tag matches, when pulling from the Github container registry get the corresponding tag from the packages [page](https://github.com/JonasHuegel/tSPMPlusDocker/pkgs/container/tspmplusdocker). Then run the following command replacing everything in `<>` with your own values:
`docker run  -ti -e DISABLE_AUTH=true -e PASSWORD=<YOUR_PASS> -e RSTUDIO_WHICH_R=/usr/local/bin/R  -p 127.0.0.1:8787:8787  -v .<path/to/data>:/home/rstudio/data -v <path/to/output>:/home/rstudio/output ghcr.io/jonashuegel/tspmplusdocker:${TAG}`


## Citation
Please cite our publication when using the package or docker container: Hügel, J., Sax, U., Murphy, S. N. & Estiri, H. tSPM+; a high-performance algorithm for mining transitive sequential patterns from clinical data. arXiv [cs.LG] (2023) doi:10.48550/arXiv.2309.05671
