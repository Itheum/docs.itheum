# Guide 1 : Make your Regular NFT Collection to be Data NFT-PH Compatible

Are you planning on minting a regular NFT collection for your project? If so, then consider making your NFT Collection Data NFT Compatible. This is possible thanks to a Data NFT type called [data-nft-ph-plug-in-hybrid.md](../../../data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md "mention").&#x20;

Data NFT-PH is for projects that want to launch their own fully controlled NFT collections independently via an NFT Launchpad, CandyMachine or via a regular mint, but would like to provide a "plug-in" interface for their regular NFTs also to be used as "hybrid Data NFTs", immediately making your NFT collection compatible with Itheum's vision for data ownership and also the Itheum's entire ecosystem of tools and community - and bringing a new dimension of utility for your original NFT and boosting community activation/engagement/loyalty that's built on the principals of "data ownership."\
\
Firstly, you should learn about all the benefits of Data NFT-PH collection in the[data-nft-ph-plug-in-hybrid.md](../../../data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md "mention") product section docs. Next, in this guide, we will walk you through the 3 step process of making your NFT collection Data NFT-PH compatible!

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-data-marshal-network v1.0.0** or above to follow this guide.
* This guide assumes that you can add a few "custom metadata attribute fields" on your NFT's JSON metadata files stored in IPFS, Arweave or any NFT metadata storage you use.
* This guide also assumes that your Data Stream (the data the Data NFT-PH will unlock) can provide some simple "access control" or "authentication" by using a [multiversx-native-auth-protected-api.md](../../../pre-aithra-integrators/data-streams-guides/multiversx-native-auth-protected-api.md "mention") as your Data Stream origin.
* The Data NFT-PH standard is available in **Mainnet Beta** mode, where it provides all the below-described functionality, but it currently does NOT support static Data Streams (i.e. static files that never change) and will require your Data Stream to be dynamic and served via a "server" or "service" where you can handle some simple "access control" or "authentication". The goal is to have future versions of Data NFT-PHs to support BOTH static and dynamic Data Streams.

***

To make the guide more practical, let's first detail the real-world user story that we will aim to achieve by following this guide.

## Target User Story:

{% hint style="info" %}
As a developer of a regular 10k collection NFT collection for a DeFi Platform, the collection is called DEFICHAMPS:

* I'd like each NFT holder also to get access to a "Data Stream" of their DeFi trade volumes/insights that are saved in my backend server and made available via an "authenticated" API only to verified NFT holders.
* I'd like the DeFi trade volumes/insights to be in near-real time and can use the NFT Token ID and Holder Address to customize the data.
* I'd like to allow my NFT holders to feel that they are "owners" of this data that's linked to their NFT. Each NFT holder will be able to "unlock" and view this data linked to the NFT and be able to have this data be "portable", allowing the NFT holder to take their data to all DApps and apps compatible with the Itheum data brokerage protocol and unlock new personalized experiences unlocked by the original NFT.&#x20;
* I'd like my NFT to be exactly like any regular NFT but "plug into" the Itheum ecosystem of apps, infrastructure, and developers only when needed.
{% endhint %}

***

## Step 1: Prepare and Launch your Public Data Stream

Data NFTs, in essence, are regular NFTs that are "connected" to a "Data Stream."

<figure><img src="../../../../.gitbook/assets/image (121).png" alt="" width="563"><figcaption></figcaption></figure>

In the current version of Data NFT-PH, the Data Stream should be dynamic, showing data that is updating in real-time or during some schedule that triggers the data update (every hour, every day, every week, etc). The Data Stream can be fully open and public or have "MultiversX Native Auth authenticated" and should be served as an HTTPS URL. The complete requirements for a Data Stream URLs are detailed here:  [data-stream-url-rules.md](../../../pre-aithra-integrators/data-streams-guides/data-stream-url-rules.md "mention")\
\
Let's assume the Data Stream URL is just a backend authenticated API, similar to this sample API: [https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo)\
(It's important to note that this sample API gives you a `"Access Forbidden as this is a protected Data Stream. No credentials sent!"` message. This is expected as the API is protected by MultiversX Native Auth and is missing an access token, more on this later)\
\
As in the user story above, we are minting a 10k NFT collection. So we can have 10k variations of the same Data Stream URL. e.g.

<table><thead><tr><th width="208">Token ID</th><th>Data Stream URL</th></tr></thead><tbody><tr><td>DEFICHAMPS-3d6635-01</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-01</mark></td></tr><tr><td>DEFICHAMPS-3d6635-02</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-02</mark></td></tr><tr><td>...</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-...</mark></td></tr><tr><td>DEFICHAMPS-3d6635-10000</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-10000</mark></td></tr></tbody></table>

