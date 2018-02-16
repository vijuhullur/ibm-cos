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


# Common error codes

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
