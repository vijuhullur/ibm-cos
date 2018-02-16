---

copyright:
  years: 2017
lastupdated: "2018-02-15"

---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}


# Common headers

### Common Headers

#### Common Request Headers
The following table describes supported common request headers. COS ignores any common headers not listed below if sent in a request, although some requests may support other headers as defined in this documentation.  More information about creating the authorization header can be found in the ["Authentication"]({{ site.baseurl }}/manage-access#authentication) section

| Header             | Note                               |
|--------------------|-------------------------------------|
| Authorization      | **Required** for all requests (AWS Signature Version 4).   |
| Host               | **Required** for all requests.                 |
| x-amz-date         | **Required** for all requests. Can also be specified as `Date`.               |
| x-amz-content-sha256 | **Required** for uploading objects or any request with information in the body. |
| Content-Length     | **Required** for uploading objects, chunked encoding also supported.    |
| Content-MD5        | A 128-bit MD5 hash value of the request body being sent.                  |
| Expect             | `100-continue` waits for the headers to be accepted before sending the body.  |
{:.opstable}

#### Common Response Headers
The following table describes common response headers.

|  Header        | Note |
|----------------|------|
| Content-Length | The length of the request body in bytes.      |
|Connection     |  Indicates whether the connection is open or closed.     |
| Date           | Timestamp of the request.     |
| ETag           | MD5 hash value of the request.     |
| Server         | Name of the responding server.     |
|X-Clv-Request-Id|  Unique identifier generated per request. |
{:.opstable}
