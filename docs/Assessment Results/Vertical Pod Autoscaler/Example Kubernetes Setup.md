---
layout: default
title: Example Kubernetes Setup
parent: Vertical Pod Autoscaler
grand_parent: Assessment Results
nav_order: 2
---

# Example Kubernetes Setup

In this example setup the data-processing and data-provider components are set to be scaled by VPA on CPU and memory and the device-communication to be only scaled on CPU.  

1. Follow the instructions at [Demonstrator Setup Instructions]({% link Demonstrator Setup Instructions.md %}) but instead use the following yaml files for the demonstrator components (they include resource request values for memory and CPU):  

   - <a download="data-provider-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-provider-minikube.yaml" title="data-provider-minikube.yaml">data-provider-minikube.yaml
    </a>  
   - <a download="device-communication-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/device-communication-minikube.yaml" title="device-communication-minikube.yaml">device-communication-minikube.yaml
    </a>  
   - <a download="data-processing-minikube.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-processing-minikube.yaml" title="data-processing-minikube.yaml">data-processing-minikube.yaml
    </a> 

2. Activate the metrics-server addon in minkube (`minikube addons enable metrics-server`)
3. Clone the [Vertical Pod Autoscaler](https://github.com/kubernetes/autoscaler) Repo on Github.
4. If running on windows with git bash it might be necessary to do the following:  
   Change in autoscaler/vertical-pod-autoscaler/pkg/admission-controller/gencerts.sh the first / in the -subj parameters of openssl to //.
5. Run ./vertical-pod-autoscaler/hack/vpa-up.sh
6. Apply the following VPA yaml files to the cluster:  
   
   - <a download="data-provider-vpa.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-provider-vpa.yaml" title="data-provider-vpa.yaml">data-provider-vpa.yaml
    </a>  
   - <a download="device-communication-vpa.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/device-communication-vpa.yaml" title="device-communication-vpa.yaml">device-communication-vpa.yaml
    </a>  
   - <a download="data-processing-vpa.yaml" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/VPA/data-processing-vpa.yaml" title="data-processing-vpa.yaml">data-processing-vpa.yaml
    </a>

Now the VPA should scale all of the three components of the demonstrator. To test with an example load a load generator can be used.  
Details on the currently assigned resources to the pods can be access using `kubectl get vpa -n demonstrator`.
