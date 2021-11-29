FROM jupyter/scipy-notebook:latest

ARG PROXY

ENV http_proxy=$PROXY \
    https_proxy=$PROXY

RUN pip install --no-cache-dir \
    albumentations==0.4.6 \
    hydra-core \
    hydra-optuna-sweeper \
    opencv-python \
    torch torchvision torchaudio \
    scikit-learn \
    timm \
    wandb

VOLUME /app

WORKDIR /app
