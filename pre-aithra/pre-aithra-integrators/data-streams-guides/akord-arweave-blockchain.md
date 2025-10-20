# Akord - Arweave blockchain

## Introduction

[Akord](https://akord.com/) is an app, API, SDK and CLI enabling permanent data storage on the Arweave blockchain with one upfront payment.&#x20;

Akord vaults can be used to store any data – images, videos, documents, audio, even websites and applications. After uploading a file, an Arweave gateway URL will be available (it normally takes 5-15 minutes for files to be committed on-chain), enabling the[ minting of a data NFT](https://docs.itheum.io/product-docs/product/data-dex/minting-a-data-nft).

Below are different options for uploading assets and obtaining the Arweave gateway URL using the app and API.

## Upload with the Akord app

1\. [Create your account](https://v2.akord.com/signup) in a few minutes. Get 100 MB of free blockchain storage to test your workflow.

2\. Select “NFT assets” when you login as the template for creating your first vault:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXddrOKELCqyk3o_KVTUgZzbnfA8ffC-cYteyooSjr3xUqjlcHf0NGLeZSZd8bkX4owr8IFJbSfVPGkygx7aMLPGAVj9NZrZbl99xc6IDd4BMlXOXkvM63j6sDUbMelv30NHqv6SUM1LxPESjvFSHboVM2qG?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>



3. Give your vault a name and optionally add a description and tag, which can help your vault be discovered on-chain in the future:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXdOcG52TjsVPV8vvEFH0RdAvKtRH0gKVrtgnxhaohRASN4OAbWZr_5y0VGR53u9ZAZCvBunpqpd87eOjq0dNAmcrKS8Uu4BPTGel9mgzQUTR_qX04Mb3Az0a04WQGBDmWy52yjWhRiY367o_31uCspsfI0?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

4. Drag and drop your assets into the main vault window or select the files by clicking “Upload a file”:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXfUBQv7r3SJIPc5YhXrOFcnFlB8wB5hEv0IiD0cnIu9KIPj7dzuaKg10Ok2jTJUbwgf6adUez9CAFWMYvj6cK30GHJj-GraG9BCFmENyENrfP9liE_ppyKqGX4QbT4ayB8gc8PpK68vi5-MOe-okXA6-IY?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

5. Click the info icon on the right side of the row once the file is uploaded to the vault:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXeD-1qfieC-_mxCNZoA4R83Ms34X9e2ne0B81ULu5XUt3C-dJqgZ00WVnGgWIsesYrBB0BsTGAF-IKcZvjq7qu3UR9fI1FD2vYByOfhHBtFMAP0yvYUma4m8BL_PFfnQ0BcjO-VuWDoKQdf2fOx4nXJC7Kx?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

6. Get an Arweave gateway URL. There are two options – akrd.net, Akord’s own gateway, or arweave.net, another popular gateway in the ecosystem:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXfZWvEK4mmg0Hfkt4fhTavD_SBwbj-3WAXKUV9hOCTRXfGHzFZdfkDzNG27mFWoYHvQVQMYvvb9GPj_8BOhOQzVRG8s81L73uA0OxD22ptMG4Byc5GdCiSL6edUmTrm24l5RgtARLP-fpELbx3HC9vajvW2?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

* Note that once the file is uploaded it takes a few moments to reflect on the Decentralized storage file explorer.
* Upon copying the URL kindly place it in a new tab/window to check if the file is accessible.

<figure><img src="../../../.gitbook/assets/image (115).png" alt=""><figcaption></figcaption></figure>

This URL can now be used for Data NFT minting.&#x20;

7. Generate a manifest if you have multiple NFTs (optional).

If you’re uploading many assets, you can generate an Arweave manifest that will contain all transaction IDs in one JSON.

Click “Create JSON metadata” link in the top right of the vault, and select the Arweave manifest option

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXcjwH0h_fu-eDg-oruIF38Pj3f2xf-O0h5ytmQ2NE7f1xibKF56bn46Q-HoJwzAxXt-stsKTj1coO8EppfUWl52VuziVYi90aWbHYk_Ev2LU7Nl-rzoeGzGuzbIJrg_LlRWAiGz7OrsL0BhCMRZ9pZRj3w?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

The generated manifest.json will look like this with all transaction IDs listed for any file in the vault:

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXdj0vC9tIvP1qXil3M9waQTX4LjympuRdPQh4ltb2f52_ablVKF2t13ow5hnOOmsnjI9x351rR69wyrSyubEMGSDkfKO2uLmTnK4Uf5gm-lOENrSKTMGna2ugQz41Bkp-eXXBYuxRPU4CKLYEYcR34zXE5T?key=ED0qkWeun-F8aJUWm45Tow" alt=""><figcaption></figcaption></figure>

All gateways follow the same scheme: https://{gateway host}/{tx-id}

You’ll also find Akord documentation on how to [generate a manifest with the CLI](https://docs.akord.com/nft-projects/get-the-arweave-urls/generate-a-manifest-cli), along with[ a script for generating Arweave gateway URLs](https://docs.akord.com/nft-projects/get-the-arweave-urls/using-a-script) without using a manifest file.

These Arweave gateway URLs can be used for Data NFT minting.



### Simple API upload

Using this method, you can use the Akord API to upload to arweave.

1\. [Create your account](https://v2.akord.com/signup) in a few minutes. Get 100 MB of free blockchain storage to test your workflow.

2\. [Get your API key here](https://v2.akord.com/account/developers).

3\. A simple API method in JavaScript:&#x20;

```
// Javascript

const fs = require('fs').promises;
const data = await fs.readFile('/path/to/your/file.txt', 'utf8'); //nodejs specific

const response = await fetch('https://api.akord.com/files', {
    method: 'POST',
    headers: {
        'Accept': 'application/json',
        'Api-Key': 'your_api_key',
        'Content-Type': 'text/plain'
    },
    body: data
})

```

\
**More API documentation**

For code snippets in Bash and Python, example responses, and upload methods with tags and larger multipart upload guidelines, [check out the Akord docs](https://docs.akord.com/nft-projects/upload-with-app-api-or-cli/use-the-api-to-upload).&#x20;

## The End Result

Upon implementing the above steps, the final result will look like this.&#x20;

{% embed url="https://www.youtube.com/watch?v=LgRhwXyhPNU" %}
