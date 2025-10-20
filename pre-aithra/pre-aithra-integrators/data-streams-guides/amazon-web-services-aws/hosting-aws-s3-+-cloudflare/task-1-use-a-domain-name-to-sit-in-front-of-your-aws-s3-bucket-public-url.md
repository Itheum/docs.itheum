# Task 1: Use a domain name to "sit in front" of your AWS S3 Bucket Public URL

In the previous sections that detail how you can use AWS S3 to host your Data Streams, the guides asked you to create a new AWS S3 bucket (e.g. `alice-datanft-bucket`) for the storage of your data assets (e.g. `my-data-stream-1.json`) and then get the Public URL of the bucket. \
\
A Public URL for your S3 bucket and data asset usually looks something like this:

`https://alice-datanft-bucket.s3.ap-southeast-2.amazonaws.com/my-data-stream-1.json`

And you could directly use this S3 Bucket Public URL as a Data Stream to mint a new Data NFT. \
\
But we highly recommend you "abstract" this AWS public URL and use a custom domain name YOU own and control. By doing this, we can put our own custom domain name to sit in front of your AWS S3 bucket, allowing us to have some extra layer of protection and flexibility for your data stream. For example, remove our "dependency" on AWS S3 for data storage. This means that you can move the data assets to a new data storage service even AFTER we mint the Data NFT. This also protects you if you accidentally delete the AWS S3 bucket or lose access to your AWS account. This level of flexibility is excellent, and we highly recommend this approach. Let's get started.\


### Step 1) **Decide on the domain name and path you would like to serve your data stream**&#x20;

If your old S3 bucket's Public URL was:

`https://alice-datanft-bucket.s3.ap-southeast-2.amazonaws.com/my-data-stream-1.json`\
\
You could decide that you new domain name and path should be:\
`https://alice-datanft-bucket.com/my-data-stream-1.json`\
\
In this example, the user buys the domain alice-datanft-bucket.com and we do some updates to the domain configuration (coming up later in this guide) to redirect `https://alice-datanft-bucket.com/my-data-stream-1.json` to load the same file as `https://alice-datanft-bucket.s3.ap-southeast-2.amazonaws.com/my-data-stream-1.json`

But ultimately, the first thing you need to do is buy your new domain alice-datanft-bucket.com



### Step 2) **Buy your new domain name**

Most people know how to buy a domain name, and there are many public resources on how to do this, so detailing this again in the guide is not practical.\
\
We recommend you use your favorite domain name registrar (a service that sells domain names) to buy your domain name. \
\
If you do not have a favorite domain name registrar, then we recommend [namecheap.com](https://www.namecheap.com/domains/domain-name-search/) \
\
You can choose to buy any domain name extension you would like. e.g. `alice-datanft-bucket.com`, `alice-datanft-bucket.co`, `alice-datanft-bucket.io` etc.

But we recommend you pick a domain name extension with a high reputation, not something obscure and cheap. This is because obscure or unknown domain name extensions may be run by companies who may discontinue the domain name extension, and you will lose access to this domain name at any time.\
\
`.com` is the most reputed domain name so we recommend you use this.



### **Step 3) Make sure to auto-renew your domain name**

All domain names expire, so you must renew your domain name to ensure you continue owning it. It would be best if you did this to prevent losing access to your domain name should it expire and someone else buying it from the market and becoming the owner of your Data Streams.&#x20;

Most domain name registrars like namecheap.com offer an "auto-renew" feature like this, so please make sure you use it to have peace of mind.

<figure><img src="../../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

You can now proceed to the next task as your domain name has been purchased and auto-renew enabled to protect it from expiring.

