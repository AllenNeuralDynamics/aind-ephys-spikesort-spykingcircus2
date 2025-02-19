# hash:sha256:6c23f64e87d36ffb019e8dae97c3f297760f1276906b06ad98f43c7148b3d7cb
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/jupyterlab:3.6.1-miniconda4.12.0-python3.9-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive
ARG AWS_ACCESS_KEY_ID
ARG AWS_DEFAULT_REGION
ARG AWS_SECRET_ACCESS_KEY

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==1.3.0 \
    hdbscan==0.8.40 \
    spikeinterface[full]==0.102.1 \
    torch==2.6.0

COPY postInstall /
RUN /postInstall
