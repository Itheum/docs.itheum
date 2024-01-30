# Manual upload of file to AWS for Data NFT Streaming

## Overview

This section provides a guide for Data NFT Minters to upload their stream/file to AWS S3 Bucket, allowing them to generate a URL for minting their Data NFT. By following these steps, users can seamlessly host their data in various formats, such as JSON, CSV, MP3, and more, on AWS.

For detailed instructions and additional information on AWS S3 setup and configuration, refer to the full documentation [Section B](https://github.com/Itheum/template-datastream-aws-s3#b-creating-an-aws-s3-bucket).

For a short summary of the instructions please visit the below.

**Steps:**

1. Creating an AWS S3 Bucket:
   * Sign in to the AWS Console and navigate to AWS S3.
   * Click on "Create bucket" and provide a unique name and region for your bucket.
   * Choose the appropriate ownership and access settings, ensuring public access is enabled.
   * Create the bucket.
2. Configuring CORS (Cross-Origin Resource Sharing):
   * In the bucket's permissions, locate "Cross-origin resource sharing (CORS)" and click on "Edit".
   * Paste the provided CORS configuration, which allows GET requests from any origin. (as mentioned in  [Section B](https://github.com/Itheum/template-datastream-aws-s3#b-creating-an-aws-s3-bucket))
   * Save the changes.
3. Uploading/Updating a File:
   * In the bucket's menu, click on "Upload" to upload a file.
   * Choose the file you want to upload, ensuring it has the desired name and extension.
   * If you need to update the file, simply overwrite the existing file with the new version of the same name and extension.
   * Note: The file has to exclusively have its read permissions enabled for public access post each upload.&#x20;
     * Browse to the file on AWS, and select the Permissions Tab.
     * In ACL (Access control list), click Edit.
     * Under Grantee "Everyone (public access)" set the Read permission to true by applying a check to the box.

Please note that AWS S3 offers a free tier for storing data up to 5GB for 12 months. You can explore custom billing plans and review AWS pricing if you require more storage.

***

### A**dditional setting needed for "Nested Streams":**

In the case that you are using [nested streams](../../../../developers/software-development-kits-sdks/data-nft-sdk/guide-3-using-nested-streams-to-access-nested-data-assets-from-a-primary-data-stream.md), you will be required to commit the following updates to the JSON file uploaded to your AWS Bucket.



&#x20;1\. Browse to the **Properties** section of your JSON file.

<figure><img src="../../../../.gitbook/assets/image (116).png" alt=""><figcaption></figcaption></figure>

&#x20;2\. Scroll down to the **Metadata** section in the properties.

* Click on Edit.
* For Type select "User defined", for the corresponding Key value enter `x-amz-meta-marshal-deep-fetch` and for the corresponding Value enter `1`.&#x20;
* Click "Add metadata"
* _This step is not mandatory, but may ben helpful to instruct the Data Marshal clearly that the file type is JSON._ For Type select "System defined", for the corresponding Key value select "Content-Type" and for the corresponding Value enter "application/json".&#x20;
* Save Changes

<figure><img src="../../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

The Data Marshal will now be able to handle nested streams for this json file. Learn more about [nested streams here](../../../../developers/software-development-kits-sdks/data-nft-sdk/guide-3-using-nested-streams-to-access-nested-data-assets-from-a-primary-data-stream.md).
