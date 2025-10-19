# Guide 1 : Minting a Custom Data NFT Collection with Authenticated Data Streams (via SDK)

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-mx-data-nft v2.1.0** or above to follow this guide.
* This guide also is specific to the **MuiltiversX Blockchain** and provides code samples that use the **@multiversx/sdk-core** and **@multiversx/sdk-dapp** libraries to authenticate and sign and track on-chain transactions. Although, these libraries are optional and you can use any MultiversX tooling to interact with the blockchain.

***

In this detailed SDK guide, we will walk you through the process on:

1. Minting a Custom Data NFT Collection
2. Protecting Data Streams with Authentication

But to make the guide more practical, let's first detail the a real-world user story that we will aim to achieve by following this guide.\


## Target User Story:

{% hint style="info" %}
As an integrator of Itheum web3 Data Brokerage infrastructure:

* I'd like to use the SDK to mint a 5,000 Data NFT collection.&#x20;
* This collection should have its own image (not the Itheum generative image service).&#x20;
* The Data Streams on the Data NFTs should also be fully non-public and implement authentication via a `Bearer` token header (based on our backend authentication requirements).&#x20;
* The Data Stream should also be customizable, where they can read a session of a user (address, tokenID) and provide some level of runtime customization before streaming out.
{% endhint %}

Let's begin...

***

## Step 1: Installation of Itheum Data NFT SDK

