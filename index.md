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


# Object Storage in the IBM Cloud

Object storage is storage for the cloud.  Essentially a key-value store, files (or any binary data) are given an identifying key (or name) and stored as an 'object' in a uniquely named 'bucket' or 'container'. This allows for highly scalable storage where the only information you need to retrieve your data is the name of the object and the bucket where it's stored.
In addition to {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.cloud_notm}} currently provides several object storage offerings for different user needs, all of which are accessible through web-based portals and REST APIs.

| Offering                                   | Interface | Defining advantage                             | Docs |
|--------------------------------------------|-----------|------------------------------------------------|------|
| {{site.data.keyword.cos_full_notm}}        | COS API   | Ideal for cloud-native development and provides strong integration with IBM Cloud Services, including Data Science Experience. Most new projects should use this to make use of IBM Cloud IAM, Key Protect, and other new features as they become available. | [Link](/docs/services/cloud-object-storage/index.html) |
| IBM Cloud Object Storage (infrastructure)  | COS API   | This version provides certain regulatory compliance only available when purchasing through IBM Cloud Infrastructure (SoftLayer).  Does not support IBM Cloud IAM or Key Protect. | [Link](/docs/infrastructure/ibm-cos/index.html) |
| OpenStack Swift (infrastructure)           | Swift API | In addition to using the OpenStack Swift API, this version is available outside of the standard set of IBM Cloud regions. | [Link](/docs/infrastructure/objectstorage-swift/index.html) |
| OpenStack Swift (Cloud Foundry)            | Swift API | This is the original OpenStack Swift object storage that was provided through Bluemix as a Cloud Foundry service. | [Link](/docs/services/ObjectStorage/index.html) |
