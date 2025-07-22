---
title: Idempotency In System Integrations
description: 
aliases:
  - Idempotency
tags:
  - tech
created-date: 2025-01-16
---


# Idempotency 

Idempotency  is the property of certain operations in mathematics and computer science whereby they can be applied multiple times without changing the result beyond the initial application.


## HTTP

An HTTP method is idempotent if the intended effect on the server of making a single request is the same as the effect of making several identical requests.


Of the major HTTP methods, GET, PUT, and DELETE should be implemented in an idempotent manner according to the standard, but POST doesn't need to be


*Note that the idempotence of a method is not guaranteed by the server and some applications may incorrectly break the idempotence constraint.


## Building Idempotent services in the context of system integrations

Let's imagine that we need to integrate an Order from System A to System B.
Every time an Order is created in System A a message is sent to the Integration Service that migrates the data to System B.

How could we make sure our Integration Service is idempotent, that is, how can we assure that if I send two identical requests it will not generate a duplicate order on System B?

Scenarios:

1. "System B" is a database that we own and we can control its model
2. "System B" is a third party API that provides idempotent mechanisms
3. "System B" is a third party API that is not idempotent

While we could try to prevent duplicate messages directly on System A (e.g., by enforcing one-time queue messages), let’s assume we only control the Integration Service.

### "System B" is a database that we own and we control its model

Easy peasy:
1. If there is an **unique** indifier coming from System A, such as the System A Order Id, we can create a field with an UNIQUE constraint on the database to store the identifier.
2. The service should try to get the record using the new field before creating
3. If not found it should create the record passing the unique indentifier to the proper field.

Even in case of concurrent requests the RDBMS has its own mechanisms to prevent two rows with the same unique field, and it would prevent duplicates. 

Note that this would not be guaranteed if the field on the database doesn't have the unique constraint, as in case of concurrent requests (race conditions) step 2 could not return an existing record for both executions, resulting in multiple inserts.


### "System B" is a third party API that provides idempotent mechanisms

Some systems - usually financial ones - like Zuora or Stripe provides a idempotency-key in their endpoints that are not idempotent by default, so the client can set a key to prevent duplicates in case of concurrency requests or retries.

### "System B" is a third party API that is not idempotent

In this case, if we have a unique key or a sort of idempotency key coming from System A we can try to implement our own idempotent approach before sending any data to System B.

- Use Redis (or any other in-memory db) to track the processing state of each request.
- On receiving a request:
    - Check Redis for the idempotency key.
    - If not found:
        - Write the key to Redis with a "processing" state.
        - Check System B (if it supports reads) to see if the record already exists:
            - If yes → return the found record.
            - If no → create the record on System B.
        - Store the response in Redis.
    - If found:
        - Return the cached response from Redis.

Note: A proper TTL should be set in redis, to make sure the cache is clean after a while.