But as the Data Stream URL (once encrypted) will need to be inserted as an NFT Attribute on each token, as you can see, it's probably not the most optimized to have a Data Stream URL for each NFT as this will require a lot more processing to encrypt and store during the mint process but also as it's not easy to know information like final NFT IDs during a mint.&#x20;

So, it's recommended that you have a _single, smart_ Data Stream URL that is the same for all NFT tokens but implements a "MultiversX Native Auth wrapper." Native Auth is simply a "signature" based authentication system where you can validate the "caller" wallet address. By doing this, the Data Stream can unpack the Native Auth token, get the caller address "identity," and use it to personalize the Data Stream response.&#x20;

The Data Stream also passes through the Data Marshal network, injecting additional metadata like NFT Token ID into your Data Stream URL. With both the metadata from the validated Native Auth token and the additional metadata from the Data Marshal, you will be able to have access to validated information like authenticated caller address, ownership validated Data NFT ID, chain ID, etc., and use this to "real-time" personalize each Data Stream URL for each NFT.&#x20;

So, with this approach, you can have the same Data Stream URL for all your tokens :

<table><thead><tr><th width="208">Token ID</th><th>Data Stream URL</th></tr></thead><tbody><tr><td>DEFICHAMPS-3d6635-01</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo</td></tr><tr><td>DEFICHAMPS-3d6635-02</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo</td></tr><tr><td>...</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo</td></tr><tr><td>DEFICHAMPS-3d6635-10000</td><td>https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo</td></tr></tbody></table>

{% hint style="success" %}
How can you make your Public API MultiversX Native Auth Protected and be a compatible Data Stream URL? The good news is that it's not hard, and we have a detailed guide and code templates you can use to get this down. Head over here : [multiversx-native-auth-protected-api.md](../../../pre-aithra-integrators/data-streams-guides/multiversx-native-auth-protected-api.md "mention")
{% endhint %}

At the end of this step, you should have a public, Native Auth-protected API that you can use as the Data Stream URL for all the NFT tokens in your collection. Your new API should be similar to `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo` \


Once you have this Data Stream URL, just one more step is required to make your new NFT collection, Data NFT-PH compatible.

## Step 2: Include Custom Attributes in your NFT's Metadata File

Adding Data NFT compatibility to a regular NFT token is achieved by including some "custom metadata attribute fields" in your NFT's JSON Metadata file. It should be noted that these Attributes are "non-sensitive" (i.e. not sensitive data like keys or identity etc).\


<table><thead><tr><th width="259">Custom NFT Attribute</th><th>Notes</th></tr></thead><tbody><tr><td>itheum_data_stream_url</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>The origin where your data will be served from. You must obtain a Data Marshal encrypted version of the Data Stream URL you setup in Step 1 of this guide.<br><br><strong>Learn how to get the encrypted version of your  data_stream_url in the next step</strong> </td></tr><tr><td>itheum_creator</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>The wallet that is considered to be the "creator" and "owner" of the <strong>data_stream_url</strong>. This should be a wallet that you as the NFT collection creator actually owns and operates and something that you can use (if requested at anytime) to generate "signatures". It can also be the NFT creator wallet as well, but that's not mandatory (as most NFT launchpad / CandyMachine based NFT collections have a Smart Contract as the creator). Ideally, it's a "end user wallet" that can generate signatures when needed.</td></tr><tr><td>itheum_data_marshal_url</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>A "default" data marshal url for your Data NFT, see <a data-mention href="../../data-marshal-network/data-marshal-node-gateway-endpoints.md">data-marshal-node-gateway-endpoints.md</a> for more information.</td></tr><tr><td>itheum_data_preview_url</td><td>A "default" preview url for your data, on Itheum's platform tools like the <a data-mention href="../../../pre-aithra-apps/data-nft-marketplace/">data-nft-marketplace</a> or <a data-mention href="../../../pre-aithra-apps/data-dex/">data-dex</a>or even the <a data-mention href="../data-nft-sdk/">data-nft-sdk</a> - we use this to request and show a "Data Preview" for new users. Ideally, this is a fully public URL with a "sample" of the real data and is used to provide new Data NFT users and consumers an idea of the type of data they can unlock by purchasing a Data NFT.</td></tr><tr><td>itheum_creation_time</td><td>Used in the same above Itheum's platform tools to improve user experience and transparency. </td></tr><tr><td>itheum_title</td><td>A "default" title for your Data NFT, used in the same above Itheum's platform tools to improve user experience.<br><br>A 10-60 alphanumeric-only title that describes your collection. e.g.<br><code>NFT boosts APR in ChampDEX; share trade insights via Data NFT stream.</code></td></tr><tr><td>itheum_description</td><td>A "description" title for your Data NFT,  Used in the same above Itheum's platform tools to improve user experience.<br><br>The description field can also be used to add any specific "terms of use" URL if needed.<br><br>A 10-400 alphanumeric-only title that describes your collection. e.g. <br><code>DefiChamps NFT holders unlock boosted APRs in the ChampDEX and can share ownership of their historic trade insights data via a Data NFT compatible portable data stream. For terms of use visit https://defichamps.nft/terms</code></td></tr></tbody></table>



