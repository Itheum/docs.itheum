# Guide 2 : Unlocking Data NFTs via MultiversX Native Auth

This guide walks you through how to use MultiversX Native Auth to access Data Stream that are served by the Itheum protocol. Native Auth significantly improves the user experience of accessing data available within Data NFT protected Data Streams.&#x20;

### What is Native Auth?

Before we begin, we need to understand what Native Auth is. Native Auth can be thought of as the traditional "Single Sign On" experience you see with many web2 apps, where you log into a single app and remain logged into other apps that are part of the same login service (e.g., Google Login). Similarly, with MultiversX Native Auth, you can log into a single DApp using your Crypto Wallet and have this "login session" persist across all other MultiversX ecosystem DApps that can access that Native Auth "login session."

## How Native Auth Improves the Data NFT User Experience&#x20;

In Itheum, we have multiple DApps that are connected to the MultiversX blockchain (e.g., Data DEX or Itheum Explorer). With Native Auth, you can log into one of these DApps, interact with the Data Marshal (a data broker node connected to the MultiversX blockchain), seamlessly prove your web3 identity and ownership of Data NFTs, unlock it, and view the data with it. Without Native Auth, you must provide your identity multiple times in a single-user journey by signing numerous messages with your wallet. This makes the user experience feel unnatural. With Native Auth, the user experience becomes closer to the traditional website experience, bringing Itheum closer to mainstream adoption by breaking down complex web3 workflows.

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-mx-data-nft v2.1.0** or above to follow this guide.
* This guide assumes that you are integrating with Itheum via an application built on the MultiversX blockchain, you use TypeScript/JavaScript as your programming language and that you use that use the **@multiversx/sdk-core** and **@multiversx/sdk-dapp** libraries to authenticate and sign and track on-chain transactions. Although, these libraries are optional and you can use any MultiversX tooling to interact with the blockchain.

***

## Target User Story:

{% hint style="info" %}
As an integrator of Itheum web3 Data Brokerage infrastructure:

* I'd like build a simple Data NFT viewer, that let's a logged in user select specific Data NFTs and open them to view the underlying data seamlessly without having to sign any extra transactions that force the user to prove ownership of the Data NFTs
* I'd also like to build some generic handler that can parse various Data Streams like JSON, TXT, SVG, AUDIO etc so I can display the content in my app
{% endhint %}

Let's begin...

***

## Step 1: Installation of Itheum Data NFT SDK

