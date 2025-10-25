---
title: "SOAP"
description: 
aliases: 
tags: 
draft: "true"
created-date: "2025-10-19"
---



To test a soap endpoint:

1. Create a file called `request.xml` that contains the SOAP request

``` 
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"
				  xmlns:gs="http://spring.io/guides/gs-producing-web-service">
   <soapenv:Header/>
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

