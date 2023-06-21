---
layout: default
title: Assessment Results
parent: Vertical Pod Autoscaler
grand_parent: Assessment Results
nav_order: 1
---

# Vertical Pod Autoscaler Assessment Results

For the Vertical Pod Autoscaler (VPA) two assessment-datapoints have been recorded.  
The results are aggregated in the following.  

The assessment was executed on the most current version of VPA at the time:  
version 0.13.0  
All numeric ratings are median values.

## Core functionality  

The Vertical Pod Autoscaler scales controllers like a Deployment vertically. This means that the assigned resources to a pod are adapted in accordance to the pod's current and past resource usage. If needed, an old pod is killed and a new pod with adapted resource requests is scheduled, in order to adapt to a change in the pod's load. In difference to the other evaluated autoscalers this means that the amount of pods in use doesn't change dynamically.  
It can only be scaled vertically on the CPU and memory resources.  
It is planned that in a future version of VPA pods will not have to be killed and recreated but updated with new resource requests dynamically, to achieve higher responsiveness and less downtime.

## Architecture

VPA comprises three components:  

- Recommender: Monitors the resource usage and recommends values for CPU and Memory
- Updater: Kills pods that have outdated resources set
- Admission plugin: Sets correct resources for newly created or recreated pods by the controller (ex. Deployment)  

## Combination with other Scalers  

According to the documentation, VPA should not be combined with the Horizontal Pod Autoscaler if using both with the same resources (that is CPU or memory). This implies that also VPA and KEDA should not be used together if scaling on CPU and memory.  
This is because the combination can lead to the HPA creating multiple new pods as a reaction to increased load, but these new pods have only little load while starting up, which again leads to VPA scaling them down vertically. In this way, one can end up with many small pods in the cluster.  
However, combinations of VPA with HPA or KEDA are possible if using HPA or KEDA only on custom and external metrics because those don't necessarily interfere with each other.

## Setup configuration decisions  

- Use scaling on CPU and Memory

## Usage decisions

- Try to optimize the request and min and max allowed resources values using a load generator
- Try scaling only on CPU

## Basic research time spent

- 55min

## Extemded research time spent

- 40min

## Main Assessment Scheme  

| No | Question/Criteria | Results |
|---|---|---|
| 1 | What can be scaled on? | CPU and memory vertically |
| 2 | What format is used for writing configurations? | yaml |
| 3 | How difficult is the setup? | Workhours: 2h 53min |
| 4 | How difficult is the setup? | Rating: 4 out of 5 (5 is very difficult) |
| 5 | Amount of configuration steps needed | 4 to 6 steps depending on the OS and version (more details in the example setup) |
| 6 | What triggers can be used for scaling? | Historic and current CPU and memory resource usage |
| 7 | Can multiple different triggers be used simultaneously? | CPU and memory are used together per default, but those are the only available triggers |
| 8 | Can configurations be changed dynamically? | Yes, the yaml files can be applied to update a running VPA resource |
| 9 | Can configurations be easily reused? (Degree of abstraction) | Rating: 3.5 out of 5 <br /> The target resource name and the min and max resource limits have to be adapted |
| 10 | How difficult is the use? | Workhours: 2h |
| 11 | How difficult is the use? | Rating: 4 out of 5 |
| 12 | How well is the Autoscaler documented? | Rating: 2.5 out of 5 |
| 13 | How helpful is the Feedback on user errors? | Rating: 2 out of 5 |
| 14 | Which explainability methods exist? | Visually by using get and describe on vpa, but the feedback is very limited |
| 15 | What query types are supported? (Current decisions, what if, forecast, counterfactuals) | Current decision: Currently set CPU and memory values with "get vpa". Current target resource request is also visible through "desribe vpa". No other query types, like what ifs or forecasts are supported |
| 16 | What interfaces are supported? | Kubectl command line tool (the VPA components are normal kubernetes resources), but no specific kubectl commands for using vpa |
| 17 | What observability tools can be used? | Prometheus to pass historical resource usage to the Recommender component |

The SUS Scale had an average Result of: 36.25

## Final summary

The Vertical Pod Autoscaler is currently in a pre-release version (0.13.0) and suffers typical pre-release problems. The documentation lacks some helpful information and on Windows adaptions to the setup script of VPA had to be made for all resources to be correctly installed. Also, the feature set is very limited and the maturity of existing features has to be improved. Especially, the explainability of the VPA components is lacking. Only very basic information on the current scaling decisions are provided (the CPU and memory request targets that are currently set by the VPA), but no information on the current CPU or memory usage, let alone what if or forecast queries.