In your NodeJS/JavaScript/TypeScript app, install the SDK `@itheum/sdk-mx-data-nft` by following the [instructions here](https://github.com/Itheum/sdk-mx-data-nft#usage-in-3rd-party-dapps). If you are using NPM then it would be.

```javascript
npm install --save @itheum/sdk-mx-data-nft
```





## Step 2: Using SDK Core to enable MultiversX Wallet Login with Native Auth Enabled

The code snippet below is just an example of how you would use the React Based `SDK Core` to drop some Wallet Login components on your DApp and configure them for Native Auth based session usage. You can choose to natively implement this as well on any other front-end using the [Native Auth Client library from MultiversX](https://github.com/multiversx/mx-sdk-js-native-auth-client). Although we find that `SDK Core` provides all that is needed to build an app fast. \
\
The below React code sample is not a complete working version, but shows the parts needed for a `SDK Core` based implementation setup for Native Auth via the [DeFi Browser Extension Wallet](../../supported-wallets/multiversx-defi-wallet.md).

{% code lineNumbers="true" fullWidth="true" %}
```javascript
import React from "react";
import { ExtensionLoginButton } from "@multiversx/sdk-dapp/UI";

function MyLoginComponent() {
  const commonProps = {
    callbackRoute: "/foobar",
    nativeAuth: {
      apiAddress: "https://devnet-api.multiversx.com",
      expirySeconds: 3000,
    },
  };

  return (
    <>
      <ExtensionLoginButton loginButtonText="DeFi Wallet" {...commonProps} />
    </>
  );
}
```
{% endcode %}

Note that the `commonProps.nativeAuth` params are important to note as you will need to match these later on when you configure `Native Auth` on Itheum's SDK in a step below.





## Step 3: Grab a Native Auth "Session Token"

As you have enabled Native Auth via `SDK Core`, the following code snippet shows you how you can obtain your Native Auth Session Token. Again, this is a `SDK Core` specific React example code snippet, you can choose to follow this or implement your custom front-end using the [Native Auth Client library from MultiversX](https://github.com/multiversx/mx-sdk-js-native-auth-client).&#x20;

{% code lineNumbers="true" fullWidth="true" %}
```javascript
import React from "react";
import { useGetLoginInfo } from "@multiversx/sdk-dapp/hooks";

function MyAppComponent() {
  const { tokenLogin } = useGetLoginInfo();
  const nativeAuthToken = tokenLogin?.nativeAuthToken;

  return <>My Native Auth Session is {nativeAuthToken}</>;
}
```
{% endcode %}





## Step 4: Open a Data NFT and "View Data" via a Native Auth session

Next, select a Data NFT and "View its Data" using the obtained Native Auth session. As detailed in the introduction of this document, as you are using Native Auth to prove your identity and, therefore, ownership of the Data NFT you are interacting with, you no longer need to sign a custom message like in the regular viewData method also available in the SDK.

In the below same React code, we get to the step of using the `Itheum Data NFT SDK` to grab a target Data NFT, get its data and then trigger a custom `View Data` method that supports Native Auth. This example builds on the previous step's code example and show how we can open a Data NFT with a JSON Data Stream.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
import React, { useState } from "react";
import { useGetLoginInfo } from "@multiversx/sdk-dapp/hooks";
import { DataNft, ViewDataReturnType } from "@itheum/sdk-mx-data-nft";

async function MyAppComponent() {
  const [showData, setShowData] = useState({});
  const { tokenLogin } = useGetLoginInfo();
  const nativeAuthToken = tokenLogin?.nativeAuthToken;

  // Specify some Data NFTs nonces that you want to fetch
  const DATA_NFT_NONCES_I_WANT_TO_OPEN = [407, 423, 453];

  try {
    /*  Here we use the SDK to fetch the Data NFTs we want to try and open for the logged in user
        note how createManyFromApi takes in a array of objects with mandatory parameter "nonce" 
        and optional parameter "tokenIdentifier" which you can use to select a separate Data NFT collection
        that you may have minted as part of Itheum Enterprise. Leaving tokenIdentifier empty will default to
        the public Data NFT-FT collection that is part of the Ithuem Protocol */
    const _nfts: DataNft[] = await DataNft.createManyFromApi(DATA_NFT_NONCES_I_WANT_TO_OPEN.map((nonce) => ({ nonce })));

    const dataNftToOpen = _nfts[0]; // from the returned set, let's open the 1st one for now just to test

    const res: ViewDataReturnType = await dataNftToOpen.viewDataViaMVXNativeAuth({
      mvxNativeAuthOrigins: ["http://localhost:3000"], // this should match the domain you are on as you run the app
      mvxNativeAuthMaxExpirySeconds: 3000, // this should match the expirySeconds value from Step 2
      fwdHeaderKeys: "authorization", // forward the authorization header to the data stream server (so it can validate the sesison and get caller address etc)
      fwdHeaderMapLookup: {
        "authorization": `Bearer ${nativeAuthToken}`,
      },
    });

    if (!res.error) {
      // if the Data Stream is JSON data this is how we grab it
      res.data = await (res.data as Blob).text();

      setShowData(JSON.parse(res.data));
    } else {
      // And Data Stream errors may end up here so you can handle them as needed
      console.error(res.error);
    }
  } catch (err) {
    // ALL Itheum Data NFT SDK errors appear here, so you can handle them as needed
    console.error(err);
  }

  return `<>JSON DATA from the Opened Data NFT is : ${JSON.stringify(showData)}</>`;
}
```
{% endcode %}

* Note that the above code will ONLY work if the logged in user owns the Data NFTs with the nonces in the `DATA_NFT_NONCES_I_WANT_TO_OPEN` array, or else you will get an error that indicates that they don't own the Data NFT.
* On \~`line 33`, we show you how you can open a JSON specific Data Stream that sits behind a Data NFT. But in reality, a Data NFT can contain a Data Stream that is in any format. So you will need some custom code to try and handle various file types. That's given next...





### Bonus Step 5: How can I parse non-JSON Data Streams?

Although this is not part of the Native Auth requirements of this guide, here is some sample code that shows you how to parse some common Data Stream types that the Itheum protocol supports. The code below is an extension to the code block shown in Step 4 and is just some sample code.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
enum BlobDataType {
  TEXT,
  IMAGE,
  AUDIO,
  SVG,
  PDF,
}

let blobDataType = BlobDataType.TEXT;
let unpackedData = null;

if (!res.error) {
  if (res.contentType.search("image") >= 0) {
    if (res.contentType == "image/svg+xml") {
      blobDataType = BlobDataType.SVG;
      unpackedData = await (res.data as Blob).text(); // parse SVG in raw data we can show inside a SVG tag
    } else {
      blobDataType = BlobDataType.IMAGE;
      unpackedData = window.URL.createObjectURL(new Blob([res.data], { type: res.contentType })); // parse IMG into a URL we can show
      
    }
  } else if (res.contentType.search("audio") >= 0) {
    res.data = 
    blobDataType = BlobDataType.AUDIO;
    unpackedData = window.URL.createObjectURL(new Blob([res.data], { type: res.contentType })); // parse Audio file into a URL we can play
  } else if (res.contentType.search("application/pdf") >= 0) {
    blobDataType = BlobDataType.PDF;
    unpackedData = window.URL.createObjectURL(new Blob([res.data], { type: res.contentType })); // parse PDF file into a URL we can open
  } else if (res.contentType.search("application/json") >= 0) {
    unpackedData = await (res.data as Blob).text(); // parse JSON file that we can use locally
    unpackedData = JSON.stringify(JSON.parse(unpackedData), null, 4);
  } else if (res.contentType.search("text/plain") >= 0) {
    unpackedData = await (res.data as Blob).text(); // parse TXT file that we can use locally
  } else {
    // we don't support that format
    unpackedData = "Sorry, this file type is currently not supported by the Explorer File Viewer. The file type is: " + res.contentType;
  }
} else {
  // And Data Stream errors may end up here so you can handle them as needed
  console.error(res.error);
}
```
{% endcode %}
