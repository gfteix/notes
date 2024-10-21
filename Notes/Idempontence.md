---
created-date: 2024-10-13
title: Idempontence
description: 
aliases: 
tags: 
draft: "true"
---

https://www.youtube.com/watch?v=4OuaONkZw1I
https://www.confluent.io/blog/exactly-once-semantics-are-possible-heres-how-apache-kafka-does-it/

https://www.linkedin.com/pulse/kafka-idempotent-consumer-transactional-outbox-rob-golder/
https://en.wikipedia.org/wiki/Idempotence

https://www.berkansasmaz.com/every-programmer-should-know-idempotency/


https://developer.salesforce.com/blogs/engineering/2013/01/implementing-idempotent-operations-with-salesforce

https://queue.acm.org/detail.cfm?id=2187821
https://developer.salesforce.com/docs/atlas.en-us.integration_patterns_and_practices.meta/integration_patterns_and_practices/integ_pat_remote_call_in.htm




Idempotent capabilities guarantee that repeated invocations are safe and won’t have a negative effect. If idempotency isn’t implemented, then repeated invocations of the same message can have different results, potentially resulting in data integrity issues, for example, creation of duplicate records, duplicate processing of transactions, and so on.

https://stripe.com/blog/idempotency

Networks are unreliable.

To overcome this sort of inherently unreliable environment, it’s important to design APIs and clients that will be robust in the event of failure, and will predictably bring a complex integration to a consistent state despite them.

The easiest way to address inconsistencies in distributed state caused by failures is to implement server endpoints so that they’re idempotent, which means that they can be called any number of times while guaranteeing that side effects only occur once.

When a client sees that a network operation has failed, there’s a good chance that it’s due to an intermittent failure that will be gone by the next retry. However, there’s also a chance that it’s a more serious problem that’s going to be more tenacious; for example, if the server is in the middle of an incident that’s causing hard downtime. Not only will retries of the operation not go through, but they may contribute to further degradation.

It’s usually recommended that clients follow something akin to an [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff) algorithm as they see errors. The client blocks for a brief initial wait time on the first failure, but as the operation continues to fail, it waits proportionally to `2^n`, where _n_ is the number of failures that have occurred. By backing off exponentially, we can ensure that clients aren’t hammering on a downed server and contributing to the problem.

>Considering the possibility of failure in a distributed system and how to handle it is of paramount importance in building APIs that are both robust and predictable. Retry logic on clients and idempotency on servers are techniques that are useful in achieving this goal and relatively simple to implement in any technology stack.
>
>Here are a few core principles to follow while designing your clients and APIs:
>
>**Make sure that failures are handled consistently**. Have clients retry operations against remote services. Not doing so could leave data in an inconsistent state that will lead to problems down the road.
>**Make sure that failures are handled safely**. Use idempotency and idempotency keys to allow clients to pass a unique value and retry requests as needed.
>**Make sure that failures are handled responsibly**. Use techniques like exponential backoff and random jitter. Be considerate of servers that may be stuck in a degraded state.



https://www.alexhyett.com/idempotency/

### Implementing idempotency - Corner cases

Useally the way to implement idempotency is to have the client sending a unique id. 

**Hash of the request body**
Another option is to hash the body of the request and use that as your unique identifier. However, you need to be sure if you are doing this that there is no reason the person would want to send exactly the same request again. There should be something about the combination of fields that makes it unique.
If someone orders a SpongeBob beach towel and then 30 seconds later orders another SpongeBob beach towel you don't know that this is a duplicate order, they might just really like SpongeBob.

**Same idempotency-key accross different clients**
With a user-supplied idempotency key, you can't guarantee that what they send you is going to be globally unique. They could end up giving you the same idempotency key as another user or the same key for multiple endpoints.

So it is important that you combine the idempotency key with a user ID and the API path that has been used.


**Idempotency Storage**
To implement idempotency you need to store your combined idempotency key somewhere along with the successful response that you send the user.

If a request with the same idempotency key comes in, instead of doing the operation you simply return the response that you sent out before. As far as the user is concerned the operation was successful and they don't need to know that you are sending them the previous response.

Typically this is done using some form of Key Value storage such as Redis or Dynamo DB.


How long you store your idempotency keys and responses really depends on your application. If it is just to prevent the user from sending a request twice due to a double click then 10 minutes or so might be ok. Generally, from what I have seen people store idempotency keys for around 24-48 hours.

However, if you have an event-based system where you might want to replay events that happened months ago then obviously your idempotency keys will need to last longer.

If you are using Redis or DynamoDB you can set the Time To Live or TTL on the items so they are deleted automatically for you.

**Same idempotency-key by mistake**

If a request comes in from the same user, for the same endpoint with the same idempotency key as a previous request we are assuming it is just a duplicate.

However, there is a chance that the user has used the same idempotency key by mistake and the body of the request is actually very different.

If you need to protect against this scenario then you can take a hash of the request body and then store that alongside the idempotency key and response and return an error if the request is different.




Companies that have idempotence-key in their API: Mercado Pago, Stripe, Zuora, Shopify