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


# Using a desktop client

For basic tasks, such as configuring routine backup or shared hosting for large files, there are GUI tools for accessing S3 API compatible object storage.

### Cyberduck

Cyberduck is a popular, open-source, and easy to use FTP client that is also capable of calculating the correct authorization signatures needed to connect to IBM COS.  Cyberduck can be downloaded from [cyberduck.io/](https://cyberduck.io/).

To use Cyberduck to create a connection to IBM COS and synchronize a folder of local files to a bucket, follow these steps:

 1. Download, install, and start Cyberduck.
 2. The main window of the application opens, where you can create a connection to IBM COS. Click **Open Connection** to configure a connection to IBM COS.
 3. A pop-up window opens. From the drop-down menu at the top, select "S3 storage". Enter information into the following fields, and then click Connect:

 	– Server: enter the nearest endpoint of IBM COS
 	– Access Key ID
 	– Secret Access Key

 4. Cyberduck takes you to the root of the account where buckets can be created. Right-click within the main panel and select **New Folder** (the application deals with many transfer protocols where Folder is the more common container construct). Enter the bucket name and then click Create.
 5. After the bucket is created, double-click the bucket to view it. Within the bucket you can perform various functions such as upload files to the bucket, list bucket contents, download objects from the bucket, synchronize local files to a bucket, synchronize objects to another bucket, or create an archive of a bucket.
 6. Right-click within the bucket and select **Synchronize**. A pop-up panel opens where you can browse to the folder that you want to synchronize to the bucket. Select the folder and click Choose.
 7. After you select the folder, a new pop-up panel opens. Here, a drop-down menu is available where you select the synchronization operation with the bucket. Three possible synchronize options are available from the menu:

 	– Download: This will download changed and missing objects from the bucket.
 	– Upload: This will upload changed and missing files to the bucket.
 	– Mirror: This will perform both download and upload operations, ensuring that all new and updated files and objects are synchronized between the local folder and the bucket.

 8. Another window opens to show active and historical transfer requests. After the synchronization request is complete, the main window will perform a list operation on the bucket to reflect updated content in the bucket.

### Cloudberry

Cloudberry is a flexible backup utility that allows users to back up some or all of a local filesystem to an S3 API compatible object storage system. It can be configured to be run either manually or scheduled based on need, and can backup different directories to different buckets if needed.  Cloudberry can be downloaded from [cloudberrylab.com](http://www.cloudberrylab.com/).

{% include note.html content="When configuring Cloudberry, select 'S3 Compatible' from the list of options, not 'Amazon S3' or 'SoftLayer'." %}

{% include warning.html content="The current release of the Cloudberry Client for Windows uses TLSv1.0 for establishing secure data transmission over the public Internet.  IBM Cloud requires the more modern TLSv1.1 or TLSv1.2 to establish a secure connection. Connections from the Cloudberry Client for Windows will fail unless the 'Use SSL' box is left **unchecked** during configuration." %}
