---
title: "AWS SQS"
description: 
aliases: 
tags: 
draft: "true"
created-date: "2025-10-19"
---



Amazon SImple Queue Service

There are two types of SQS queues, **standard** and **FIFO**.

Standard queues support **at-least-once message delivery**, and FIFO queues support **exactly-once message processing** and **high-throughput mode.**

**at-least-once delivery**: Amazon SQS stores copies of your messages on multiple servers for redundancy and high availability. On rare occasions, one of the servers that stores a copy of a message might be unavailable when you receive or delete a message.

If this occurs, the copy of the message isn't deleted on the server that is unavailable, and you might get that message copy again when you receive messages. Design your applications to be idempotent (they should not be affected adversely when processing the same message more than once). 

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
