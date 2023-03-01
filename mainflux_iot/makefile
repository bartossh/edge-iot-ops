SHELL = /bin/bash

.PHONY: kube-up
kube-up: TAG := $(shell date +"%Y-%m-%d-%I-%M-%S")
kube-up:
	@echo
	@echo "Start K3s cluster and registry locally."
	docker-compose \
	-f ./docker-compose.yaml \
	up -d


.PHONY: kube-down
kube-down:
	@echo
	@echo "Stop K3s cluster and registry locally."
	docker-compose \
	-f ./docker-compose.yaml \
	down

.PHONY: mainflux-up
mainflux-up:
	cat ./agent-deployment.yaml | kubectl --kubeconfig=./kubeconfig.yaml apply -f -

.PHONY: mainflux-down
mainflux-down:
	cat ./agent-deployment.yaml | kubectl --kubeconfig=./kubeconfig.yaml delete -f -