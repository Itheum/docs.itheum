# Task 3: Use Cloudflare to connect your Domain Name to your S3 Bucket securely

In task 2, we created a "**static website hosting**" friendly AWS S3 bucket to host our data assets and uploaded our data assets into this bucket like so:

<figure><img src="../../../../../.gitbook/assets/image (93).png" alt=""><figcaption></figcaption></figure>

### Step 1: Find the AWS S3 Website URLs for your bucket and data assets

These data assets are now publicly available via internal "**AWS S3 website URLs**," and we need to know these URLs to continue with the steps.

To find the "**AWS S3 website URLs**" on your AWS S3 bucket, navigate to the "**Properties"** tab of your bucket and down to the  **“Static website hosting,”** and you will see the following "**Bucket website endpoint.**"

<figure><img src="../../../../../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

Click on this link, and it should open a new tab with this URL and the following error message.

<figure><img src="../../../../../.gitbook/assets/image (95).png" alt="" width="563"><figcaption></figcaption></figure>

This error means it could not find a default "index.html" file, as we may not have uploaded it (as we don't need it for our Data Stream). But, if you append the paths (folder + file name) of the files we uploaded in the S3 bucket, we can view these files publicly. Let's do that now; in our example, the files paths would be like so:

* `http://dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com/file_storage/stream_1.json`
* `http://dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com/file_storage/stream_2.svg`

And when you open these links, you should see both your JSON and SVG files.

<figure><img src="../../../../../.gitbook/assets/image (96).png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (98).png" alt="" width="563"><figcaption></figcaption></figure>

So we now have public URLs for our files, but these URLs are not secure (they don't support https://), and they are not hosted behind our new domain name. Let's use Cloudflare to get this done and complete our process.

### Step 2: Sign up for a free Cloudflare account

Cloudflare is a leading content and security platform that provides many features, and best of all, its **free version** is all we need. When writing this guide, there was also no requirement for a credit card to sign up.\
\
Head over to [https://www.cloudflare.com/](https://www.cloudflare.com/) and sign up for a new account with you email.\
\
Once you signup, you will be taken to the dashboard, and you should see a "Get Started" button somewhere on the screen like this.

<figure><img src="../../../../../.gitbook/assets/image (99).png" alt="" width="563"><figcaption></figcaption></figure>

Enter the new "**Domain Name**" you procured as part of [task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md](task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md "mention")

<figure><img src="../../../../../.gitbook/assets/image (100).png" alt="" width="563"><figcaption></figcaption></figure>

Select the "**Free Plan**" and click on Continue.

<figure><img src="../../../../../.gitbook/assets/image (101).png" alt="" width="563"><figcaption></figcaption></figure>

### Step 3: Import your Domain's DNS settings into Cloudflare

Cloudflare will then begin importing your Domain Name's DNS records (the configuration settings for your domain name) into Cloudflare's system. You will see a similar (not the same) screen if it can detect your domain via your registrar. Click on **Continue**.

<figure><img src="../../../../../.gitbook/assets/image (102).png" alt="" width="563"><figcaption></figcaption></figure>

In the next step, Cloudflare will ask you to change the "nameservers" in your domain registrar (e.g., namecheap, GoDaddy, etc.). This is the action that moves the DNS records over to Cloudflare.

{% hint style="info" %}
Important: ONLY do this step if your domain name is new. There may be unintended consequences if you do this with a domain name already hosting some websites. This guide is for people using a new domain name to mint Data NFTs.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (88).png" alt="" width="375"><figcaption><p>Copy the Cloudflare nameservers from here</p></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (89).png" alt="" width="563"><figcaption><p>In this example, the domain name is with Namecheap and we copy Cloudflare's name servers to here</p></figcaption></figure>

Once you update the **nameservers**, it may take time for Cloudflare to complete the DNS import, and when it's a success, you will see a similar message on the Cloudflare dashboard.

<figure><img src="../../../../../.gitbook/assets/image (90).png" alt="" width="563"><figcaption></figcaption></figure>

### Step 4: Add a new CNAME record to complete the connection of your domain name with S3

In **step 1** above, we discovered that the "**Bucket website endpoint**" for our S3 bucket was&#x20;

`dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com`

This was in our example, your  "**Bucket website endpoint**" will of course be different.



And we had a full url to our **Data Stream** link so:

`http://dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com/file_storage/stream_1.json`\
\
In [task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md](task-1-use-a-domain-name-to-sit-in-front-of-your-aws-s3-bucket-public-url.md "mention") we obtained the domain name `https://alice-datanft-bucket.com`

In [#step-1-find-the-aws-s3-website-urls-for-your-bucket-and-data-assets](task-3-use-cloudflare-to-connect-your-domain-name-to-your-s3-bucket-securely.md#step-1-find-the-aws-s3-website-urls-for-your-bucket-and-data-assets "mention") we decided that we intend to host our data assets in a subdomain `https://dataassets.alice-datanft-bucket.com`

So that our current Data Stream link:

`http://dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com/file_storage/stream_1.svg`\
\
Can become:

`https://dataassets.alice-datanft-bucket.com/file_storage/stream_2.svg`

This can be achieved by setting up a new CNAME record in Cloudflare's DNS that point the "**dataassets**" subdomain to the S3 bucket's website endpoint host.

```
Record Type: CNAME
Name: dataassets (the subdomain of your main domain)
Target: dataassets.alice-datanft-bucket.com.s3-website-ap-southeast-2.amazonaws.com (only the host name of your "Bucket website endpoint")
TTL: Auto (or similar)
```

Click on "**Add Record**" and create a new **CNAME** with the relevant details and click on "**Save**"

<figure><img src="../../../../../.gitbook/assets/image (91).png" alt="" width="563"><figcaption></figcaption></figure>

Once this has been done, it may take some time for the **CNAME** to apply. But once it's done, you should be able to view your new AWS S3-based data stream link behind your domain name. e.g., `https://dataassets.alice-datanft-bucket.com/file_storage/stream_2.svg`

<figure><img src="../../../../../.gitbook/assets/image (92).png" alt="" width="563"><figcaption></figcaption></figure>

### Step 5: Disable cache on Cloudflare&#x20;

As we will use automated scripts to keep the data assets updated on AWS S3, and now that we have Cloudflare sitting in front of our S3 bucket, there is some possibility that our S3 data assets get heavily cached by Cloudflare as it is also a Content Distribution Network (CDN) and caches content to speed up content delivery. Unfortunately, this caching behavior is not good for users trying to unlock Data NFTs to view data in a timely manner. Therefore, it is advisable to "disable" caching on Cloudfront.

We don't need to turn off ALL cache; we only need to create some Cloudfront Cache Rules to disable the specific folders (or paths) we have set up in AWS S3 that hosts our data assets for the Data Stream.

In yr Cloudflare dashboard, click on your **Site** and then to "**Caching"** and then to "**Cache Rules"**. Create a new Cache Rule. As our data assets are stored in the "**/file\_storage**" path (and S3 Bucket) we disable caching for this, like the image below. Click on "**Save**" and wait a few minutes for this rule to take effect.

<figure><img src="../../../../../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

***

**Congratulations!** And with this, you should have a fully robust, secure, flexible, and production grand Data NFT Data Stream up and running. If you need any help with this guide, please get in touch with us on [Discord's technical support channel](https://itheum.io/discord)
