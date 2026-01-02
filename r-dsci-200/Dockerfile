# Copyright (c) UBC-DSCI Development Team.
# Distributed under the terms of the Modified BSD License.
FROM quay.io/jupyter/minimal-notebook:python-3.12

USER root

# R pre-requisites
RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    fonts-dejavu \
    unixodbc \
    unixodbc-dev \
    vim \
    libgsl27 \
    libgsl-dev \
    libgl1 \
    build-essential \
    r-cran-rodbc \
    gfortran \
    gcc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN rm -rf "/home/${NB_USER}/.cache/"

USER ${NB_UID}

WORKDIR "${HOME}/work"

# Install R packages
COPY conda-linux-64.lock /tmp/conda-linux-64.lock

# R packages including IRKernel which gets installed globally.
# r-e1071: dependency of the caret R package
RUN mamba install --yes --file /tmp/conda-linux-64.lock && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}" && \
    Rscript -e "devtools::install_github('diverse-data-hub/diversedata')"

RUN Rscript -e "lib <- 'simputation'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}" 

RUN Rscript -e "lib <- 'cellWise'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}"

RUN Rscript -e "lib <- 'NHANES'; install.packages(lib, repos='http://cran.us.r-project.org'); if ( ! library(lib,character.only=TRUE,logical.return=TRUE)){quit(status=1,save='no')}"

# disable warnings that pollute build logs; seems to be related to the update to python 3.11
# https://discourse.jupyter.org/t/debugger-warning-it-seems-that-frozen-modules-are-being-used-python-3-11-0/16544/12
ENV PYDEVD_DISABLE_FILE_VALIDATION=1

# Disable the cell toolbar (which ignores metadata and students often accidentally click + delete grading cells)
RUN jupyter labextension disable "@jupyterlab/cell-toolbar-extension"

# Disable announcement pop-up on start
RUN jupyter labextension disable "@jupyterlab/apputils-extension:announcements"

# Install the extension to remove the shift+M merge shortcut
COPY shortcuts.jupyterlab-settings /home/${NB_USER}/.jupyter/lab/user-settings/\@jupyterlab/shortcuts-extension/shortcuts.jupyterlab-settings

# Copy jupyter_server_config.py which allows students to see and delete hidden files
COPY jupyter_server_config.py /home/${NB_USER}/.jupyter

# Install config file that sets windowing mode to 'defer'
COPY tracker.jupyterlab-settings /home/${NB_USER}/.jupyter/lab/user-settings/@jupyterlab/notebook-extension/tracker.jupyterlab-settings

# Enable resource usage bar
COPY topbar-item.jupyterlab-settings /home/jovyan/.jupyter/lab/user-settings/@jupyter-server/resource-usage/topbar-item.jupyterlab-settings

# Make sure everything in the home folder is owned by NB_USER
USER root
RUN chown -R ${NB_USER} /home/${NB_USER}
USER ${NB_UID}

# Disable healthcheck for performance reasons
HEALTHCHECK NONE