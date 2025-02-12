---
title: "Designing Data-Intensive Applications"
description: 
aliases: 
tags: 
draft: "true"
created-date: "2025-02-12"
---



## Chapter 1 - Reliable, Scalable, and Maintainable Applications

> The internet was done so well that most people think of it as a natural resource like the Pactific Ocean, rather than something that was main-made. When was the last time a technology with a scale like that was so error-free?

Alan Kay, in interview with Dr Dobb's Journal (2012)


Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications- bigger problemas are usually the amount of data, the complexity of data, and the speed at which it is changing


### Reliability 
The system should continue to work correctly even in the face of adversity.


> Fault is not the sae as failure. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. It is impossible to reduce the probability of a fault to zero. therefore it is ussually best t odesign fault-tolerance mechanisms that prevent faults from causing failures. In this book we conver several techniques for building eliable systems from unreliable parts.


### Scalability 
Is the system ability to cope with increased load