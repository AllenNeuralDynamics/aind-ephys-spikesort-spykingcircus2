# hash:sha256:93b51867528c727a3f8af65b68fd228cf4e67f36d026a66098f36b0290c00f34
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
    aind-data-schema==1.0.0 \
    hdbscan==0.8.38.post1 \
    spikeinterface[full]==0.101.2 \
    torch==2.2.0

COPY postInstall /
RUN /postInstall
