# Troubleshooting

### Troubleshooting&#x20;

#### 1. AWS Configuration Issues

If you open a new domain link and the you see that AWS S3 throws the following errors, then there is more likely some configuration issues. The following may help you debug.\
\
**ERROR: NoSuchKey**

Error:

```
404 Not Found

- Code: NoSuchKey
- Message: The specified key does not exist.
- Key: index.html
- RequestId: ......
- HostId: ......
```

Reason: the specified index or error file is not there. Double check your settings and the files in the bucket. But index.html is not really needed, but you may see that an error related to the data assets that you uploaded.



**ERROR: NoSuchBucket**

Error:

```
404 Not Found

- Code: NoSuchBucket
- Message: The specified bucket does not exist
- BucketName: dataassets.alice-datanft-bucket.com
- RequestId: ......
- HostId: ......
```

Reason: the bucket name does not match your domain name; set your bucket name to `dataassets.alice-datanft-bucket.com`



**ERROR: NoSuchWebsiteConfiguration**

Error:

```
404: Not Found

- Code: NoSuchWebsiteConfiguration
- Message: The specified bucket does not have a website configuration
- BucketName: dataassets.alice-datanft-bucket.com
- RequestId: 1C661A36E8D467EB
- HostId: q7grWdZIyMJOw1Oc94nrrNteMpQu52Q154rLHHP02Tr9FAt8U71LAkUeVS0EuA+Y9JoHket/O2k=
```

Reason: Static Website Hosting is not enabled.



#### Other Common Issues

ERROR:&#x20;

You update your data assets in AWS S3 via the automated Github based scripts mentioned in [storage-aws-s3](../storage-aws-s3/ "mention") or manually in a S3 bucket, but the Data Stream URL is still showing the old version of a file.\
\
REASON: This is most likely caused by caching on the Cloudflare level if you are using Cloudflare as per [task-3-use-cloudflare-to-connect-your-domain-name-to-your-s3-bucket-securely.md](task-3-use-cloudflare-to-connect-your-domain-name-to-your-s3-bucket-securely.md "mention") or caching on any other Content Distribution Network (CDN) or web hosting provider. To solve this issue, you will need to turn off the cache. Instructions for Cloudflare as described here[#step-5-disable-cache-on-cloudflare](task-3-use-cloudflare-to-connect-your-domain-name-to-your-s3-bucket-securely.md#step-5-disable-cache-on-cloudflare "mention")

