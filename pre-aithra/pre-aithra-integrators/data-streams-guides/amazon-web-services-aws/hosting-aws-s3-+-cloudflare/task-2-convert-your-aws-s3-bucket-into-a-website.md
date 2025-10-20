# Task 2: Convert your AWS S3 Bucket into a "website"

If you followed the guides on [storage-aws-s3](../storage-aws-s3/ "mention") and used AWS S3 to store your data assets for the Data Streams, then this section details how you can "slightly" update your processes to convert your S3 buckets into a "website".\
\
This allows you to connect the domain you now own as per your previous task [task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md](task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md "mention")to your AWS S3 bucket.

### Step 1) **Name your AWS S3 Bucket the exact same as your full domain name**

Note that in our previous Task, we procured the domain `alice-datanft-bucket.com` which we intend to use to load content from our S3 Bucket.

We recommend that you also use a **subdomain** to point to your S3 bucket as this gives you a lot more flexibility in future to grow the the content for your domain.\
\
Based on this, let's pick a subdomain called `dataassets`. So, now the full domain `dataassets.alice-datanft-bucket.com` will be setup to load content from your S3 bucket.

Let's now proceed with the naming of the AWS S3 bucket.

In the steps mentioned in [storage-aws-s3](../storage-aws-s3/ "mention") where it says **"Create an AWS S3 bucket"**, you will need to make sure to use the exact same name of your full domain as the bucket name. So, name your S3 bucket `dataassets.alice-datanft-bucket.com`

{% hint style="info" %}
Note that this above instruction is only related to the "name of the S3 bucket", you will still need to follow the other S3 bucket creation instructions mentioned here : [https://github.com/Itheum/template-datastream-aws-s3#b-creating-an-aws-s3-bucket](https://github.com/Itheum/template-datastream-aws-s3#b-creating-an-aws-s3-bucket)
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (84).png" alt=""><figcaption></figcaption></figure>



### Step 2) Enable "Static website hosting" for your bucket

Once you have created your S3 bucket, the next step is to configure it for website hosting. To do this, navigate to the "**Properties"** tab of your bucket and click on **“Static website hosting.”** Select the "**Host a static website"** option and enter an "**index document"** (a dummy index.html file will do, this file does not need to exist). Click the **“Save changes”** button to save your settings.\


<figure><img src="../../../../../.gitbook/assets/image (86).png" alt="" width="563"><figcaption></figcaption></figure>



### Step 3) Add appropriate Bucket policy&#x20;

And finally, navigate to the "**Permissions"** tab of your bucket, scroll down to the "Bucket Policy" section, click on Edit and enter the following.

**Make sure to change the bucket name in `Resource`: to match your bucket name**

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadForGetBucketObjects",
			"Effect": "Allow",
			"Principal": "*",
			"Action": "s3:GetObject",
			"Resource": "arn:aws:s3:::dataassets.alice-datanft-bucket.com/*"
		}
	]
}
```

<figure><img src="../../../../../.gitbook/assets/image (87).png" alt="" width="563"><figcaption></figcaption></figure>

Click the **“Save changes”** button to save your settings.



### Step 4) Upload your data assets to this new bucket

As per the instructions in the guides on [storage-aws-s3](../storage-aws-s3/ "mention"), you can now upload the data assets that you want to use as data NFT Data Streams into this new bucket you created.\
\
Again, we recommend that you make a new **"folder"** inside the S3 Bucket and then place the data assets in this folder, this furthermore allows for a lot of flexibility if you intend to mint multiple Data NFTs and host it all in a single AWS S3 bucket. But this is optional and you don't need to do it if you don't want to.\
\
In the screenshot below, we have created a new folder call `file_storage` inside our `dataassets.alice-datanft-bucket.com` bucket and uploaded two data assets inside it. These are the files that can be used for 2 separate Data Streams if needed, and this is the benefit of having the separate folder as described. The final Data Stream URLs for both these Data Streams will eventually be:

1. https://dataassets.alice-datanft-bucket.com/file\_storage/stream\_1.json
2. https://dataassets.alice-datanft-bucket.com/file\_storage/stream\_2.svg

<figure><img src="../../../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>



We are now ready to move onto our final step to complete this process...
