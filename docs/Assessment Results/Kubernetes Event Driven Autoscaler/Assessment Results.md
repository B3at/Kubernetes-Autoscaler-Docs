---
layout: default
title: Assessment Results
parent: Kubernetes Event Driven Autoscaler
grand_parent: Assessment Results
nav_order: 1
---

# Kubernetes Event Driven Autoscaler Assessment Results 

For the Kubernetes Event Driven Autoscaler (KEDA) three assessment datapoints have been recorded. The results are aggregated in the following.

The assessment was executed on the most current version of KEDA at the time:
version 2.10.1.

## Core functionality

KEDA is an autoscaler that builds upon the Horizontal Pod Autoscaler. This means that it can only scale horizontally by adding more pods. But as a new feature KEDA adds Events and Triggers upon these events. When an Event happens, a deployment can be scaled from 0 to 1 pods, or from 1 to 0 pods. If a pod is already existent, more pods can also be created (HPA functionality is not lost when using KEDA).

## Architecture

KEDA perfroms three roles:

- Agent: Activates and deactivates deployments (sclaes from 0 to 1, or from 1 to 0).
- Metrics: Exposes event data to the deployment. Enables Event integration.
- Admission Webhooks: Validates ressource configurations to avoid misconfiguration.

## Combination with other Scalers

In principle KEDA can be used with VPA and HPA. For HPA it is not advised to use them together scaling the same workload, as the scalers will start to compete. Instead the CPU-/Memory-Triggers implemented in KEDA can be used.

It is not documented, if VPA can be used with KEDA, but VPA should not be used with HPA. So as long as KEDA is used to scale upon CPU and Memory, VPA should be avoided. If KEDA is used only for other trtiggers a combination should be fine though.

## Setup configuration decisions

- Scale on RabbitMQ Event and CPU

## Usage decisions

- Try to scale CPU and Memory when load generator is used

## Basic research time spent

- Average: 60 min

## Extended research time spent

- Average: 45 min

## Main Assessment Scheme

| No | Question/Criteria | Results |
|---|---|---|
| 1 | What can be scaled on? | Pods can be scaled on Evenets from 0 to 1, then more pods can be added. |
| 2 | What format is used for writing configurations? | yaml, helm charts |
| 3 | How difficult is the setup? | Average Workhours: 1h 30min |
| 4 | How difficult is the setup? | Average Rating: 3 out of 5 (5 is very difficult) |
| 5 | Amount of configuration steps needed | 3 steps |
| 6 | What triggers can be used for scaling? | KEDA features a very large and extensive list of Events that can be used for scaling. |
| 7 | Can multiple different triggers be used simultaneously? | Yes, very easily |
| 8 | Can configurations be changed dynamically? | Yes, a new yaml file can be reapplied and the ScaledObject should restart. |
| 9 | Can configurations be easily reused? (Degree of abstraction) | As KEDA has a lot of different Events this has to be differentiated. Same Events and plattform Average Rating: 5, Different Events or Different Plattform: Average 2.5 |
| 10 | How difficult is the use? | Average Workhours: 2h 20min |
| 11 | How difficult is the use? | Median Rating: 2.3 out of 5 |
| 12 | How well is the Autoscaler documented? | Median Rating: 4.3 out of 5 |
| 13 | How helpful is the Feedback on user errors? | Median Rating: 4 out of 5 |
| 14 | Which explainability methods exist? | As KEDA builds upon HPA the same explainability methods exist |
| 15 | What query types are supported? (Current decisions, what if, forecast, counterfactuals) | The current decision can be seen through the metric server. It is not really possible to see the Events happening, so why and what if are not supported. |
| 16 | What interfaces are supported? | Kubectl command line tool |
| 17 | What observability tools can be used? | Prometheus, Grafana, Datadog, Sysdig and others |

The SUS Scale had an average Result of:  80

## Final summary

The Kubernetes Event Driven Autoscaler feels like a very finished and polished product. The documentation is very extensive, although sometimes a little bit outdated. The very big list of events that can be scaled upon, which are all documented individually, offers a variety of use cases, making this scaler useful in almost every case. The installation is very easy and the configuration is managable. Before using this autoscaler, an understanding of HPA is recommended.