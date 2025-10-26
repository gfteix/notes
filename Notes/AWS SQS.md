---
title: AWS SQS
description:
aliases:
tags:
  - tech
draft: "true"
created-date: 2025-10-19
---
Amazon Simple Queue Service

There are two types of SQS queues, **standard** and **FIFO**.

- Use standard queues to send data between applications when throughput is crucial.
- Use FIFO queues to send data between applications when the order of events is important.

## Standard 
**Unlimited throughput** – Standard queues support a very high, nearly unlimited number of API calls per second, per action.

**At-least-once delivery** – Guaranteed at-least-once delivery, meaning that every message is delivered at least once, but in some cases, a message may be delivered more than once due to retries or network delays. It is important to design the applications to be idempotent (they should not be affected adversely when processing the same message more than once). 

**Best-effort ordering** – Provides best-effort ordering, meaning that while Amazon SQS attempts to deliver messages in the order they were sent, it does not guarantee this. In some cases, messages may arrive out of order.

**Durability and redundancy** – Standard queues ensure high durability by storing multiple copies of each message across multiple AWS Availability Zones.

**Visibility timeout** – Amazon SQS allows you to configure a visibility timeout to control how long a message stays hidden after being received, ensuring that other consumers do not process the message until it has been fully handled or the timeout expires.

## Fifo 
**High throughput** – FIFO queues support up to 300 messages per second, per API action without batching, or 3,000 with batching

**Exactly-once processing** – FIFO queues deliver each message once and keep it available until you process and delete it

**First-in-first-out delivery** – FIFO queues ensure that you receive messages in the order they are sent within each message group. By distributing messages across multiple groups, you can process them in parallel while still maintaining the order within each group.


## SQS - Lambda Integration

- Lambda Services reads messages in batches and it process up to 5 messages at once.
- Each batch goes to an invocation of an function, the messages in the batch becomes hidden from other consumers for the duration of the queue visibility timeout settings
- When the lambda successfully process the batch, the lambda services deletes that batch from the Queue
- If the functions returns an error or it doesn't respond, the messages in the batch becomes visible again -> NOTE: **IF ANY MESSAGE IN THE BATCH FAILS ALL MESSAGES IN THE BATCH BECOMES VISIBLE IN THE QUEUE AGAIN**
- Some messages can be processed more than once
- Lambda should handle partial failures and manually remove the sucessfull message from the queue

https://docs.aws.amazon.com/lambda/latest/dg/example_serverless_SQS_Lambda_batch_item_failures_section.html

```typescript
import { SQSEvent, SQSBatchResponse, Context, SQSBatchItemFailure, SQSRecord } from 'aws-lambda';

export const handler = async (event: SQSEvent, context: Context): Promise<SQSBatchResponse> => {
    const batchItemFailures: SQSBatchItemFailure[] = [];

    for (const record of event.Records) {
        try {
            await processMessageAsync(record);
        } catch (error) {
            batchItemFailures.push({ itemIdentifier: record.messageId });
        }
    }

    return {batchItemFailures: batchItemFailures};
};
```

- As a good practice, configure a DLQ in the source queue to receive messages that failed continually
