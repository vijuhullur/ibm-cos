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


# About COS (infrastructure)

Information stored with {{site.data.keyword.cos_full}} is encrypted and dispersed across multiple geographic locations, and accessed over HTTP using a REST API. This service makes use of the distributed storage technologies provided by the {{site.data.keyword.cos_full_notm}} System (formerly Cleversafe).

{{site.data.keyword.cos_full_notm}} is available with three types of resiliency: Cross Region, Regional, and Single Data Center.  Cross Region provides higher durability and availability than using a single region at the cost of slightly higher latency, and is available today in the US and EU. Regional service reverses those tradeoffs, and distributes objects across multiple availability zones within a single region, and is available in the US South and US East regions. If a given region or availability zone is unavailable, the object store continues to function without impediment.  Single Data Center distributes objects across multiple machines within the same physical location.

Developers use an {{site.data.keyword.cos_full_notm}} API to interact with their object storage. This documentation provides support to [get started](/docs/cloud-object-storage/index.html#getting-started-console-) with provisioning accounts, to create buckets, to upload objects, and to use a reference of common API interactions.
