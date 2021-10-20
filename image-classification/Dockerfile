FROM pytorch/pytorch:1.9.0-cuda11.1-cudnn8-runtime

RUN pip install --no-cache-dir \
    albumentations==0.4.6 \
    mlflow \
    opencv-python \
    timm \
    wandb

VOLUME /app/inputs
VOLUME /app/working
VOLUME /app/outputs

WORKDIR /app/working
