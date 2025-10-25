---
title: Request-Reply Pattern
description:
aliases:
tags:
  - tech
draft: "true"
created-date: 2025-10-25
---
When two applications communicate via Messaging, the communication is one-way. The applications may want a two-way conversation.


Send a pair of Request-Reply messages, each on its own channel.

Request-Reply has two participants:
- Requestor – Sends a request message and waits for a reply message.
- Replier – Receives the request message and responds with a reply message.
