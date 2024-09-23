# hash:sha256:4137838071da450218338c54bc1ebe48e3c83bcc4cf152e516b50848fa59a25b
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/jupyterlab:3.6.1-miniconda4.12.0-python3.9-ubuntu20.04

ARG DEBIAN_FRONTEND=noninteractive

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    aind-data-schema==1.0.0 \
    hdbscan==0.8.38.post1 \
    spikeinterface[full]==0.101.1 \
    torch==2.2.0
