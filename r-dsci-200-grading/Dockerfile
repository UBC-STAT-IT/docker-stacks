# Copyright (c) UBC-DSCI Development Team.
# Distributed under the terms of the Modified BSD License.
# FROM ubcdsci/r-dsci-200:latest
FROM r-dsci-200:20251204

# Install nbgrader
RUN mamba install nbgrader

# Allow all shortcuts
RUN rm -f /home/${NB_USER}/.jupyter/lab/user-settings/\@jupyterlab/shortcuts-extension/shortcuts.jupyterlab-settings