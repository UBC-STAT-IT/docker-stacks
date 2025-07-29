# Copyright (c) UBC-DSCI Development Team.
# Distributed under the terms of the Modified BSD License.
FROM quay.io/jupyter/minimal-notebook:python-3.12

LABEL maintainer="Brian Kim <brian.kim@stat.ubc.ca>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Install all OS dependencies for a fully functional Server
RUN apt-get update --yes && \
    apt-get install --yes --no-install-recommends \
    # Common useful utilities
    curl \
    git \
    zip \
    nano-tiny \
    tzdata \
    unzip \
    vim-tiny \
    # git-over-ssh
    openssh-client \
    # `less` is needed to run help in R
    # see: https://github.com/jupyter/docker-stacks/issues/1588
    less \
    # `nbconvert` dependencies
    # https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex
    texlive-xetex \
    texlive-fonts-recommended \
    texlive-plain-generic \
    # Enable clipboard on Linux host systems
    xclip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Install packages
COPY conda-linux-64.lock /tmp/conda-linux-64.lock

RUN mamba install -y --file /tmp/conda-linux-64.lock && \
    mamba clean --all -y -f && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}" 

# disable warnings that pollute build logs; seems to be related to the update to python 3.11
# https://discourse.jupyter.org/t/debugger-warning-it-seems-that-frozen-modules-are-being-used-python-3-11-0/16544/12
ENV PYDEVD_DISABLE_FILE_VALIDATION=1

# Disable the cell toolbar (which ignores metadata and students often accidentally click + delete grading cells)
RUN jupyter labextension disable @jupyterlab/cell-toolbar-extension

# Disable announcement pop-up on start
RUN jupyter labextension disable "@jupyterlab/apputils-extension:announcements"

# Install config file to remove certain shortcuts
COPY shortcuts.jupyterlab-settings /home/${NB_USER}/.jupyter/lab/user-settings/\@jupyterlab/shortcuts-extension/shortcuts.jupyterlab-settings

# Enable resource usage bar
COPY topbar-item.jupyterlab-settings /home/${NB_USER}/.jupyter/lab/user-settings/@jupyter-server/resource-usage/topbar-item.jupyterlab-settings

# Copy jupyter_server_config.py which contains extra server config 
COPY jupyter_server_config.py /home/${NB_USER}/.jupyter

# Make sure everything in the home folder is owned by NB_USER
USER root
RUN chown -R ${NB_USER} /home/${NB_USER}
USER ${NB_UID}
WORKDIR "${HOME}/work"

# Disable healthcheck for performance reasons
HEALTHCHECK NONE