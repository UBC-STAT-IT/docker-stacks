# Copyright (c) UBC-DSCI Development Team.
# Distributed under the terms of the Modified BSD License.
FROM ubcstatit/r-stat-545:latest

# Install nbgrader
RUN mamba install nbgrader

# Allow all shortcuts
RUN rm -f /home/${NB_USER}/.jupyter/lab/user-settings/\@jupyterlab/shortcuts-extension/shortcuts.jupyterlab-settings