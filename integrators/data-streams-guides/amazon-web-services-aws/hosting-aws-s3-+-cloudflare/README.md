---
description: Using a Domain Name and CloudFlare to protect and serve your Data Streams
---

# Hosting : AWS S3 + Cloudflare

In the previous [storage-aws-s3](../storage-aws-s3/ "mention") section, we described how to use an AWS S3 bucket to store your data assets and use the S3 Bucket Public URL as the Data Stream to mint your Data NFT.

This approach works well enough, but there are some limitations that you will need to consider:

1. You are now tied to AWS S3 as your data storage tool for the lifetime of the Data NFT (in most cases, this will be forever as NFTs cannot be deleted once you trade them with someone else)
2. If you accidentally delete your AWS S3 bucket or your AWS account is inaccessible or compromised, then your Data NFT will no longer work. And you wont be able to "edit" the Data NFT to point to a new Data Stream that you may have produced as a replacement.

We recommend that you use AWS S3 for data storage and use the S3 Bucket Public URLs only in test environments (like Itheum Devnet), but when it comes time to mint Data NFTs on Mainnet and have your Data NFTs listed on the Data NFT Marketplace for real economic value - then we highly recommend that you do the following three tasks to ensure your Data Streams are ready for mainstream adoption and long term growth.

The following step-by-step sections will walk you through these tasks in detail.

* **Task 1:** **Use a domain name to "sit in front" of your AWS S3 Bucket Public URL**
* **Task 2:** **Convert your AWS S3 Bucket into a "website" so you can manage within it multiple Data Streams (like you would a website that has with multiple files)**
* **Task 3:** **Use a service like CloudFlare to protect your Data Streams**

Let's get started with Task 1...
