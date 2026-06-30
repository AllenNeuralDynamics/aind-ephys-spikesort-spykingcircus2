# hash:sha256:54b6f821746a7690da3ac9b0afc777a0ad8d85d8bba90e2dbeb23d181df8fc8b
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/mambaforge3:24.5.0-0-python3.12.4-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-ask-pass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential=12.9ubuntu3 \
    && rm -rf /var/lib/apt/lists/*

RUN pip install -U --no-cache-dir \
    aind-data-schema==2.8.1 \
    hdbscan==0.8.43 \
    spikeinterface[full]==0.104.7 \
    torch==2.6.0