In your NodeJS/JavaScript/TypeScript app, install the SDK `@itheum/sdk-mx-data-nft` by following the [instructions here](https://github.com/Itheum/sdk-mx-data-nft#usage-in-3rd-party-dapps). If you are using NPM then it would be.

```javascript
npm install --save @itheum/sdk-mx-data-nft
```





## Step 2: Minting your Data NFT Collection

We are now going to use the SDK to mint a new 5,000 Data NFT Collection. On `Devnet` you can do this without any issues, but on `Mainnet`, [you will need to be "whitelisted" to mint (as part of CanaryNet requirements)](https://medium.com/itheum-newsletter/the-whitelisting-process-is-now-live-apply-to-mint-your-data-as-nfts-on-itheums-data-marketplace-799361c15099)

We will assume that you are integrating with Itheum on the MultiversX Blockchain so we provide some helper code from the MultiversX SDKs as well to demonstrate a complete solution that can get you started quick.



### A) **Import and initialize your libraries required for Minting**

{% code lineNumbers="true" fullWidth="true" %}
```javascript
// Itheum SDK's Minter Import (used to mint Data NFTs)
import { SftMinter } from "@itheum/sdk-mx-data-nft";

// Itheum SDK Minter initialization
const dataNftMinter = new SftMinter("devnet"); // or "mainnet"

// MultiversX Imports (need to interact with the Blockchain)
import { Address, Transaction } from "@multiversx/sdk-core/out";
import { sendTransactions } from "@multiversx/sdk-dapp/services";
import { refreshAccount } from "@multiversx/sdk-dapp/utils/account";
```
{% endcode %}



### B) Mint a "Regular" Data NFT Collection&#x20;

A "Regular" Data NFT collection uses Itheum's Image Generative Service and Traits Engine to automatically generate random NFT images for you that look similar to these:

<figure><img src="../../../.gitbook/assets/image (12).png" alt="" width="375"><figcaption></figcaption></figure>

This "Regular" type of Data NFT is the most straightforward to produce and can be minted with the following code:

<pre class="language-javascript" data-line-numbers data-full-width="true"><code class="lang-javascript"><strong>try {
</strong><strong>    // we need to 1st get the live anti-spam minting tax requirement from the smart contract
</strong><strong>    const requirements = await dataNftMinter.viewMinterRequirements(new Address(address));
</strong><strong>    const antiSpamTax = requirements?.antiSpamTaxValue;
</strong><strong>
</strong><strong>    const mintTransaction: Transaction = await dataNftMinter.mint(
</strong><strong>        new Address(address),
</strong><strong>        "MY_GM_DATA", // Short token Name (between 3 and 20 alphanumeric characters - no spaces)
</strong><strong>        "https://data_marshal_URL.com", // The Data Marshal endpoint
</strong><strong>        "https://data_stream_URL.com/protected_data_stream", // The Data Stream URL
</strong><strong>        "https://data_preview_URL.com", // The public Data Preview URL
</strong><strong>        1500, // Royalty in % with 2 trailing zeros (e.g. 1500 is 15% or 500 would be 5% or 0 would be 0%. Max is 5000 of 50%)
</strong><strong>        5000, // Collection size (max supply)
</strong><strong>        "My Gaming Data", // Title (between 10 and 60 alphanumeric characters with spaces allowed)
</strong><strong>        "My PlayStation gaming data in JSON format", // Description (between 10 and 400 alphanumeric characters with spaces allowed)
</strong><strong>        antiSpamTax, // Live Anti Spam Tax value
</strong><strong>        {
</strong><strong>          nftStorageToken: "XXX" // Your nft.storage token
</strong><strong>        }
</strong><strong>    );
</strong><strong>
</strong><strong>    await refreshAccount();
</strong><strong>
</strong><strong>    const { sessionId, error } = await sendTransactions({
</strong><strong>        transactions: mintTransaction,
</strong><strong>        transactionsDisplayInfo: {
</strong><strong>          processingMessage: "Minting Standard Data NFT",
</strong><strong>          errorMessage: "Data NFT minting error",
</strong>          successMessage: "Data NFT minted successfully",
        },
<strong>        redirectAfterSign: false,
</strong><strong>    });
</strong><strong>} catch(e) {
</strong><strong>    console.log("Minting Standard Data NFT FAILED");
</strong><strong>    console.error(e);
</strong><strong>}
</strong><strong>
</strong></code></pre>



**There are a few things to note here. Let's break them down.**

1. `mintTransaction` is a `Transaction` object, that needs to be transmitted to the MultiversX Blockchain. This is done on `line 22 - 31` via the `refreshAccount` and `sendTransactions` hooks. As we are using `sdk-dapp` we can configure it to show the default "Transaction Toast UI" in your app. This is beyond the scope of this guide but you can learn how to set it up by heading the [instructions here](https://github.com/multiversx/mx-sdk-dapp#transactions)
2. Any errors from the SDK's `datanftminter.mint(...)` method will be thrown in the `catch(e)` block on `line 33`. You can handle these errors yourself.
3. The `antiSpamTax` value is the live anti-spam tax requirement that's currently in place to prevent Data NFT spamming and is enforced by the Itheum Protocol as a means to regulate spam content. The `antiSpamTax` is in `ITHEUM tokens` and you will need to have this in your wallet (that you are connected with) to pay the `antiSpamTax` during the mint step.
4. Let's breakdown the `datanftminter.mint(...)`parameters that need a bit of extra explanation, but note that the SDK is fully documented so if you are using an IDE like Visual Studio Code, you can hover over each method to get detailed explanations of parameters and types.
   1. `https://data_marshal_URL.com` : A available Data Marshal Node endpoint that is effectively the "decentralized data broker". The Data Marshal Node Network is being developed by Itheum and will evolve into a complex, distributed system that cannot be censored. Anyone will be able to run their own Data Marshal or stake against existing Data Marshals in a system similar to validator staking. For now, you can use Itheum's flagship Data Marshal for your own Data NFT Collection.&#x20;
      1. Data Marshal on Devnet : https://api.itheumcloud-stg.com/datamarshalapi/achilles/v1
      2. Data Marshal on Mainnet : Reach out to us on Discord to find out more
   2. `https://data_stream_URL.com/protected_data_stream` : The is your "Origin Data Stream" location. It can be a dynamic file on [AWS S3](../../data-streams-guides/amazon-web-services-aws/), a static file on IPFS or [Arweave](https://www.arweave.org/) or even a backend server that you control.&#x20;
      1. This file or backend server MUST be publicly available, which means that it needs to return a 200 OK HTTP Status Code. This Data Stream URL is not exposed by the Itheum Protocol and fully abstracted from a end user. The Data Marshal encrypts it and only "streams" data out direct to the user via a "pipe" once ownership of the Data NFT is verified in real-time. So you can consider the Data Stream URL to be not really public. You can think of it as being similar to YouTube's "Unlisted Video URLs", which are "public" but not discoverable.
         1. But, you can take further actions to make them harder to access by making sure that search engines cannot index them, contruct this as random characters (so they are not-easily "guessable") and by also enforcing "authentication" headers (more on this later in this guide)
   3. `Royalty in % & Collection Size` : Collection size indicates the maximum number that will be pre-minted (in this use case it's 5,000). Note that this number cannot be increased but you will be able to `burn` supply to reduce the total collection size. Royalty in % (with 2 trailing zeros as shown in above example code comments) is basically the "Creator Royalty" that will be distributed to your as the Minter, if the tokens are re-traded in secondary trade situations.&#x20;
   4. `Short token Name` : A short, simple name for the token. Between 3 and 20 alphanumeric characters and no spaces. e.g. MY\_GM\_DATA
   5. `Title` : A title for the Data NFT. Between 10 and 60 alphanumeric characters. e.g. My Gaming Data
   6. `Description` : Describe your Data NFT. Between 10 and 400 alphanumeric characters. e.g. My Gaming Data. e.g. My PlayStation gaming data in JSON format
   7. `nftStorageToken: "XXX"` : In the Regular Data NFT format, your generated image and trait file will be uploaded to IPFS before being attached to the Data NFT on the blockchain. We currently support [NFT.Storage](https://nft.storage/) which is a free IPFS gateway you can use. You will need to sign up to this service and register for a API Key/Token and replace the XXX value with your obtained value.



### C) Mint a "Custom" Data NFT Collection&#x20;

If you prefer to use your own image and trait file (as opposed to Itheum's Image Generative Service and Traits Engine), this is also possible via the SDK minting toolkit. With this option, you can mint your own unique Data NFT that might have it own Image and Trait Meta Data file that is located on IPFS or even in a centrazlied server.&#x20;

Having a centralized image and Trait location will allow you to build "Dynamic Data NFT", where you can change the image layers and traits dynamically over time.&#x20;

<figure><img src="../../../.gitbook/assets/image (13).png" alt="" width="473"><figcaption><p>E.g. Custom Image of a gift card Data NFT - Can be from a centralized Server so it can "dynamically evolve"</p></figcaption></figure>



You can then have a "dynamic" Traits file that can "evolve" with your image.

{% code fullWidth="true" %}
```json
{
  "description": "Itheum GiftX Card. Super Rare 1st Edition.", // mandatory
  "attributes": [
    {
      "trait_type": "Creator", // mandatory
      "value": "erd1v...zzzz"
    },
    {
      "trait_type": "Data Preview URL", // mandatory
      "value": "https://data_preview_URL"
    },
    {
      "trait_type": "icon",
      "value": "medusa"
    },
    {
      "trait_type": "bg",
      "value": "red"
    },
    {
      "trait_type": "rarity",
      "value": "super rare"
    },
    {
      "trait_type": "original_value_usd",
      "value": "100"
    },
    {
      "trait_type": "remaining_value_usd",
      "value": "90"
    }
  ]
}
```
{% endcode %}



This "Custom" type of Data NFT can be minted with the following code:

{% code lineNumbers="true" fullWidth="true" %}
```javascript
try {
    // we need to 1st get the live anti-spam minting tax requirement from the smart contract
    const requirements = await dataNftMinter.viewMinterRequirements(new Address(address));
    const antiSpamTax = requirements?.antiSpamTaxValue;

    const mintTransaction: Transaction = await dataNftMinter.mint(
        new Address(address),
        "GIFTX_ED_1", // Short token Name (between 3 and 20 alphanumeric characters - no spaces)
        "https://data_marshal_URL.com", // The Data Marshal endpoint
        "https://data_stream_URL.com/protected_data_stream", // The Data Stream URL
        "https://data_preview_URL.com", // The Public Preview URL
        1500, // Royalty in % with 2 trailing zeros (e.g. 1500 is 15% or 500 would be 5% or 0 would be 0%. Max is 5000 of 50%)
        5000, // Collection size (max supply)
        "GiftX Edition 1", // Title (between 10 and 60 alphanumeric characters with spaces allowed)
        "Itheum GiftX Card. Super Rare 1st Edition", // Description (between 10 and 400 alphanumeric characters with spaces allowed)
        antiSpamTax, // Live Anti Spam Tax value
        {
          imageUrl: "https://my_website.com/giftx_card_demo/image-service?id=giftx-card&return=png",
          traitsUrl: "https://my_website.com/giftx_card_demo/metadata.json"
        }
    );

    await refreshAccount();

    const { sessionId, error } = await sendTransactions({
        transactions: mintTransaction,
        transactionsDisplayInfo: {
          processingMessage: "Minting Standard Data NFT",
          errorMessage: "Data NFT minting error",
          successMessage: "Data NFT minted successfully",
        },
        redirectAfterSign: false,
    });
} catch(e) {
    console.log("Minting Standard Data NFT FAILED");
    console.error(e);
}

```
{% endcode %}



As you will see, most code is exactly the same as the "Regular" Data NFT collection minting example provided before this section.  **But there are a few changes to note here.**&#x20;

1. `imageUrl (line 18)` : This can be a static image served from either IPFS or via a centralized location. In this example, we point to a hosted "image service", that can generate dynamic images that "evolve". E.g. the Gift Card Value and Balance change based on real-world activity
2. `traitsUrl (line 19)`: Like the image, this can be a static image served from either IPFS or via a centralized location and is used to describe the image. You can add any traits that you want, but description, attributes > trait\_type > Creator and attributes > trait\_type > Data Preview URL are mandatory to ensure they comply with the Itheum Protocol's compatibility of Data NFTs

If you followed this guide up until this step, you would have successfully minted your 5,000 Data NFT Collection and you will find this collection in your MultiversX Wallet. You can view and interact act with them by visiting the Data DEX ([https://stg.datadex.itheum.io](https://stg.datadex.itheum.io/) on Devnet and [https://datadex.itheum.io/](https://datadex.itheum.io/) on Mainnet). Using the Data DEX, you can also list them on the public Data NFT Marketplace, where they can be traded in this open and decentralized data market.\
\
Let's now explore how you can build a "client side" app that enables you to securely open and view Data NFTs.





## 3) Unlocking a Data NFT to securely "View Data"

In the above minting code example, we used a sample URL `https://data_stream_URL.com/protected_data_stream` as the Data Stream URL. Let's assume this is your "Origin Data Stream" where a dynamic and secure Data Stream is located off your origin web server.

In most cases, this Data Stream may contain non-sensitive data and you won't have a need to authenticate it before access is grant to the holder of the Data NFT. But maybe in this scenario, you do want to enable authentication to protect the data. So for example, if the Data NFT is opened via the SDK's methods to "viewData" without an authenticated session, your Data Stream will throw such an error.&#x20;

<figure><img src="../../../.gitbook/assets/image (9).png" alt="" width="563"><figcaption></figcaption></figure>

Here we had the Data Stream web app using the MultiversX Blockchains Native Auth service and the web app using the [https://github.com/multiversx/mx-sdk-js-native-auth-server](https://github.com/multiversx/mx-sdk-js-native-auth-server) library to validate incoming Authorization Bearer tokens.

The Itheum SDK now also supports the MultiversX Blockchain's NativeAuth standard for secure authentication and authorization, allowing you to "forward" Authorization headers via the Itheum Protocol over to your origin server. Lets explore how we can set this up.



### A) Obtain a Native Auth Access Token

In your client-side application, where your user logs in with their wallet, you can use `SDK Core` or [https://github.com/multiversx/mx-sdk-js-native-auth-client](https://github.com/multiversx/mx-sdk-js-native-auth-client) to obtain a `Native Auth accessToken.`\
\
And on your Data Stream Origin server, you can validate this accessToken via a library like [https://github.com/multiversx/mx-sdk-js-native-auth-server](https://github.com/multiversx/mx-sdk-js-native-auth-server)

Effectively, your client-side application is going to send an Authorization header that will get forwarded to your origin Data Stream web server. The Native Auth accessToken will need to have the appropriate TTL (time to live) and origins as explained in the native-auth-client and native-auth-server library links above. So, if you have an expired accessToken for example you server may return such as error.

<figure><img src="../../../.gitbook/assets/image (10).png" alt="" width="563"><figcaption></figcaption></figure>

Once your have setup the Native Auth accessToken code on both your client-side app and the origin Data Stream server, we can now use the Itheum SDK to coordinate the access control.



### B) Use the Itheum SDK to "View Data" on Data NFTs with Data Steams that need Native Auth accessToken

{% hint style="info" %}
Please note that the below code example uses a method called `viewData` to unlock and open a Data NFT, this method works as intended but it requires an additional `signMessage` step. In newer version of the SDK, there is a method called `viewDataViaMVXNativeAuth` which significantly improves the user experience by not request any additional steps from the user to sign messages. You can follow [this guide on how you can use the viewDataViaMVXNativeAuth method](guide-2-unlocking-data-nfts-via-multiversx-native-auth.md)
{% endhint %}

On your client side app, include these imports:

```javascript
import { DataNft, ViewDataReturnType } from "@itheum/sdk-mx-data-nft";
```

Grab a collection of Data NFTs found in the user's wallet like so:

```javascript
const _dataNfts = await DataNft.ownedByAddress(address);
```

Grab a selected Data NFT and trigger its `viewData` method by passing in the Native Auth's `accessToken` as an `authorization` header. In your IDE like Visual Studio Code, just hover over the viewData method to get detailed tooltips on the parameter types.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
const dataNft = dataNfts[0]; // just get the 1st Data NFTone here

// Next, we need to get a messageToBeSigned from the Data Marshal
const messageToBeSigned = await dataNft.getMessageToSign();

// Next, we need to get the user to sign this message with their wallet's private key
const signedMessage = await signMessage({
    message: messageToBeSigned,
    callbackRoute: undefined // if it's web wallet, you will need to have callback route
});

// For a more detailed code sample on the above messageToBeSigned and signedMessage:
// See a live implementation here : https://github.com/Itheum/explorer-dapp/blob/main/src/pages/AppMarketplace/MultiversxInfographics/index.tsx#L155

const nativeAuthAccessToken = 'ZXJkMX...c7f900e'; // the accessToken

// Next, we call viewData with the accessToken header
// Note that authorization HAS to be all lower case as the service is case sensitive.
const res : ViewDataReturnType = await dataNft.viewData({
    signedMessage: messageToBeSigned, 
    signableMessage: signedMessage, 
    stream: true, 
    fwdHeaderKeys: "authorization", 
    fwdHeaderMapLookup: {
        "authorization": `Bearer ${nativeAuthAccessToken}`,
    }
});

/* res will be of type ViewDataReturnType so you can obtain any of the following:

ViewDataReturnType {
    data: any;
    contentType: string;
    error?: string;
}

and handle your display logic. 'data' contains the Data Stream
*/


```
{% endcode %}

If the `viewData` method return the following error message via the Data Marshal:

<figure><img src="../../../.gitbook/assets/image (11).png" alt="" width="375"><figcaption></figcaption></figure>

Note that this is most likely caused by the following reasons:

* Both the `authorization` keywords on line 23 and 25 HAVE to be lowercase
* The `authorization` token was empty or didn't have the `Bearer` prefix or was malformed



### C) The role of the Data Marshal and Designing your Protected Origin Data Stream

* Here, the client-side interacts with the backend (Origin Data Stream) via the Itheum Protocol's `Data Marshal`. The Marshal is effectively forwarding the `accessToken` to your backend and it's doing this in a fully un-opinionated way, so this way you can choose to implement ANY form of authentication and authorization system for your Data NFTs + Private Data Stream.
* At this stage, the Data Marshal can ONLY forward the `authorization` header, as we saw in the example above. No other headers are supported and should you need any other headers, please reach out to us to discuss possibility. This limitation is due to significant architecture work happening to convert the Data Marshal to a distributed node based system and scope for new features are only considered if it benefits a large number of integrators.
* The Data Marshal is also being upgraded to use the Native Auth accessTokens as well to authenticate a Data NFT holder (i.e. if it sees it being passed in by the client). Once this feature has been added, the step to generate and sign a custom message before `viewData` can be called will no longer be needed and should provide a better UX.
* The Data Marshal also injects some custom headers to help your origin data stream server to identify more context from the incoming request.  These headers will evolve, but are currently:
  * `itm-marshal-fwd-chainid` : to indicate of it's mainnet or devnet
  * `itm-marshal-fwd-tokenid` : the full Data NFT token ID being opened
* Along with these headers, you also get the Native Auth accessToken which has context of the authenticated `address` of the user opening the Data NFT. This combination of headers and session data can allow your to fully customize your Origin Data Stream and allow for truly unique and dynamic Data Stream.
* Below is a sample dynamic Data Stream we built to test this implementation of the SDK. This is just a basic example for your viewing curiosity,  you can follow any format that suits your needs. The demo Data Stream details how a Data NFT can be linked to a shopper's activity.

{% code fullWidth="true" %}
```json
{
  "data_stream": {
    "name": "private stream for erd1qm---fkcc6",
    "creator": "Itheum",
    "created_on": 1692571700,
    "last_modified_on": 1692571710,
    "generated_on": 1692751836
  },
  "data": [
    {
      "txId": 1001,
      "category": "purchase",
      "date": 1692571701,
      "item": "Gold Watch",
      "store": "Nice jewellers",
      "meta": "https://some_session_to_full_meta_data_of_transaction?txId=1001&user=erd1qm---fkcc6&session=ZXJk---jYzc.YUh---6Vjk.b56---f04"
    },
    {
      "txId": 1000,
      "category": "purchase",
      "date": 1692571702,
      "item": "Small Cafe Latte",
      "store": "Corner Coffee Shop",
      "meta": "https://some_session_link_to_full_meta_data_of_transaction?txId=1000&user=erd1qm---fkcc6&session=ZXJk---jYzc.YUh---6Vjk.b56---f04"
    }
  ],
  "metaData": {
    "data_marshal_injected": {
      "itm-marshal-fwd-chainid": "devnet",
      "itm-marshal-fwd-tokenid": "xxx-11-1"
    },
    "mvx_native_auth": {
      "decodedSession": {
        "ttl": 3600,
        "origin": "http://localhost:3000",
        "address": "erd1qm---fkcc6",
        "signature": "b56---f04",
        "blockHash": "ed717fea562875d9edd70eae35f1d2ce3cb70c7c89e3d2cb99d90eb65f3edc5c",
        "body": "aHR---MDAw.ed717---dc5c.3600.eyJ0---zV9",
        "extraInfo": { "timestamp": 1692751835 }
      },
      "validateSession": {
        "issued": 1692751836,
        "expires": 1692755436,
        "address": "erd1qm---fkcc6",
        "origin": "http://localhost:3000",
        "extraInfo": { "timestamp": 1692751835 }
      }
    }
  }
}

```
{% endcode %}



## The End Result

If you have implemented the solution per the above steps, the final result will look like this. We built this real-world sample implementation using our SDK to ensure the integration works end-to-end.

{% embed url="https://youtu.be/7Jtk8JNMKfk" %}

