---
title: AWS CDK
description: 
aliases: 
tags:
  - tech
created-date: 2025-08-03
---

![[cdk.png]]

AWS CDK It is a software development framework for defining infrastructure. In another words: is a framework/tool that let’s you model and provision AWS Cloud resources using the programming language of your choice.

- Behind the scenes, it uses **AWS CloudFormation** to provision resources in a safe and reusable manner.




**AWS CloudFormation**: It is a AWS service that uses template files (YAML, JSON) to automate the setup of AWS resources.

**Basic Comands**

- Create a CDK project using the CDK CLI
`cdk init sample-app --langage=typescript`

`npm run build`

`cdk ls` : lists the stacks in the app

`cdk synth`: synthesize the stack to an AWS CloudFormation template (this generates a cdk.out file, containing a YAML template).


![[cdk_steps.png]]


The application is represented by the class `App` from AWS CDK and usually is the root of the tree of your constructs.

```tsx
const app = new App();
new AWSCommunityStack(app, 'cdk-2021');
app.synth();
```

## Constructs:

Constructs are the basic building blocks of AWS CDK apps. A construct represents a cloud component and encapsulates everything AWS CloudFormation needs to create the component.

For example, the s3.Bucket class represents an Amazon S3 bucket.

All constructs are implemented having the class `Construct` as base class. All the constructs can receive 3 parameters: `scope`, `id` and `props` (props is optional).

- `scope`: It is the construct in which this construct is created. In many cases, a construct is defined in the context of the current construct - the root or app (passing `this` as the first argument)
- `Id`: is the local identifier of the construct that must be unique inside the scope.
- `props`: is the object or set of initialization properties that are specific to each construct and define its initial configuration.

L1: These constructs represent all of the AWS resources that are available in AWS CloudFormation. They are named CfnXyz, where Xyz represents the name of the resource. For example, s3.CfnBucket represents the AWS::S3::Bucket CFN resource.

```tsx
const bucket = new s3.CfnBucket(this, 'uploads-bucket');
```

L2: (Higher Level) They provide the same functionality, but handle much of the details, boilerplate, and glue logic required by CFN constructs. Example: s3.Bucket

```tsx
	const myVpc = new ex2.Vpc(this, 'my-vpc', {
		cidr: '10.0.0.0/16'
	});
```

> L2 constructs, also known as _curated_ constructs, are thoughtfully developed by the CDK team and are usually the most widely used construct type. L2 constructs map directly to single AWS CloudFormation resources, similar to L1 constructs. Compared to L1 constructs, L2 constructs provide a higher-level abstraction through an intuitive intent-based API. L2 constructs include sensible default property configurations, best practice security policies, and generate a lot of the boilerplate code and glue logic for you.



L3: (Even higher-level) Patterns. These constructs are designed to help you complete common tasks in AWS, often involving multiple kinds of resources.

```tsx
	const lambdaRestApi = new apigateway.LambdaRestApi(this, 'lambda-rest-api', {
		handler: lambdaFunction }
	);
```

> L3 constructs, also known as _patterns_, are the highest-level of abstraction. Each L3 construct can contain a collection of resources that are configured to work together to accomplish a specific task or service within your application. L3 constructs are used to create entire AWS architectures for particular use cases in your application.



## Stacks

Stacks are the unit of deployment in the AWS CDK.

All AWS resources defined within the scope of a stack, either directly or indirectly, are provisioned as a single unit.

When you run the cdk synth command for an app with multiple stacks, the cloud assembly includes a separate template for each stack instance.

```tsx
const app = new App();
new MyFirstStack(app, 'stack1');
new MySecondStack(app, 'stack2);
app.synth();
```

References



https://docs.aws.amazon.com/cdk/v2/guide/home.html
[https://www.ernestchiang.com/en/notes/aws/cdk/](https://www.ernestchiang.com/en/notes/aws/cdk/)
https://docs.aws.amazon.com/cdk/v2/guide/constructs.html
[https://ibrahimcesar.cloud/blog/mergulho-cdk/](https://ibrahimcesar.cloud/blog/mergulho-cdk/)