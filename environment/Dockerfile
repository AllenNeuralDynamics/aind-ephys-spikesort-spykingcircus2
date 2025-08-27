# hash:sha256:596f9c3a0ac0d0705ffef84a691a4094bff27f0aa1cba0d75ac81a9663260a2f
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/mambaforge3:24.5.0-0-python3.12.4-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-askpass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        build-essential=12.9ubuntu3 \
    && rm -rf /var/lib/apt/lists/*

RUN pip install -U --no-cache-dir \
    aind-data-schema==1.3.0 \
    hdbscan==0.8.40 \
    spikeinterface[full]==0.103.0 \
    torch==2.6.0
