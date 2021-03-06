.PHONY: help
.DEFAULT_GOAL := help

NOW = $(shell date '+%Y%m%d-%H%M%S')
TAG = "ngc-21.11"
# TAG = "1.9.0"


build: ## Build docker image
	@docker build --build-arg PROXY=$(http_proxy) -t torch-image-baseline:$(TAG) .


push: ## Push docker image
	@docker tag torch-image-baseline:$(TAG) quay.io/yoshio_sugiyama/torch-image-baseline:$(TAG)
	@docker push quay.io/yoshio_sugiyama/torch-image-baseline:$(TAG)


test-local: ## Test docker image
	@docker run --gpus '"device=1,2,3"' --shm-size=64g -v /data/jupyter/sugiyama/cassava/inputs:/app/inputs -v /data/jupyter/sugiyama/cassava/working:/app/working torch-image-baseline:$(TAG) make debug_train


shell-local: ## Run interactive shell
	@docker run -it --rm --gpus '"device=1,2,3"' --shm-size=64g -v /data/jupyter/sugiyama/cassava/inputs:/app/inputs -v /data/jupyter/sugiyama/cassava/working:/app/working torch-image-baseline:$(TAG) bash


run: ## Run training on kubernetes
	@oc create -f ./job_train.yaml


clean: ## Clean up pod
	@oc delete -f ./job_train.yaml || :


help: ## Show this help
	@awk 'BEGIN {FS = ":.*?## "} /^[a-zA-Z_-]+:.*?## / {printf "\033[38;2;98;209;150m%-15s\033[0m %s\n", $$1, $$2}' $(MAKEFILE_LIST)
