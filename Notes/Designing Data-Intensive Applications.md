---
title: Designing Data-Intensive Applications
description: 
aliases: 
tags: 
created-date: 2025-02-12
---



## Chapter 1 - Reliable, Scalable, and Maintainable Applications

> The internet was done so well that most people think of it as a natural resource like the Pactific Ocean, rather than something that was man-made. When was the last time a technology with a scale like that was so error-free?

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



**Document Databases**: ideal to store nested records (one-to-many relationships, like position, education or contact_info) within their parent record rather than in a separate table.


When it comes to representing many-to-one relationships, relational and document databases are not fundamentally different: in both cases, the related item is referenced by a unique identifier, which is called a foreign key in the relational model and a document reference in the document model

**Relational versus Document Databses today (Differences in the data model)**
Main arguments in favor of the document data model: schema flexibility, better performance due to locality, and for some applications it is closer to the data strctures used by the application.
Relational model: better support for joins, and many-to-one and many-to-many relationships.

**Which data model leads to simplet application code?** If the data in your application has a document-like structure (i.e., a tree of one-to-many relationships, where typically the entire tree is loaded at once), then it is probably a good idea to use a document model. The relational technique of shredding-splitting a document-like structure into multiple tables can lead to cumbersome schemas and unnecessary complicated application code.







