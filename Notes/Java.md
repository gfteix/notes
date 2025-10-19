---
title: Java
description:
aliases:
tags:
draft: "true"
created-date: 2025-10-17
---
**Servlet**:  Jakarta Servlet is a Java class in Jakarta EE that conforms to the Jakarta Servlet API, a standard for implementing Java classes that respond to requests.
A Servlet  is an object that receives a request and generates a response based on that request.

**Tomcat**: A web container is responsible for managing the lifecycle of servlets, mapping a URL to a particular servlet and ensuring that the URL requester has the correct access-rights. A web container handles requests to servlets,

- Before Servlet 3.0 specificatin (Tomcat 7.0) -> Configuring the **web.xml** to map a servlet to the url was the only option
- After servlet 3.0 -> the **@WebServlet** annotation can be used to map any servlet to one or more URL patterns.

Servlet can be packed in WAR files 

.jar files: The .jar files contain libraries, resources and accessories files like property files.

.war files: The war file contains the web application that can be deployed on any servlet/jsp container. The .war file contains jsp, html, javascript and other files necessary for the development of web applications.


