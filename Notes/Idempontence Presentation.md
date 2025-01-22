---
title: Idempontence Presentation
description: 
aliases: 
tags: 
draft: "true"
created-date: 2025-01-16
---


# Idempotency 


Idempotency  is the property of certain operations in mathematics and computer science whereby they can be applied multiple times without changing the result beyond the initial application.





$$ f(f(x)) = f(x) $$


## HTTP

An HTTP method is idempotent if the intended effect on the server of making a single request is the same as the effect of making several identical requests.


Of the major HTTP methods, GET, PUT, and DELETE should be implemented in an idempotent manner according to the standard, but POST doesn't need to be



*Note that the idempotence of a method is not guaranteed by the server and some applications may incorrectly break the idempotence constraint.



## Building Idempotent Services

- Use some sort of UNIQUE field to prevent duplicates
- If you are creating data in a database, validate if the data already exists before inserting
- Use Transactions and  `FOR UPDATE` (if updating an existing record) to prevent a bad state in case of concurrent requests 

## Building Idempotent services in the context of system integrations

The Service should integrate an Order from System A to System B.

Scenarios:

1. "System B" is a database that we own and we can control it's model
2. "System B" is a third party API that is not idempotent
3. "System B" is a third party API that provides idempotent mechanisms


## "System B" is a database that we own and we can control it's model

Easy peasy:
- If there is an unique indifier coming from System A we should create an UNIQUE field on the database to store the identifier
- The service should try to get the record using the new field before creating

Even in case of concurrent requests the SGDB has it's own mechanisms to prevent two rows with the same unique field, and it would prevent duplicates.

## "System B" is a third party API that is not idempotent

In this case, we need a unique key or a sort of idempotency key coming from the request so we can try to implement our own idempotent approach before sending any data to System B

- Use Redis
- Try to GET the idempotency key
	- if not found -> Write the idempotency key to redis with a "processing" state -> send request to System B -> Update the idempotency key to redis to have the response returned from System B
	- If found -> return the response from redis
- Note: There should be an strategy to expire the idemptotency key on redis after some time.


## "System B" is a third party API that provides idempotent mechanisms

Awesome, some systems - usually financial ones - like Zuora or Stripe provides a idempotency-key on it's endpoints that are not idempotent by default, so the client can defined the key to prevent duplicates in case of concurrency requests or retries.