### **2.1) Get a Data Marshal Network-compatible encrypted Data Stream URL for the data\_stream\_url token Attribute:**

You can do this via a simple node.js script and by using our Data Marshal Network SDK.

Install the SDK:

```javascript
npm install --save @itheum/sdk-data-marshal-network
```

then write a simple node.js script (e.g. job.js) which has the following code and run it locally via `node job.js`

{% code overflow="wrap" lineNumbers="true" fullWidth="true" %}
```javascript
const { DataMarshal } = require("@itheum/sdk-data-marshal-network");

async function runJob() {
  // Initialization
  const dataMarshal = new DataMarshal("devnet"); // or "mainnet" based on where you are minting

  /* Get your encrypted Data Stream URL:
  Param 1: is your clear text, Data Stream URL that will be encrypted by the Data Marshal network
  
  Param 2: This can be thought of as the "creator" or "owner" of the  Data Stream URL. In this case, it is "erd1qmsq6ej344kpn8mc9xfngjhyla3zd6lqdm4zxx6653jee6rfq3ns3fkcc7". Note that this needs to be a valid MultiversX Wallet or the method will fail with an error similar to 'Error: Issue with data marshal generating payload'. 
  
  IMPORTANT!!! you need to make sure that you use this EXACT SAME Param 2 value, (i.e. "creator" or "owner" of the Data Stream URL) as the "itheum_creator" NFT attribute in the NFT metadata file, or else the Data Marshal network will not allow for the Data Stream to be viewed.
  */
  const encryptPayload = await dataMarshal.encryptDataStream(
    "https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo",
      "erd1qmsq6ej344kpn8mc9xfngjhyla3zd6lqdm4zxx6653jee6rfq3ns3fkcc7"
    );

  console.log(encryptPayload);

  /*
  console logged value:
  {
    messageHash: '9ae257fd4014bc84b35692832ac49a30d140712d2b0d4c53726d7847bf3d1378',
    dataStreamEncrypted: 'eyJBIjoiOWFlMjU3ZmQ0MDE0YmM4NGIzNTY5MjgzN2JiMmE3MjEzODhkZTkxMGEzMGYyZTcwIiwiQiI6IjllZDM1NTFjMmRkZmYwOTFhNWRlOWI4YTUyMTIyNTkzYTQ3NzViZDkwZTg3ZDNiMjE0NDU0N2VhNzMxOGRiOGMiLCJDIjoiMDZiNWRkYjlhNjA1NzcyNWQ5NzdkMDdhOGUwZTFmZmJmMTUwYjdmNTY3ZGNiOWZiMmE0OThlZDc5OTQzNGMwZCIsIkQiOiJkMWY2NTJhMWZkZGRkOTY4MzdmODEzNjU5YzlmM2EwNGRiMDE3Nzc3ZDkxMDA1YWU2ODI2ZjdkMzZhNGE0YmRmYjM3NzA1MTZiZTg2YzQ3YjkxOWUwODFlNjU2YjY2MGQ0MWViZDJjOGRhOGZlZTcwN2QyZDkyMzY2NTkzMzUyYTM0ODhmMmU3NTRjYjk5NzYwMDgxMmNkZjI5NTZhMjRlZmU1NzdiOWUxODkxMzY3MmNhZGE4Mjc3N2M3NWMwZTg4YmIyMjA4NjQwNDcwNjczYTRmNjA4YzNhMGFmYzExNGUxNDA5YzQ0N2FjZDUxYTkyZjcxZjgxZDFlNDY3Zjc1MmEzNGZkM2U4ZTdkNzQ2NDFjZTQzY2YwMTg3OTA4YzY5YzU1NmZjODA4YjUxNzkwMzU0MDc4YWMyZDZjZTcxMjdjZGUxNDY0YjljM2Q1NDgxNjA3YjI1MjVlYzhjOThiZWY2ZmMwNTUxNjVmMzExYmU3MGVjNGI1NThhOTA4MDQ2MDU5ZGU1M2FhOTEzZGIwZDgwMzFlYTBhMTFlYWFiZjBjZmViOWJmYzgwMDhjNzc4YzIyNzY4ZGU1ZmFkYzBlIiwiRSI6Ijc1MWY4NjgzMjYxN2U0MGMwZmJlYTM3MDFmMzM3NGVlMDM5MmEzN2Y0MzA2ODU4NThiNjIzMDVlOTA1MWI5YTE1ODg0ZDFmNTRiMDNlYTk5MTM2NTc3YWRjYzgyYWQ3N2FiOTczZjZjNGFiMGRhMWZmNDNmNDI2NTE1NWRiZDBmIn0='
  }
  
  - messageHash is a unique hash you can use to identify your Data Stream URL (you can use this as a "provenance" ID of sorts if needed)
  - dataStreamEncrypted is the value you need to use for the "itheum_data_stream_url" NFT Attribute
  */
}

runJob();
```
{% endcode %}

