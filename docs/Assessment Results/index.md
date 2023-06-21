---
layout: default
title: Assessment Results
nav_order: 6
has_children: true
---

# Assessment Results

Details on the individual scaler's results can be found in the respective subpages.  
This page gives a general overview on main characteristics of the scalers.

## Core functionality

Horizontal Pod Autoscaler (HPA) and Kubernetes Event Driven Autoscaler (KEDA) are both horizontal autoscaler. Hence they adapt the amount of Pods running in a deployment depending on the present or historic resource usage, where different metrics can be taken into account.  
In difference Vertical Pod Autoscaler (VPA) changes the amount of resources that are designated to already present Pods depending on the memory and or cpu load.  

## Scaler combinations

|     | HPA |               KEDA               |                   VPA                  |
|------|:---:|:--------------------------------:|:--------------------------------------:|
| HPA  |  x  | If not scaled by the same metric |  If HPA doesn't scale by cpu or memory |
| KEDA |  -=-  |                 x                | If KEDA doesn't scale by cpu or memory |

## Setup and usage

In the setup phase of the scalers simple scaling designs are applied to the demonstrator project using the respective scaler by scaling on metrics like cpu and memory, after familiarizing with the documentation.  
In the usage phase a load generator is deployed to validate the previously configured scaler and more complex metrics and also combinations of metrics are tested.  
The difficulty of executing these steps is recorded in the assessment.

## Main Assessment Scheme

The most important categories are enlisted in the following. The full assessments are provided on the respective subpages.  

| No | Question/Criteria | HPA | KEDA | VPA |
|---|---|---|---|---|
| 4 | How difficult is the setup? |  | 3 out of 5 | 4 out of 5 |
| 6 | What triggers can be used for scaling? | CPU and memory and any custom or external metric (extra effort needed) | CPU and memory and many more with small effort | Only CPU and memory |
| 11 | How difficult is the use? |  | 2.3 out of 5 | 4 out of 5 |
| 12 | How well is the Autoscaler documented? |  | 4.3 out of 5 | 2.5 out of 5 |
|  | SUS Score |  | 80 | 36.25 |