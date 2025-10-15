FROM prairielearn/workspace-jupyterlab-r:523b1a9d375f8c8e14b917eaa7195921e5ae388a

USER root

# Install R packages
COPY conda-linux-64.lock /tmp/conda-linux-64.lock

RUN mamba install --yes --file /tmp/conda-linux-64.lock && \
    mamba clean --all -f -y 

USER ${NB_UID}