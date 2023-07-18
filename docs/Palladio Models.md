---
layout: default
title: Palladio Models
nav_order: 7
---

# Palladio Models

In the following we list exemplatory models of specific scenarios that we created using Palladio with Slingshot and the SPD language to model and test scaling behaviors.  

## SingleService

This is a simple example modelling a books database. It consists of a Website component and a Database component and offers a single method: "string searchBook(long ISBN)", that simulates retrieving a book by ISBN from the book database. The resource environment consists of a single Node (Resource Container).  
The model includes an SPD scaling policy that fires on CPU utilization of over 60 percent and relatively adjusts by 100 percent and therefore resembles a simple scaling behavior as implementable using HPA or KEDA.  

Download: <a download="SingleService.zip" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/SingleService.zip" title="SingleService.zip">SingleService.zip
</a>

## SingleServiceDistributed

This is an adaption of the SingleService model. It uses two Nodes instead of a single one that communicate over a linking resource. Also, the CPU resources have two replicas.  So, this model is meant to represent a distributed scenario like in a Kubernetes cluster.  

Download: <a download="SingleServiceDistributed.zip" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/SingleServiceDistributed.zip" title="SingleServiceDistributed.zip">SingleServiceDistributed.zip
</a>

## CalculationService

This is a model simulating a Calculation Server. It consists of a Web component, that sends the desired values that should be calculated to the Server. The Server now calcultes and sends the result back to the Web. The model includes an SPD scaling policy that scales in steps. If the Trend of the CPU Utilization is at MAX, one more replica is created, if it is at MIN, a replica is deleted.

Download: <a download="SingleServiceDistributed.zip" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/CalculationService.zip" title="CalculationService.zip">CalculationService.zip
</a>

## MassiveServce

This is a model simulating a very big Server, that has to be logged in to. It consists of a Web component, which sends the Log In request to the Server. This Server now tries to authenticate the Log In using the Database Component. The SPD scaling policy doubles the current number of elements if the current CPU Utilization is greater or equal to MAX, it halves the current number of elements, if the current CPU Utilization is lesser or equal to AVERAGE.

Download: <a download="SingleServiceDistributed.zip" href="/Kubernetes-Autoscaler-Docs/demonstratorDownloads/MassiveService.zip" title="MassiveService.zip">MassiveService.zip
</a>

