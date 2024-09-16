# hash:sha256:2bd679749752e6ef80dde9fecc4343f5a13eb7d61d7d62a3f1c43d4ef068a89a
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/jupyterlab:3.6.1-miniconda4.12.0-python3.9-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==1.0.0 \
    hdbscan==0.8.38.post1 \
    spikeinterface[full]==0.101.0

COPY postInstall /
RUN /postInstall
