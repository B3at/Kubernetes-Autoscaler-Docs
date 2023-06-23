---
layout: default
title: Example Kubernetes Setup
parent: Horizontal Pod Autoscaler
grand_parent: Assessment Results
nav_order: 2
---

# Example Kubernetes Setup

In this example all components are set to be scaled upon CPU and Memory triggers.

1. Follow the instructions at [Demonstrator Setup Instructions]({% link docs/Demonstrator Setup Instructions.md %}) but instead use the following yaml files for the demonstrator components (they include resource request values for memory and CPU):  
    - <a download="data-provider-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/HPA/data-provider-minikube.yaml" title="data-provider-minikube.yaml">data-provider-minikube.yaml
    </a>  
   - <a download="device-communication-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/HPA/device-communication-minikube.yaml" title="device-communication-minikube.yaml">device-communication-minikube.yaml
    </a>  
   - <a download="data-processing-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/HPA/data-processing-minikube.yaml" title="data-processing-minikube.yaml">data-processing-minikube.yaml
    </a>
2. Activate the metrics-server addon in minkube (`minikube addons enable metrics-server`)
3. Apply the following HPA yaml files to the cluster:  

   - Data Provider:  

   ```yaml
   apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: data-provider-hpa
      namespace: demonstrator
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: data-provider
    minReplicas: 1
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
          name: cpu
          target:
            type: Utilization
            averageUtilization: 60
    - type: Resource
        resource: 
          name: memory
          target: 
            type: Utilization
            averageUtilization: 70
   ```

   - Device Communication:  

   ```yaml
   apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: device-communication-hpa
      namespace: demonstrator
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: device-communication
    minReplicas: 1
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
          name: cpu
          target:
            type: Utilization
            averageUtilization: 60
   ```

   - Data Processing:  

   ```yaml
   apiVersion: autoscaling/v2
    kind: HorizontalPodAutoscaler
    metadata:
      name: data-processing-hpa
      namespace: demonstrator
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: data-processing
    minReplicas: 1
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
          name: cpu
          target:
            type: Utilization
            averageUtilization: 60
    - type: Resource
        resource: 
          name: memory
          target: 
            type: Utilization
            averageUtilization: 70
   ```

4. Alternatively one can also use the kubectl commands for creating the hpa configurations, but this currently only supports scaling by CPU utilization:
   `kubectl autoscale deployment data-provider --cpu-percent=60 --min=1 --max=10 -n demonstrator`

Now the HPA should scale all of the three components of the demonstrator. To test with an example load a load generator can be used.  
Details on the currently assigned resources to the pods can be access using `kubectl get hpa -n demonstrator`.
