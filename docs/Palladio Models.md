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