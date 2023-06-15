---
layout: default
title: Example Kubernetes Setup
parent: Kubernetes Event Driven Autoscaler
grand_parent: Assessment Results
nav_order: 2
---

# Example Kubernetes Setup

In this example all components are set to be scaled upon CPU triggers. Additionally Data Processing scales upon the RabbitMQ Message Rate.

1. Follow the instructions at [Demonstrator Setup Instructions]({% link docs/Demonstrator Setup Instructions.md %}) but instead use the following yaml files for the demonstrator components (they include resource request values for memory and CPU):  
    - <a download="data-provider-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-provider-minikube.yaml" title="data-provider-minikube.yaml">data-provider-minikube.yaml
    </a>  
   - <a download="device-communication-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/device-communication-minikube.yaml" title="device-communication-minikube.yaml">device-communication-minikube.yaml
    </a>  
   - <a download="data-processing-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-processing-minikube.yaml" title="data-processing-minikube.yaml">data-processing-minikube.yaml
    </a> 
2. Activate the metrics-server addon in minkube (`minikube addons enable metrics-server`)
3. Apply the KEDA yaml file (`kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.10.1/keda-2.10.1.yaml`)^
4. Apply the following KEDA yaml files to the cluster:
    - <a download="keda-dataprocessing.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/KEDA/keda-data-processing.yaml" title="keda-data-processing.yaml">keda-data-processing.yaml
    </a>  
   - <a download="keda-data-provider.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/KEDA/keda-data-provider.yaml" title="keda-data-provider.yaml">keda-data-provider.yaml
    </a>  
   - <a download="keda-device-communication.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/keda-device-communication-vpa.yaml" title="keda-device-communication.yaml">keda-device-communication.yaml
    </a>

    Now KEDA should scale upon CPU and RabbitMQ. To test this a load generator can be used.