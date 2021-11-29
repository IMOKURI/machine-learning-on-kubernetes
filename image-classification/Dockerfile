FROM nvcr.io/nvidia/pytorch:21.11-py3

ARG PROXY

ENV http_proxy=$PROXY \
    https_proxy=$PROXY

RUN apt update && \
    apt install -y --no-install-recommends \
        git \
        make && \
    apt clean

RUN pip install --no-cache-dir \
    albumentations==0.4.6 \
    hydra-core \
    hydra-optuna-sweeper \
    mlflow \
    opencv-python \
    scikit-learn \
    timm \
    wandb

VOLUME /app/inputs
VOLUME /app/working
VOLUME /app/outputs

WORKDIR /app/working
