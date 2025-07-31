---
title: multipart form-data
description: 
aliases: 
tags:
  - tech
draft: "true"
created-date: 2025-07-30
---
multipart/form-data is a media/content type used in HTTP requests.

RFC: https://www.rfc-editor.org/rfc/rfc7578.html

It is very suitable for file uploads as it allows binary data to be sent along with other form data in a single request.


The body is divided into multiple sections, each representing a distinct piece of data from the form (text fields, files, etc).

Boundaries: A unique string, defined in the Content-Type header of the main HTTP request, acts as a delimiter to separate these individual parts.

Each individual part within the multipart/form-data body can have its own headers, such as Content-Type, as well as its body data.

## Example

Method: POST
Path: http://www-example.com/api/resource
Header: `Content-Type: multipart/form-data; boundary=----------abcd
Body:
```
----------abcd
Content-Disposition: form-data; name="name"

My Name
----------abcd
Content-Disposition: form-data; name="file"; filename="document.pdf"
Content-Type: application/pdf

<binary data for the pdf>
----------abcd

```

