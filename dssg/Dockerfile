# Copyright (c) UBC-DSCI Development Team.
# Distributed under the terms of the Modified BSD License.
FROM jupyter/r-notebook

USER root

# install vim and libgsl (for tidyclust)
RUN apt-get update && apt-get install -y vim libgsl27 libgsl-dev build-essential

# disable warnings that pollute build logs; seems to be related to the update to python 3.11
# https://discourse.jupyter.org/t/debugger-warning-it-seems-that-frozen-modules-are-being-used-python-3-11-0/16544/12
ENV PYDEVD_DISABLE_FILE_VALIDATION=1

# Install R packages
COPY conda-linux-64.lock /tmp/conda-linux-64.lock

RUN mamba update --quiet --file /tmp/conda-linux-64.lock && \
	mamba clean --all -y -f

# Disable announcement pop-up on start
RUN jupyter labextension disable "@jupyterlab/apputils-extension:announcements"

# Use custom start.sh
COPY start.sh /usr/local/bin/start.sh

# Disable healthcheck for performance reasons
HEALTHCHECK NONE