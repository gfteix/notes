---
title: Untitled
description: 
aliases: 
tags:
  - tech
draft: "true"
created-date: 2024-09-17
---

# Overview
Salesforce is a CRM (Customer Relationship Management) software.

Is the biggest CRM in the market, and probably the most versatil one, as it has several clouds that are a lot more than just a CRM such as Commerce Cloud (Demandware) - is a whole ecommerce platform, Marketing cloud - that is a marketing platform to handle mass campaings and personalized emails, etc - and much others.

Salesforce is a highly extensive software, which means there is a great industry of developer, admins and Salesforce consultants whose job is to expand and work within the platform to fufill client/business requirements.

# Tech Stuff

Salesforce has some particularities:
In order to program inside it, you have to use a proprietary language called Apex (It is similar to Java, but more limited). It has a SQL like query language called SOQL. It has a frontend framework simillar to react called LWC https://github.com/salesforce/lwc - that curiosaly is open source.

Salesforce also supports a lot of low code automations - its main one is called Flow.
They call low code solutions as declarative (do not confuse with declaritive programming, the paradigm).

In Salesforce you don't have tables you have objects. There are several standard object that comes with every Salesforce org by default, such as Account, Contact, Lead, Opportunity, etc.

Salesforce started first as a CRM sales related features, this is what they called SalesCloud today. In SalesCloud you are able to generate leads (potencial clients), and convert these leads to a contact/acconunt and opportunity (an opportunity of a sale or a deal), with the build in functionality and the standard objects it is possible to automate a company sales process.

## Permissions Management
- Profile
- Permission Set
- Custom Permissions
- Running users of apex/flows

## Apex

## Flow
There are different types of flows:
- Record Trigger flows
	- Simillar to a database trigger, you can define the entry criteria (e.g When an Account with type Customer is created) and add your business logic on it
- Autolaunched flows
	- Flows that can be reused accross other flows, simillar to a reusable functions
- Screen Flows
	- Flows that have interactive screens (e.g show some inputs to be filled by the user, after it a new record is created)


It's possible to add fault paths in flow elements to run some operation when a step failed. Example: you have a flow that Get's a specified account and then updates the account name. It's possible to add a fault path to both elements, so in case any of them fails you can create a log or send an email to monitore it.

Rollbacks inside flows:
- If you add a Fault path to a flow element Salesforce doesn't rollback the transaction, it only executes the fault path
- No fault path -> it rollbacks the transaction
- Alternatives -> use platform event with publish imediataly to create a log and then trigger the rollback manually.


Calling Apex inside flows:

- When an error ocurrs in an apex that is called by a flow the stack trace is not showed in the flow debug (and it is not returned in the flow error message). In order to return it in the flow level it is necessay to create a custom exception inside the apex and rethrow the exception with the custom one.


## LWC


## Limitations


## API
- Rest API
- SOAP API?
- Composite API
- Limits


## Platform Event - An event driven approach


### Using the coposite API to send multiple events


### Using Platform Event Triggers to consume events



