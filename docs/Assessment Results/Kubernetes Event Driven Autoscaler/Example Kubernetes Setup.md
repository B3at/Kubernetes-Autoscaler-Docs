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
    - <a download="data-provider-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/KEDA/data-provider-minikube.yaml" title="data-provider-minikube.yaml">data-provider-minikube.yaml
    </a>  
   - <a download="device-communication-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/KEDA/device-communication-minikube.yaml" title="device-communication-minikube.yaml">device-communication-minikube.yaml
    </a>  
   - <a download="data-processing-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/KEDA/data-processing-minikube.yaml" title="data-processing-minikube.yaml">data-processing-minikube.yaml
    </a>
2. Activate the metrics-server addon in minkube (`minikube addons enable metrics-server`)
3. Apply the KEDA yaml file (`kubectl apply -f https://github.com/kedacore/keda/releases/download/v2.10.1/keda-2.10.1.yaml`)^
4. Apply the following ScaledObject yaml files to the cluster:

    - Data Provider:  

    ```
    apiVersion: keda.sh/v1alpha1
    kind: ScaledObject
    metadata: 
    name: keda-data-provider
    namespace: demonstrator
    spec:
    scaleTargetRef:
        name: data-provider
    triggers:
    - type: cpu
        metricType: Utilization
        metadata:
        value: "60"   
    ```

    - Device Communication:  

    ```
    apiVersion: keda.sh/v1alpha1
    kind: ScaledObject
    metadata: 
    name: keda-device-communication
    namespace: demonstrator
    spec:
    scaleTargetRef:
        name: device-communication
    triggers:
    - type: cpu
        metricType: Utilization
        metadata:
        value: "60"      
    ```

    - Data Processing:  

    ```
    apiVersion: keda.sh/v1alpha1
    kind: ScaledObject
    metadata: 
    name: keda-data-processing
    namespace: demonstrator
    spec:
    scaleTargetRef:
        name: data-processing
    triggers:
    - type: rabbitmq
        metadata:
        host: amqp://user:k7cwXXdsPk@10.110.18.77:5672//
        mode: MessageRate
        value: "100.50"
        queueName: data-available
    - type: cpu
        metricType: Utilization
        metadata:
        value: "60"   
    ```

    Now KEDA should scale upon CPU and RabbitMQ. To test this a load generator can be used.
