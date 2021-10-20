FROM pytorch/pytorch:1.9.0-cuda11.1-cudnn8-runtime

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
    mlflow \
    opencv-python \
    scikit-learn \
    timm \
    wandb

VOLUME /app/inputs
VOLUME /app/working
VOLUME /app/outputs

WORKDIR /app/working
