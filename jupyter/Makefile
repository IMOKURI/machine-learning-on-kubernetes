.PHONY: help
.DEFAULT_GOAL := help

NOW = $(shell date '+%Y%m%d-%H%M%S')
IMAGE_NAME = "jupyter-baseline"
TAG = "torch1.10-cuda10"


build: ## Build docker image
	@docker build --build-arg PROXY=$(http_proxy) -t $(IMAGE_NAME):$(TAG) .


push: ## Push docker image
	@docker tag $(IMAGE_NAME):$(TAG) quay.io/yoshio_sugiyama/$(IMAGE_NAME):$(TAG)
	@docker push quay.io/yoshio_sugiyama/$(IMAGE_NAME):$(TAG)


test-local: ## Test docker image
	@docker run -d --rm --gpus '"device=1,2,3"' --shm-size=64g -v /data/jupyter/sugiyama/machine-learning-on-kubernetes/jupyter:/app -w /app -p 18888:8888 $(IMAGE_NAME):$(TAG)


shell-local: ## Run interactive shell
	@docker run -it --rm --gpus '"device=1,2,3"' --shm-size=64g -v /data/jupyter/sugiyama/machine-learning-on-kubernetes/jupyter:/app -w /app -p 18888:8888 $(IMAGE_NAME):$(TAG) bash


run: ## Run training on kubernetes
	@oc create -f ./job_train.yaml


clean: ## Clean up pod
	@oc delete -f ./job_train.yaml || :


help: ## Show this help
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[38;2;98;209;150m%-15s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)
