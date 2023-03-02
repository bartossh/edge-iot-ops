SHELL = /bin/bash
MYEKUIPER=my-ekuiper

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
	KUBECONFIG=./kubeconfig.yaml helm install $(MYEKUIPER) emqx/kuiper
	@echo
	@echo "Waiting for deployment done."
	until kubectl --kubeconfig=./kubeconfig.yaml get pods $(MYEKUIPER)-0 --no-headers -o custom-columns=":status.phase"; do sleep 2; done



.PHONY: deployment-down
deployment-down:
	@echo
	@echo "Stop K3s cluster and registry locally."
	docker-compose \
	-f ./docker-compose.yaml \
	down
