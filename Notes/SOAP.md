---
title: "SOAP"
description: 
aliases: 
tags: 
draft: "true"
created-date: "2025-10-19"
---

SOAP is an XML message format used in web service interactions. SOAP messages are typically sent over HTTP or JMS, but other transport protocols can be used.

A SOAP message is encoded as an XML document, consisting of an `<Envelope>` element, which contains an optional `<Header>` element, and a mandatory `<Body>` element. The `<Fault>` element, contained in `<Body>`, is used for reporting errors.


**WSDL** is an XML notation for describing a web service. A WSDL definition tells a client how to compose a web service request and describes the interface that is provided by the web service provider.


To test a soap endpoint:

1. Create a file called `request.xml` that contains the SOAP request

``` 
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
				  xmlns:gs="http://spring.io/guides/gs-producing-web-service">
   <soapenv:Body>
      <gs:getCountryRequest>
         <gs:name>Spain</gs:name>
      </gs:getCountryRequest>
   </soapenv:Body>
</soapenv:Envelope>
```

2. Use CURL to send the request

```
curl --header "content-type: text/xml" -d @request.xml http://localhost:8080/ws
```

