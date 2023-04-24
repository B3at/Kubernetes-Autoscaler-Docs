---
layout: default
title: Assessment Scheme
nav_order: 5
---

Assessment Scheme:
=

The idea of this Scheme is to create a basic Assessment structure that can easily be used to categorize different Autoscalers. The questions further presented are categorized in to different Goals:  
(Ex) Explainability (Co) Configurability (Ac) Accessibility  
and different Metric Groups:  
(Fea) Feature-grounded (Sub) Subjective Human-grounded (Obj) Objective Human-grounded  
The categorization of all Autoscalers is conducted using this Assessment Scheme. This Assessment Scheme is based on the ideas presented in the paper (TODO: Insert Paper Link here).

| No | Goal | Question/Criteria | Metric | Metric Group |
|---|---|---|---|---|
| 1 | Co | What can be scaled on? | List | Fea |
| 2 | Co | What format is used for writing configurations? | Type | Fea |
| 3 | Ac | How difficult is the setup? | Workhours | Obj |
| 4 | Ac | How difficult is the setup? | Numeric 1-5 | Sub |
| 5 | Ac | Amount of cofiguration steps needed | Numeric | Obj |
| 6 | Co | What triggers can be used for scaling? | List | Fea |
| 7 | Co | Can multiple different triggers be used simultaneously? | Boolean | Fea |
| 8 | Co | Can configurations be changed dynamically? | Boolean | Fea |
| 9 | Co | Can configurations be easily reused? (Degree of abstraction) | Numeric 1-5 | Sub |
| 10 | Ac | How difficult is the use? | Workhours | Obj |
| 11 | Ac | How difficult is the use? | Numeric 1-5 | Sub |
| 12 | Ac | How well is the Autoscaler documented? | Numeric 1-5 | Sub |
| 13 | Ac | How helpful is the Feedback on user errors? | Numeric 1-5 | Sub |
| 14 | Ex | Which explainability methods exist? | List | Fea |
| 15 | Ex | What query types are supported? (Current decisions, what if, forecast, counterfactuals) | List | Fea |
| 16 | Ex | What interfaces are supported? | List | Fea |
| 17 | Ex | What observability tools can be used? | List | Fea |

Afterwards the SUS Assessment Scheme will be used to give each Autoscaler an additional Score.

Assessment Process:
-
The Scheme derived earlier can now be categorized into different steps of the Assessment Process:  
1-2 Basic research for one hour 
3-5 Autoscaler Setup
6-13 Autoscaler Usage
14-17 Extended explainability research for one hour

Autoscaler Setup: Basic Autoscaler Setup using the Demonstrator with CPU Trigger.  
Autoscaler Usage: Add Load Generator and add additional RAM Trigger. Try to use multiple triggers, if supported.  
