FROM prairielearn/workspace-jupyterlab-r:a64f8e8b8cd2fa0273f61a7aa5bbdef3cf682503

USER root

# Install R packages
COPY conda-linux-64.lock /tmp/conda-linux-64.lock

RUN mamba install --yes --file /tmp/conda-linux-64.lock && \
    mamba clean --all -f -y 

# Install CRAN packages
RUN Rscript -e "lib <- 'simputation'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}" 

RUN Rscript -e "lib <- 'cellWise'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}"

RUN Rscript -e "lib <- 'NHANES'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}"

USER ${NB_UID}
