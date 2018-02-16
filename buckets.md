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


# Bucket operations

---
title: API reference
keywords:
last_updated: November 18, 2016
tags:
summary:
sidebar: crs_api_sidebar
permalink: api-reference
redirect_from:
  - /crs-api-reference
  - /crs-api-reference.html
folder: api-reference
toc: false
---

### Overview

The IBM Cloud Object Storage implementation of the S3 API supports the most commonly used subset of Amazon S3 API operations. A complete list of supported operations can be found in the [API overview]({{ site.baseurl }}/about-compatibility-api).

{% include note.html content="This reference documentation is being continously improved. If you have technical questions about using the API in your application, please post them on StackOverflow using both `ibm-bluemix` and `object-storage` tags and we will do our best to answer promptly, and then improve this documentation thanks to your feedback." %}

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

### Error Codes

| Error Code | Description | HTTP Status Code |
| --- | ---| --- |
| AccessDenied | Access Denied | 403 Forbidden |
| AccessDenied | Access Denied - Server-Side Encryption with Customer-Provided Keys is not enabled for this vault. | 403 Forbidden |
| BadDigest | The Content-MD5 you specified did not match what we received. | 400 Bad Request |
| BucketAlreadyExists | The requested bucket name is not available. The bucket namespace is shared by all users of the system. Please select a different name and try again. | 409 Conflict |
| BucketNotEmpty | The bucket you tried to delete is not empty. | 409 Conflict |
| CredentialsNotSupported | This request does not support credentials. | 400 Bad Request |
| EntityTooSmall | Your proposed upload is smaller than the minimum allowed object size. | 400 Bad Request |
| EntityTooLarge | Your proposed upload exceeds the maximum allowed object size. | 400 Bad Request |
| IncompleteBody | You did not provide the number of bytes specified by the Content-Length HTTP header. | 400 Bad Request |
| IncorrectNumberOfFilesInPostRequest | POST requires exactly one file upload per request. | 400 Bad Request |
| InlineDataTooLarge | Inline data exceeds the maximum allowed size. | 400 Bad Request |
| InternalError | We encountered an internal error. Please try again. | 500 Internal Server Error |
| InvalidAccessKeyId | The AWS access key Id you provided does not exist in our records. | 403 Forbidden |
| InvalidArgument | Invalid Argument | 400 Bad Request |
| InvalidArgument | Requests specifying Server-Side Encryption with Customer-Provided Keys must be made over a secure connection. | 400 Bad Request |
| InvalidArgument | Requests specifying Server-Side Encryption with Customer-Provided Keys must provide an appropriate secret key. | 400 Bad Request |
| InvalidArgument | Requests specifying Server-Side Encryption with Customer-Provided Keys must provide the client calculated MD5 of the secret key. | 400 Bad Request |
| InvalidArgument | The MD5 hash of the secret key was improperly encoded. The MD5 hash must be Base64 encoded.| 400 Bad Request |
| InvalidArgument | The calculated MD5 hash of the key did not match the hash that was provided. | 400 Bad Request |
| InvalidBucketName | The specified bucket is not valid. | 400 Bad Request |
| InvalidBucketState | The request is not valid with the current state of the bucket. | 409 Conflict |
| InvalidDigest | The Content-MD5 you specified is not valid. | 400 Bad Request |
| InvalidEncryptionAlgorithmError | The Encryption request you specified is not valid. Supported value: AES256. | 400 Bad Request |
| InvalidLocationConstraint | The specified location constraint is not valid. For more information about regions, see How to Select a Region for Your Buckets. | 400 Bad Request |
| InvalidObjectState | The operation is not valid for the current state of the object. | 403 Forbidden |
| InvalidPart | One or more of the specified parts could not be found. The part might not have been uploaded, or the specified entity tag might not have matched the part's entity tag. | 400 Bad Request |
| InvalidPartOrder | The list of parts was not in ascending order. Parts list must specified in order by part number. | 400 Bad Request |
| InvalidRange | The requested range cannot be satisfied. | 416 Requested Range Not Satisfiable |
| InvalidRequest | Please use AWS4-HMAC-SHA256. | 400 Bad Request |
| InvalidRequest | The object was stored using a form of Server-Side Encryption. The correct parameters must be provided to retrieve the object. | 400 Bad Request |
| InvalidRequest | The encryption parameters are not applicable to this object. | 400 Bad Request |
| InvalidRequest | The object was stored using a form of Server-Side Encryption. The correct parameters must be provided to retrieve the object. | 400 Bad Request |
| InvalidSecurity | The provided security credentials are not valid. | 403 Forbidden |
| InvalidURI | Couldn't parse the specified URI. | 400 Bad Request |
| KeyTooLong | Your key is too long. | 400 Bad Request |
| MalformedACLError | The XML you provided was not well-formed or did not validate against our published schema. | 400 Bad Request |
| MalformedPOSTRequest | The body of your POST request is not well-formed multipart/form-data. | 400 Bad Request |
| MalformedXML | This happens when the user sends malformed xml (xml that doesn't conform to the published xsd) for the configuration. The error message is, "The XML you provided was not well-formed or did not validate against our published schema." | 400 Bad Request |
| MaxMessageLengthExceeded | Your request was too big. | 400 Bad Request |
| MaxPostPreDataLengthExceededError | Your POST request fields preceding the upload file were too large. | 400 Bad Request |
| MetadataTooLarge | Your metadata headers exceed the maximum allowed metadata size. | 400 Bad Request |
| MethodNotAllowed | The specified method is not allowed against this resource. | 405 Method Not Allowed |
| MissingContentLength | You must provide the Content-Length HTTP header. | 411 Length Required |
| MissingRequestBodyError | This happens when the user sends an empty xml document as a request. The error message is, "Request body is empty." | 400 Bad Request |
| NoSuchBucket | The specified bucket does not exist. | 404 Not Found |
| NoSuchKey | The specified key does not exist. | 404 Not Found |
| NoSuchUpload | The specified multipart upload does not exist. The upload ID might be invalid, or the multipart upload might have been aborted or completed. | 404 Not Found |
| NotImplemented | A header you provided implies functionality that is not implemented. | 501 Not Implemented |
| OperationAborted | A conflicting conditional operation is currently in progress against this resource. Try again. | 409 Conflict |
| PreconditionFailed | At least one of the preconditions you specified did not hold. | 412 Precondition Failed |
| Redirect | Temporary redirect. | 307 Moved Temporarily |
| RequestIsNotMultiPartContent | Bucket POST must be of the enclosure-type multipart/form-data. | 400 Bad Request |
| RequestTimeout | Your socket connection to the server was not read from or written to within the timeout period. | 400 Bad Request |
| RequestTimeTooSkewed | The difference between the request time and the server's time is too large. | 403 Forbidden |
| SignatureDoesNotMatch | The request signature we calculated does not match the signature you provided. Check your AWS secret access key and signing method. For more information, see REST Authentication and SOAP Authentication for details. | 403 Forbidden |
| ServiceUnavailable | Reduce your request rate. | 503 Service Unavailable |
| SlowDown | Reduce your request rate. | 503 Slow Down |
| TemporaryRedirect | You are being redirected to the bucket while DNS updates. | 307 Moved Temporarily |
| TooManyBuckets | You have attempted to create more buckets than allowed. | 400 Bad Request |
| UnexpectedContent | This request does not support content. | 400 Bad Request |
| UnresolvableGrantByEmailAddress | The email address you provided does not match any account on record. | 400 Bad Request |
| UserKeyMustBeSpecified | The bucket POST must contain the specified field name. If it is specified, check the order of the fields. | 400 Bad Request |
| VaultQuotaExceeded | The capacity used on the target vault has exceeded a hard quota | 507 Insufficient Storage |

### Operations on the Account
{: #operations-on-service}

#### List buckets belonging to an account

A `GET` issued to the endpoint root returns a list of buckets owned by the requesting account.  This operation does not make use of operation specific headers, query parameters, or payload elements.

##### Syntax

```bash
GET https://{endpoint}/
```

##### Sample request

```http
GET / HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160822T030815Z
Authorization: {authorization-string}
```

##### Sample response

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ListAllMyBucketsResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <Owner>
        <ID>{access-key}</ID>
        <DisplayName>{access-key}</DisplayName>
    </Owner>
    <Buckets>
        <Bucket>
            <Name>bucket-27200-lwx4cfvcue</Name>
            <CreationDate>2016-08-18T14:21:36.593Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-27590-drqmydpfdv</Name>
            <CreationDate>2016-08-18T14:22:32.366Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-27852-290jtb0n2y</Name>
            <CreationDate>2016-08-18T14:23:03.141Z</CreationDate>
        </Bucket>
        <Bucket>
            <Name>bucket-28731-k0o1gde2rm</Name>
            <CreationDate>2016-08-18T14:25:09.599Z</CreationDate>
        </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

----

<!--
#### View the storage class of buckets belonging to an account

A `GET` issued to the endpoint root with the `pagination` query parameter returns a list of buckets associated with the requesting account along with their storage class (shown as `LocationConstraint`).

##### Syntax

```bash
GET https://{endpoint}/?pagination=
```

##### Sample request

```http
GET /?pagination= HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160822T030815Z
Authorization: {authorization-string}
```

##### Sample response

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<ListAllMyBucketsResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <Owner>
        <ID>{account-id}</ID>
        <DisplayName>{account-id}</DisplayName>
    </Owner>
    <Buckets>
        <Bucket>
            <Name>bucket-27200-lwx4cfvcue</Name>
            <CreationDate>2016-08-18T14:21:36.593Z</CreationDate>
            <LocationConstraint>us-standard</LocationConstraint>
        </Bucket>
        <Bucket>
            <Name>bucket-27590-drqmydpfdv</Name>
            <CreationDate>2016-08-18T14:22:32.366Z</CreationDate>
            <LocationConstraint>us-standard</LocationConstraint>
        </Bucket>
        <Bucket>
            <Name>bucket-27852-290jtb0n2y</Name>
            <CreationDate>2016-08-18T14:23:03.141Z</CreationDate>
            <LocationConstraint>us-cold</LocationConstraint>
        </Bucket>
        <Bucket>
            <Name>bucket-28731-k0o1gde2rm</Name>
            <CreationDate>2016-08-18T14:25:09.599Z</CreationDate>
            <LocationConstraint>us-vault</LocationConstraint>
        </Bucket>
    </Buckets>
</ListAllMyBucketsResult>
```

----

-->

### Operations on Buckets
{: #operations-on-buckets}

#### Create a new bucket

A `PUT` issued to the endpoint root followed by a string will create a bucket using that string for a name.  Bucket names must be unique, and storage instances are limited to 100 buckets.  Bucket names are required to be DNS-compliant; names must be between 3 and 63 characters long must be made of lowercase letters, numbers, and dashes. Bucket names must begin and end with a lowercase letter or number.  Bucket names resembling IP addresses are not allowed, although dot characters (`.`) are permitted. This operation does not make use of operation specific headers or query parameters.

{% include custom/locations.md %}

##### Syntax

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

#### Optional payload elements

If an XML block specifying a `LocationConstraint` is provided it must correspond with a valid provisioning code (e.g. `us-standard`).  If the request payload is left empty, the default provisioning code is used.

```xml
<CreateBucketConfiguration>
  <LocationConstraint>{provisioning-code}</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample request

This is an example of creating a new bucket called 'images'.

```http
PUT /images HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160821T052842Z
Authorization:{authorization-string}
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:45:25 GMT
X-Clv-Request-Id: dca204eb-72b5-4e2a-a142-808d2a5c2a87
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: dca204eb-72b5-4e2a-a142-808d2a5c2a87
Content-Length: 0
```

----

#### Create a Vault bucket

To create a Vault bucket, send an XML block specifying a bucket configuration with a `LocationConstraint` of `us-vault` in the body of a `PUT` request to a bucket endpoint.  Note that standard bucket [naming rules]({{ site.baseurl }}/api-reference#create-a-new-bucket) apply.

{% include custom/locations.md %}

##### Syntax

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-vault</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample request

This is an example of creating a new bucket called 'vault-images'.

```http
PUT /vault-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```
```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-vault</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

----

#### Create a Cold Vault bucket

To create a Vault bucket, send an XML block specifying a bucket configuration with a `LocationConstraint` of `us-cold` in the body of a `PUT` request to a bucket endpoint.  Note that standard bucket [naming rules]({{ site.baseurl }}/api-reference#create-a-new-bucket) apply.

{% include custom/locations.md %}

##### Syntax

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-cold</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample request

This is an example of creating a new bucket called 'cold-vault-images'.

```http
PUT /cold-vault-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```
```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-cold</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

----

#### Create a Flex bucket

To create a Flex bucket, send an XML block specifying a bucket configuration with a `LocationConstraint` of `us-flex` in the body of a `PUT` request to a bucket endpoint.  Note that standard bucket [naming rules]({{ site.baseurl }}/api-reference#create-a-new-bucket) apply.

{% include custom/locations.md %}

##### Syntax

```shell
PUT https://{endpoint}/{bucket-name} # path style
PUT https://{bucket-name}.{endpoint} # virtual host style
```

```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-flex</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample request

This is an example of creating a new bucket called 'flex-images'.

```http
PUT /flex-images HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20170317T175217Z
x-amz-content-sha256: {hashed-request-body}
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 110
```
```xml
<CreateBucketConfiguration>
  <LocationConstraint>us-flex</LocationConstraint>
</CreateBucketConfiguration>
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Fri, 17 Mar 2017 17:52:17 GMT
X-Clv-Request-Id: b6483b2c-24ae-488a-884c-db1a93b9a9a6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
Content-Length: 0
```

<!--

----

#### Retrieve a bucket's storage class

A `GET` issued to a bucket with the proper parameters will return the storage class for that bucket.  This operation does not make use of operation specific headers, additional query parameters, or payload elements.

##### Syntax

```bash
HEAD https://{endpoint}/{bucket-name}?location= # path style
HEAD https://{bucket-name}.{endpoint}?location= # virtual host style
```

##### Sample request

This is an example of fetching the headers for the 'images' bucket.

```http
GET /images?location= HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160821T052842Z
Authorization:{authorization-string}
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 24 May 2017 17:46:35 GMT
X-Clv-Request-Id: 0c2832e3-3c51-4ea6-96a3-cd8482aca08a
Accept-Ranges: bytes
Server: Cleversafe/3.10.138
X-Clv-S3-Version: 2.5
Content-Length: 151
```

```xml
<LocationConstraint xmlns="http://s3.amazonaws.com/doc/2006-03-01/">us-flex</LocationConstraint>
```

-->

----

#### Retrieve a bucket's headers

A `HEAD` issued to a bucket resource will return the headers for that bucket. This operation does not make use of operation specific headers, query parameters, or payload elements.

##### Syntax

```bash
HEAD https://{endpoint}/{bucket-name} # path style
HEAD https://{bucket-name}.{endpoint} # virtual host style
```

##### Sample request

This is an example of fetching the headers for the 'images' bucket.

```http
HEAD /images HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160821T052842Z
Authorization:{authorization-string}
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:46:35 GMT
X-Clv-Request-Id: 0c2832e3-3c51-4ea6-96a3-cd8482aca08a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: 0c2832e3-3c51-4ea6-96a3-cd8482aca08a
Content-Length: 0
```

----

#### List objects in a given bucket

A `GET` request addressed to a bucket returns a list of objects, limited to 1,000 at a time and returned in non-lexographical order. The `StorageClass` value that is returned in the response is a default value as storage class operations are not implemented in COS. This operation does not make use of operation specific headers or payload elements.

##### Syntax

{% include note.html content="Note that the 'version 2' method of listing objects within a bucket is not supported, and the 'version 1' syntax is needed." %}

```bash
GET https://{endpoint}/{bucket-name} # path style
GET https://{bucket-name}.{endpoint} # virtual host style
```

##### Optional query parameters

Name | Type | Description
--- | ---- | ------------
`prefix` | string | Constrains response to object names beginning with `prefix`.
`delimiter` | string | Groups objects between the `prefix` and the `delimiter`.
`encoding-type` | string | If unicode characters that are not supported by XML are used in an object name, this parameter can be set to `url` to properly encode the response.
`max-keys` | string | Restricts the number of objects to display in the response.  Default and maximum is 1,000.
`marker` | string | Specifies the object from where the listing should begin, in UTF-8 binary order.

##### Sample request

This request lists the objects inside the "apiary" bucket.

```http
GET /apiary HTTP/1.1
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
X-Amz-Date: 20160822T225156Z
Authorization: {authorization-string}
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 24 Aug 2016 17:36:24 GMT
X-Clv-Request-Id: 9f39ff2e-55d1-461b-a6f1-2d0b75138861
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.115
X-Clv-S3-Version: 2.5
x-amz-request-id: 9f39ff2e-55d1-461b-a6f1-2d0b75138861
Content-Type: application/xml
Content-Length: 909
```
```xml
<ListBucketResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Name>apiary</Name>
  <Prefix/>
  <Marker/>
  <MaxKeys>1000</MaxKeys>
  <Delimiter/>
  <IsTruncated>false</IsTruncated>
  <Contents>
    <Key>drone-bee</Key>
    <LastModified>2016-08-25T17:38:38.549Z</LastModified>
    <ETag>"0cbc6611f5540bd0809a388dc95a615b"</ETag>
    <Size>4</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
  <Contents>
    <Key>soldier-bee</Key>
    <LastModified>2016-08-25T17:49:06.006Z</LastModified>
    <ETag>"37d4c94839ee181a2224d6242176c4b5"</ETag>
    <Size>11</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
  <Contents>
    <Key>worker-bee</Key>
    <LastModified>2016-08-25T17:46:53.288Z</LastModified>
    <ETag>"d34d8aada2996fc42e6948b926513907"</ETag>
    <Size>467</Size>
    <Owner>
      <ID>{account-id}</ID>
      <DisplayName>{account-id}</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
  </Contents>
</ListBucketResult>
```

----

#### Delete a bucket

A `DELETE` issued to an empty bucket deletes the bucket. After deleting a bucket the name will be held in reserve by the system for 10 minutes, after which it will be released for re-use.  *Only empty buckets can be deleted.* This operation does not make use of operation specific headers, query parameters, or payload elements.

##### Syntax

```bash
DELETE https://{endpoint}/{bucket-name} # path style
DELETE https://{bucket-name}.{endpoint} # virtual host style
```

##### Sample request

```http
DELETE /images HTTP/1.1
Host: s3-api.us-geo.objectstorage.softlayer.net
x-amz-date: 20160822T064812Z
Authorization: {authorization-string}
```

The server responds with `204 No Content`.

If a non-empty bucket is requested for deletion, the server responds with `409 Conflict`.

##### Sample request

```http
DELETE /apiary HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20160825T174049Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

##### Sample response

```xml
<Error>
  <Code>BucketNotEmpty</Code>
  <Message>The bucket you tried to delete is not empty.</Message>
  <Resource>/apiary/</Resource>
  <RequestId>9d2bbc00-2827-4210-b40a-8107863f4386</RequestId>
  <httpStatusCode>409</httpStatusCode>
</Error>
```

----

#### Create an access control list for a bucket

A `PUT` issued to a bucket with the necessary query parameter creates or replaces an access control list (ACL) for that bucket.  Access control lists allow for granting different sets of permissions to different storage accounts using the account's ID, or by using a pre-made ACL.

{% include important.html content="Credentials are generated for each storage account, not for individual users.  As such, ACLs do not have the ability to restrict or grant access to a given user, only to a storage account. However, `public-read-write` allows any other COS storage account to access the resource, as well as the general public. " %}

ACLs can use pre-made permissions sets (or 'canned ACLs') or be customized in the body of the request. Pre-made ACLs are specified using the `x-amz-acl` header and custom ACLs are specified using XML in the request payload. Only one method (header or payload) can be used in a single request.

This operation does not make use of additional operation specific query parameters.

ACL grantees must be other COS storage instances, and their UUID can be found along with credentials in the web portal.


The assigned permissions behave as follows:

| Permission | When granted on a bucket | When granted on an object |
|------------|--------------------------|---------------------------|
| READ | Allows grantee to list and read all objects in bucket | Allows grantee to read object data and metadata |
| WRITE | Allows grantee to create, overwrite and delete any object in bucket. Cannot be granted independently from READ permission. | N/A |
| READ_ACP | This permission does not exist for buckets; default setting is FULL_CONTROL | Allows grantee to read object ACL |
| WRITE_ACP | Default setting is FULL_CONTROL | Allows grantee to write ACL for applicable object |
| FULL_CONTROL | Allows grantee READ, WRITE, READ_ACP and WRITE_ACP permissions on bucket | Allows grantee READ, READ_ACP and WRITE_ACP permissions on object |

**Note:** The ``READ_ACP``, ``WRITE_ACP``, and ``FULL_CONTROL`` permissions are implied by the bucket “own” permission. When any of these permissions are assigned to a grantee in a bucket ACL, that grantee will be granted the bucket “own” permission.

The following canned ACLs are supported by IBM COS.  Values not listed below are not supported.

| Canned ACL | Applies to | Notes |
|------------|------------|-----------|
| private | Bucket and object | When set on a bucket, the requestor is interpreted as the bucket owner. |
| public-read | Bucket and object | When set on a bucket, the requestor is interpreted as the bucket owner. |
| public-read-write | Bucket and object | When set on a bucket, the requestor is interpreted as the bucket owner. |
| authenticated-read  | Bucket and object | Supported when set on an object only. Not supported as a bucket ACL. |

{% include note.html content="`READ` access, including `public-read`, when granted on a bucket does not allow for the actual access of objects themselves, only the ability to list them." %}

##### Syntax

```bash
PUT https://{endpoint}/{bucket-name}?acl= # path style
PUT https://{bucket-name}.{endpoint}?acl= # virtual host style
```

##### Sample request Basic pre-made ACL

This is an example of specifying a pre-made ACL to allow for `public-read` access to the "apiary" bucket. This allows any storage account to view the bucket's contents and ACL details.

```http
PUT /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
x-amz-acl: public-read
Host: s3-api.us-geo.objectstorage.softlayer.net
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Tue, 4 Oct 2016 19:03:55 GMT
X-Clv-Request-Id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Content-Length: 0
```

##### Sample request Custom ACL

This is an example of specifying a custom ACL to allow for another user using their username to view the ACL for the "apiary" bucket, but not to list objects stored inside the bucket. A third account is given full access to the same bucket as another element of the same ACL.  All authenticated users of the system can list objects in the bucket.

```http
PUT /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Owner>
    <ID>{owner-storage-account-uuid}</ID>
    <DisplayName>OwnerDisplayName</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{first-grantee-storage-account-uuid}</ID>
        <DisplayName>Grantee1DisplayName</DisplayName>
      </Grantee>
      <Permission>READ_ACP</Permission>
    </Grant>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{second-grantee-storage-account-uuid}</ID>
        <DisplayName>Grantee2DisplayName</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Tue, 4 Oct 2016 19:03:55 GMT
X-Clv-Request-Id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 73d3cd4a-ff1d-4ac9-b9bb-43529b11356a
```

----

#### Retrieve the access control list for a bucket

A `GET` issued to a bucket with the proper parameters retrieves the ACL for a bucket. This operation does not make use of operation specific headers, additional query parameters, or payload elements.

##### Syntax

```bash
GET https://{endpoint}/{bucket-name}?acl= # path style
GET https://{bucket-name}.{endpoint}?acl= # virtual host style
```

##### Sample request

This is an example of retrieving a bucket ACL.

```http
GET /apiary?acl= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 14:14:34 GMT
X-Clv-Request-Id: eb57e60e-d84e-4237-b18a-be9c2bb0deb8
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: eb57e60e-d84e-4237-b18a-be9c2bb0deb8
Content-Type: application/xml
Content-Length: 550
```

```xml
<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Owner>
    <ID>{owner-storage-account-uuid}</ID>
    <DisplayName>{owner-storage-account-uuid}</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="CanonicalUser">
        <ID>{owner-storage-account-uuid}</ID>
        <DisplayName>{owner-storage-account-uuid}</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy>
```

----

#### List canceled/incomplete multipart uploads for a bucket

A `GET` issued to a bucket with the proper parameters retrieves information about any canceled or incomplete multipart uploads for a bucket. This operation does not make use of operation specific headers, additional query parameters, or payload elements.

##### Syntax

```bash
GET https://{endpoint}/{bucket-name}?uploads= # path style
GET https://{bucket-name}.{endpoint}?uploads= # virtual host style
```

**Parameters**

Name | Type | Description
--- | ---- | ------------
`prefix` | string | Constrains response to object names beginning with `{prefix}`.
`delimiter` | string | Groups objects between the `prefix` and the `delimiter`.
`encoding-type` | string | If unicode characters that are not supported by XML are used in an object name, this parameter can be set to `url` to properly encode the response.
`max-uploads` | integer | Restricts the number of objects to display in the response.  Default and maximum is 1,000.
`key-marker` | string | Specifies from where the listing should begin.
`upload-id-marker` | string | Ignored if `key-marker` is not specified, otherwise sets a point at which to begin listing parts above `upload-id-marker`.

##### Sample request

This is an example of retrieving all current canceled and incomplete multipart uploads.

```http
GET /apiary?uploads= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

##### Sample response (no multipart uploads in progress)

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:22:27 GMT
X-Clv-Request-Id: 9fa96daa-9f37-42ee-ab79-0bcda049c671
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 9fa96daa-9f37-42ee-ab79-0bcda049c671
Content-Type: application/xml
Content-Length: 374
```

```xml
<ListMultipartUploadsResult xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Bucket>apiary</Bucket>
  <KeyMarker/>
  <UploadIdMarker/>
  <NextKeyMarker>multipart-object-123</NextKeyMarker>
  <NextUploadIdMarker>0000015a-df89-51d0-2790-dee1ac994053</NextUploadIdMarker>
  <MaxUploads>1000</MaxUploads>
  <IsTruncated>false</IsTruncated>
  <Upload>
    <Key>file</Key>
    <UploadId>0000015a-d92a-bc4a-c312-8c1c2a0e89db</UploadId>
    <Initiator>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Initiator>
    <Owner>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2017-03-16T22:09:01.002Z</Initiated>
  </Upload>
  <Upload>
    <Key>multipart-object-123</Key>
    <UploadId>0000015a-df89-51d0-2790-dee1ac994053</UploadId>
    <Initiator>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Initiator>
    <Owner>
      <ID>d4d11b981e6e489486a945d640d41c4d</ID>
      <DisplayName>d4d11b981e6e489486a945d640d41c4d</DisplayName>
    </Owner>
    <StorageClass>STANDARD</StorageClass>
    <Initiated>2017-03-18T03:50:02.960Z</Initiated>
  </Upload>
</ListMultipartUploadsResult>
```

----

#### List any cross-origin resource sharing configuration for a bucket

A `GET` issued to a bucket with the proper parameters retrieves information about cross-origin resource sharing (CORS) configuration for a bucket. This operation does not make use of operation specific headers, additional query parameters, or payload elements.

##### Syntax

```bash
GET https://{endpoint}/{bucket-name}?cors= # path style
GET https://{bucket-name}.{endpoint}?cors= # virtual host style
```

##### Sample request

This is an example of listing a CORS configuration on the "apiary" bucket.

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

##### Sample response No CORS configuration set

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:20:30 GMT
X-Clv-Request-Id: 0b69bce1-8420-4f93-a04a-35d7542799e6
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 0b69bce1-8420-4f93-a04a-35d7542799e6
Content-Type: application/xml
Content-Length: 123
```

```xml
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/"/>
```

----

#### Create a cross-origin resource sharing configuration for a bucket

A `PUT` issued to a bucket with the proper parameters creates or replaces a cross-origin resource sharing (CORS) configuration for a bucket. Note that in addition to a SHA256 hash of the body, a `Content-MD5` header is required as well. This operation does not make use of operation specific headers or additional query parameters.

##### Syntax

```bash
PUT https://{endpoint}/{bucket-name}?cors= # path style
PUT https://{bucket-name}.{endpoint}?cors= # virtual host style
```

#### Optional payload elements

In the XML block defining the key CORS elements (`AllowedOrigin` and `AllowedMethod`) there are two optional elements that can be optionally specified.

| Element | Description |
| --- | --- |
| MaxAgeSeconds | Time in seconds that the browser will cache the response to the pre-flight OPTIONS request for the specified resource. |
| ExposeHeader | Defines specific headers that will be exposed to external applications. |

##### Sample request

This is an example of adding a CORS configuration that allows requests from `www.ibm.com` to issue `GET`, `PUT`, and `POST` requests to the bucket.

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
x-amz-content-sha256: 2938f51643d63c864fdbea618fe71b13579570a86f39da2837c922bae68d72df
Content-MD5: GQmpTNpruOyK6YrxHnpj7g==
Content-Type: text/plain
Host: s3-api.us-geo.objectstorage.softlayer.net
Content-Length: 237
```

```xml
<CORSConfiguration>
  <CORSRule>
    <AllowedOrigin>http:www.ibm.com</AllowedOrigin>
    <AllowedMethod>GET</AllowedMethod>
    <AllowedMethod>PUT</AllowedMethod>
    <AllowedMethod>POST</AllowedMethod>
  </CORSRule>
</CORSConfiguration>
```

##### Sample response

```http
HTTP/1.1 200 OK
Date: Wed, 5 Oct 2016 15:39:38 GMT
X-Clv-Request-Id: 7afca6d8-e209-4519-8f2c-1af3f1540b42
Accept-Ranges: bytes
Server: Cleversafe/3.9.0.129
X-Clv-S3-Version: 2.5
x-amz-request-id: 7afca6d8-e209-4519-8f2c-1af3f1540b42
Content-Length: 0
```

----

#### Delete any cross-origin resource sharing configuration for a bucket

A `DELETE` issued to a bucket with the proper parameters creates or replaces a cross-origin resource sharing (CORS) configuration for a bucket.

##### Syntax

```bash
DELETE https://{endpoint}/{bucket-name}?cors= # path style
DELETE https://{bucket-name}.{endpoint}?cors= # virtual host style
```

##### Sample request

This is an example of deleting a CORS configuration for a bucket.

```http
GET /apiary?cors= HTTP/1.1
Authorization: {authorization-string}
x-amz-date: 20161011T190354Z
Host: s3-api.us-geo.objectstorage.softlayer.net
```

The server responds with `204 No Content`.
