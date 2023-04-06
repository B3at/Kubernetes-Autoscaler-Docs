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
| 4 | Ac | Amount of cofiguration steps needed | Numeric | Obj |
| 5 | Co | What triggers can be used for scaling? | List | Fea |
| 6 | Co | Can multiple different triggers be used simultaneously? | Boolean | Fea |
| 7 | Co | Can configurations be changed dynamically? | Boolean | Fea |
| 8 | Co | Can configurations be easily reused? (Degree of abstraction) | Numeric 1-5 | Sub |
| 9 | Ac | How difficult is the use? | Workhours | Obj |
| 10 | Ac | How well is the Auroscaler documented? | Numeric 1-5 | Sub |
| 11 | Ac | How helpful is the Feedback on user errors? | Numeric 1-5 | Sub |
| 12 | Ex | Which explainability methods exist? | List | Fea |
| 13 | Ex | What query types are supported? (Current decisions, forecast, counterfactuals) | List | Fea |
| 14 | Ex | What interfaces are supported? | List | Fea |
| 15 | Ex | What observability tools can be used? | List | Fea |


Assessment Process:
-
The Scheme derived earlier can now be categorized into different steps of the Assessment Process:  
1-2 Basic research  
3-4 Autoscaler Setup  
5-11 Autoscaler Usage  
12-15 Extended explainability research

Ideas for the Process:  
Autoscaler Setup: Basic Autoscaler Setup using the Demonstrator with CPU Trigger.  
Autoscaler Usage: Add Load Generator and add additional RAM Trigger. Try to use multiple triggers, if supported.  
