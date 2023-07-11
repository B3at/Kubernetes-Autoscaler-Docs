---
layout: default
title: Assessment Scheme
nav_order: 5
---

Assessment Scheme
=

The idea of this Scheme is to create a basic Assessment structure that can easily be used to categorize different Autoscalers. The questions further presented are categorized in to different Goals:  
(Ex) Explainability (Co) Configurability (Ac) Accessibility  
and different Metric Groups:  
(Fea) Feature-grounded (Sub) Subjective Human-grounded (Obj) Objective Human-grounded  
The categorization of all Autoscalers is conducted using this Assessment Scheme. This Assessment Scheme is based on the ideas presented in the paper [Hitchhiker's Guide for Explainability in Autoscaling](https://doi.org/10.1145/3578245.3584728).

| No | Goal | Question/Criteria | Metric | Metric Group |
|---|---|---|---|---|
| 1 | Co | What can be scaled on? | List | Fea |
| 2 | Co | What format is used for writing configurations? | Type | Fea |
| 3 | Ac | How difficult is the setup? | Workhours | Obj |
| 4 | Ac | How difficult is the setup? | Numeric 1-5 (5 is very difficult) | Sub |
| 5 | Ac | Amount of configuration steps needed | Numeric | Obj |
| 6 | Co | What triggers can be used for scaling? | List | Fea |
| 7 | Co | Can multiple different triggers be used simultaneously? | Boolean | Fea |
| 8 | Co | Can configurations be changed dynamically? | Boolean | Fea |
| 9 | Co | Can configurations be easily reused? (Degree of abstraction) | Numeric 1-5 (5 is very high reusability) | Sub |
| 10 | Ac | How difficult is the use? | Workhours | Obj |
| 11 | Ac | How difficult is the use? | Numeric 1-5 (5 is very difficult) | Sub |
| 12 | Ac | How well is the Autoscaler documented? | Numeric 1-5 (5 is very well) | Sub |
| 13 | Ac | How helpful is the Feedback on user errors? | Numeric 1-5 (5 is very helpful) | Sub |
| 14 | Ex | Which explainability methods exist? | List | Fea |
| 15 | Ex | What query types are supported? (Current decisions, what if, forecast, counterfactuals) | List | Fea |
| 16 | Ex | What interfaces are supported? | List | Fea |
| 17 | Ex | What observability tools can be used? | List | Fea |

Afterwards the SUS Assessment Scheme will be used to give each Autoscaler an additional Score.

Assessment Process
-
The Scheme derived earlier can now be categorized into different steps of the Assessment Process:  
1-2 Basic research for one hour  
Decide on how to scale the different services of the Demonstrator  
3-5 Autoscaler Setup  
6-13 Autoscaler Usage  
14-17 Extended explainability research for one hour  

Autoscaler Setup: Basic Autoscaler Setup using the Demonstrator.  
Autoscaler Usage: Add Load Generator and test more advanced scaling configurations. Try to use multiple triggers, if supported.  
