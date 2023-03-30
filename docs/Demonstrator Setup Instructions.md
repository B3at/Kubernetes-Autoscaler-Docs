---
layout: default
title: Demonstrator Setup Instructions
nav_order: 3
---

This is a Step by Step Guide to install minikube and the provided Demonstrator Test Environment. Download Links for the Files will be provided in the Future.

Downloading all components
-

1. Get and install minikube from the Website: <https://minikube.sigs.k8s.io/docs/start/>
2. From the Demonstrator Pull/Download MongoDB, Data Processing, Data Provider and Device Communication
3. Get and install helm: <https://helm.sh/docs/intro/install/>
4. You need the following provided Files (the gitlab-credentials.yaml needs to contain a valid token to fetch the demonstrator images):  
<a download="gitlab-credentials.yaml" href="/demonstratorDownloads/gitlab-credentials.yaml" title="gitlab-credentials.yaml">gitlab-credentials.yaml
</a>  
<a download="protocomCalibration-pvc.yaml" href="/demonstratorDownloads/protocomCalibration-pvc.yaml" title="protocomCalibration-pvc.yaml">protocomCalibration-pvc.yaml
</a>  
<a download="data-provider-minikube.yaml" href="/demonstratorDownloads/data-provider-minikube.yaml" title="data-provider-minikube.yaml">data-provider-minikube.yaml
</a>  
<a download="device-communication-minikube.yaml" href="/demonstratorDownloads/device-communication-minikube.yaml" title="device-communication-minikube.yaml">device-communication-minikube.yaml
</a>  
<a download="data-processing-minikube.yaml" href="/demonstratorDownloads/data-processing-minikube.yaml" title="data-processing-minikube.yaml">data-processing-minikube.yaml
</a>

Setup MongoDB
-

1. `kubectl create namespace demonstrator`
2. `kubectl apply -f gitlab-credentials.yaml`
3. Apply all yaml files from the mongo-master folder
4. `kubectl get pods`
5. Now you can Port Forward the mongo-express to test if it works (`kubectl port-forward service/[mongo_express_something] PORT`)

Setup Persistent Volume Claims
-

1. `kubectl apply -f protocomCalibration-pvc.yaml`

Setup RabbitMQ
-

1. `helm repo add bitnami https://charts.bitnami.com/bitnami`
2. `helm install my-rabbit-rabbitmq --set auth.username=user,auth.password=k7cwXXdsPk,persistence.enabled=false,extraPlugins=rabbitmq_message_timestamp,communityPlugins=https://github.com/rabbitmq/rabbitmq-message-timestamp/releases/download/v3.10.0/rabbitmq_message_timestamp-3.10.0.ez bitnami/rabbitmq`

Setup Data Provider/Data Processing/Device Communication
-

1. `kubectl apply -f data-provider-minikube.yaml`
2. `kubectl get pods -n demonstrator`
3. `kubectl logs pod/[data-provider-something] -f -n demonstrator` to Test (First time installation will load a while)
4. Repeat above steps for Data Processing and Device Communication

Access Services
-

1. Wait for Device Communication and Data Provider to finish in the Logs
2. `kubectl get services -n demonstrator`
3. `minikube service [service-name] --url` for Device Communication and Data Provider
