---
title: Designing Data-Intensive Applications
description: 
aliases: 
tags: 
created-date: 2025-02-12
---



## Chapter 1 - Reliable, Scalable, and Maintainable Applications

> The internet was done so well that most people think of it as a natural resource like the Pactific Ocean, rather than something that was main-made. When was the last time a technology with a scale like that was so error-free?

Alan Kay, in interview with Dr Dobb's Journal (2012)


Many applications today are data-intensive, as opposed to compute-intensive. Raw CPU power is rarely a limiting factor for these applications- bigger problemas are usually the amount of data, the complexity of data, and the speed at which it is changing


### Reliability 
The system should continue to work correctly even in the face of adversity. A system is reliable depending on its ability to tolerate fault.

> Fault is not the same as failure. A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user. It is impossible to reduce the probability of a fault to zero. therefore it is ussually best to design fault-tolerance mechanisms that prevent faults from causing failures. In this book we conver several techniques for building eliable systems from unreliable parts.


### Scalability 
Scalability is the system ability to cope with increased load

- throughput: the number of records we can process per second.
- latency: is the duration that a request is waiting to be handled
- response time: besides the actual time to process the request, it includes network delays and queueing delays.
- Mean is not a good metric to determine the typical response time, because it doesn't tell you how many users actually experienced that delay. It is best to use percentiles.
- Percentile: a scale that indicates the percent of a distribution that is equal to or below it.
	- p99 response time is 1 second -> it means 99% of the request takes less than 1 second.
	- Percentiles are often used in service level objectives (SLOs) and service level agreements (SLAs)


Tail Latency amplification

When several backend calls are needed to serve a request, it takes just a single slow backend request to slow down the entire end-user request.

### Maintainability
In essence, it's about making life better for the engineering and operations teams who need to work with the system. Good abstractions can help reduce complexity and make the system easier to modify and adapt for new use cases. Good operability means having good visibility into the system's health and having effective ways of maning it.


**Operability**: Make it easy for operations teams to keep the system running smoothly

**Simplicity**: Make it easy for new engineers to understand the system, removing as much complexity as possbile from the system.

**Evolvability**: Make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change. Also known as extensibility, modifiability, or plasticity.




## Chapter 2 - Data Models and Query Languages

> The limit of my language mean the limits of my world.

Ludwig Wittgenstein, Tractatus Logico-Philosophicus (1922)

