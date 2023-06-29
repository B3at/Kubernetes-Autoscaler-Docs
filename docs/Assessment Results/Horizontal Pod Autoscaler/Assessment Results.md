---
layout: default
title: Assessment Results
parent: Horizontal Pod Autoscaler
grand_parent: Assessment Results
nav_order: 1
---

# Horizontal Pod Autoscaler Assessment Results

For the Horizontal Pod Autoscaler (HPA) three assessment data points have been recorded.  
The results are aggregated in the following.  

The assessment was executed on the most current version of HPA at the time.  
HPA is shipped with minikube and has no independent version.  
At the time of writing minikube v1.30.1  
All numeric ratings are average values.

## Core functionality 

The Horizontal Pod Autoscaler scales controllers like a Deployment horizontally.
This means that new pods are created on demand.
Triggers can be set for resources available to the existing pods.
HPA provides scaling based on CPU and memory metrics by default, as well as a system to define custom metrics.
When these resources meet a certain threshold, pods with the same amount of resources are created to satisfy the demand.  
These are called "replicas".

## Architecture

HPA can be broken down into three components:

- Metrics provider: collects and exposes metrics used by the HPA to make scaling decisions.
- Metrics processor: analyzes the available metrics based on the configured scaling algorithm.
- Controller manager: adjusts the number of replicas based on the scaling decisions made by the metrics processor.

## Combination with other Scalers 

HPA and VPA scale pods in different dimensions.
This works as long as they're not both scaling based on the same metrics.
One common strategy is configuring VPA to scale on CPU and/or memory while HPA scales on custom metrics.  
KEDA extends the functionality of HPA and scales horizontally as well.
This means using them together is redundant, but not impossible.  

## Setup configuration decisions 

- Use scaling on CPU (60%)
- Use scaling on memory (70%)

## Usage decisions

- CPU and memory scaling work out of the box.
- Try scaling only on CPU for the device communication.
- Custom metrics require additional software, like Prometheus.

## Basic research time spent

- 45min

## Extended research time spent

- 30min

## Main Assessment Scheme  

| No | Question/Criteria | Results |
|---|---|---|
| 1 | What can be scaled on? | number of replicas (pods) |
| 2 | What format is used for writing configurations? | yaml |
| 3 | How difficult is the setup? | Workhours: 45 min |
| 4 | How difficult is the setup? | Rating: 2 out of 5 (5 is very difficult) |
| 5 | Amount of configuration steps needed | 3 steps including necessary setup |
| 6 | What triggers can be used for scaling? | CPU, memory, and custom metrics |
| 7 | Can multiple different triggers be used simultaneously? | Yes |
| 8 | Can configurations be changed dynamically? | Yes |
| 9 | Can configurations be easily reused? (Degree of abstraction) | 4 out of 5 |
| 10 | How difficult is the use? | Workhours: 1h 30 min on its own, more with Prometheus |
| 11 | How difficult is the use? | Rating: 3 out of 5 |
| 12 | How well is the Autoscaler documented? | Rating: 3.6 out of 5 |
| 13 | How helpful is the Feedback on user errors? | Rating: 3.6 out of 5 |
| 14 | Which explainability methods exist? | Visually through events and stats |
| 15 | What query types are supported? (Current decisions, what if, forecast, counterfactuals) | Current decisions |
| 16 | What interfaces are supported? | CLI with kubectl, GUI with Kubernetes Dashboard, REST API |
| 17 | What observability tools can be used? | Several third party tools including Prometheus and Grafana |

The SUS Scale had an average Result of: 75

## Final summary

The Horizontal Pod Autoscaler is a native component of Kubernetes.
Even though its functionality is limited out of the box, it allows for extensibility when necessary.
This extensibility comes at the cost of configuration time.
Depending on the particular needs, it might be worth it to use KEDA instead of "reinventing the wheel".
However, for scenarios when the main scalability concern is physical resources, HPA provides an easy and quick solution without compromising robustness.