... now that you have an encrypted "**itheum\_data\_stream\_url**" value, we can proceed with the next steps.\


### 2.2) Adding the Custom Attributes to your NFT's JSON Metadata File

As you will know, all NFT collections use a JSON Metadata file to store data about Traits, etc. On MultiversX you can view this JSON file by visiting any collection on Explorer  (as an example...)

<figure><img src="../../../../.gitbook/assets/image (136).png" alt=""><figcaption><p>These NFT JSON Metadata files are usually stored on IPFS and referenced on the NFT token on-chain</p></figcaption></figure>

You need to add the Custom NFT Attributes described in the table above to this file. You MUST add the Mandatory fields "**itheum\_data\_stream\_url**" (should be encrypted as described above), "**itheum\_creator**" (should be the same value used in the encryption process of itheum\_data\_stream\_url as described above), and "**itheum\_data\_marshal\_url**" (use latest devnet or mainnet values as per [data-marshal-node-gateway-endpoints.md](../../data-marshal-network/data-marshal-node-gateway-endpoints.md "mention")).&#x20;

The remaining "itheum\_\[\*]" fields are optional but recommended.&#x20;

Once you add the custom fields, your JSON Metadata file should look EXACTLY like this:

<figure><img src="../../../../.gitbook/assets/image (137).png" alt=""><figcaption></figcaption></figure>

Note that the custom fields MUST be on the "top-level" - e.g. on the same level as "name", "description", "attributes" etc. If they are NOT on the "top-level" it will NOT work.



## Step 3: Enable Basic "NFT Collection Token ID Verification" in your Origin Data Stream Service&#x20;

{% hint style="warning" %}
Note that this step is only required as Data NFT-PH is in Mainnet Beta mode. This won't be required once the Itheum protocol ships a feature called "Creator Bonding", which is due in very early Q2 2024.\
\
This step may also NOT be needed if you are doing Native Auth validation on the caller's address and signature.
{% endhint %}

The final step is to include some basic NFT Collection Token ID verification in your [multiversx-native-auth-protected-api.md](../../../pre-aithra-integrators/data-streams-guides/multiversx-native-auth-protected-api.md "mention") Data Stream origin, this is only needed as we are in a Mainnet Beta mode and aims to provide some extra authentication layer to ensure that only your Data NFT-PH collection holders can open and view your data stream.\
\
The logic is fairly simple, and is shown in this code example (in red box)

<figure><img src="../../../../.gitbook/assets/image (138).png" alt=""><figcaption></figcaption></figure>

This code is from the open-source [multiversx-native-auth-protected-api.md](../../../pre-aithra-integrators/data-streams-guides/multiversx-native-auth-protected-api.md "mention") template we provide, you [can check out the code here](https://github.com/Itheum/data-stream-expressjs-native-auth-wrapper-template/blob/main/app.js)



{% hint style="success" %}
Congratulations! Your NFT collection is now Data NFT-PH compatible. A full list of benefits is provided in the section[#benefits-of-using-the-data-nft-ph-standard](../../../data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md#benefits-of-using-the-data-nft-ph-standard "mention")

Your Data NFTs will now seamlessly work across all of Itheum's ecosystem tools and services and empower your NFT holders with Data Ownership!&#x20;
{% endhint %}
