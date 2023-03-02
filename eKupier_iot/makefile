SHELL = /bin/bash

.PHONY: deployment-up
deployment-up: TAG := $(shell date +"%Y-%m-%d-%I-%M-%S")
deployment-up:
	@echo
	@echo "Start K3s cluster and registry locally."
	docker-compose \
	-f ./docker-compose.yaml \
	up -d

	KUBECONFIG=./kubeconfig.yaml helm repo add emqx https://repos.emqx.io/charts
	KUBECONFIG=./kubeconfig.yaml helm repo update
	KUBECONFIG=./kubeconfig.yaml helm install my-ekuiper emqx/kuiper
	@echo
	@echo "Waiting for deployment done."
	until kubectl --kubeconfig=./kubeconfig.yaml get pods; do sleep 1; done



.PHONY: deployment-down
deployment-down:
	@echo
	@echo "Stop K3s cluster and registry locally."
	docker-compose \
	-f ./docker-compose.yaml \
	down
