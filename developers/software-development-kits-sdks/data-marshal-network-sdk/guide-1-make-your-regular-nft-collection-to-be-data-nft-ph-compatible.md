# Guide 1 : Make your Regular NFT Collection to be Data NFT-PH Compatible

Are you planning on minting a regular NFT collection for your project? If so, then consider making your NFT Collection Data NFT Compatible. This is possible thanks to a Data NFT type called [data-nft-ph-plug-in-hybrid.md](../../../product/data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md "mention").&#x20;

Data NFT-PH is for projects that want to launch their own fully controlled NFT collections independently but would like to provide a "plug-in" interface for their regular NFTs also to be used as hybrid Data NFTs, immediately making your NFTs compatible with Itheum's vision for data ownership and also the Itheum's entire ecosystem of tools and community - and bringing a new dimension of utility for your original NFT and boosting community activation/engagement/loyalty that's built on the principals of "data ownership."\
\
Firstly, you should learn about all the benefits of Data NFT-PH collection in the[data-nft-ph-plug-in-hybrid.md](../../../product/data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md "mention") product section docs. Next, in this guide, we will walk you through the 3 step process of making your NFT collection Data NFT-PH compatible.

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-data-marshal-network v1.0.0** or above to follow this guide.
* This guide assumes that you still need to mend your NFT collection and can include new on-chain NFT Attributes on your token collection during the mint phase. If you have already minted your NFT collection, you can still make it Data NFT-PH compatible, but it will require an NFT token upgrade to include new on-chain NFT Attributes (read on for some details on this).

***

To make the guide more practical, let's first detail the a real-world user story that we will aim to achieve by following this guide.

## Target User Story:

{% hint style="info" %}
As a developer of a regular 10k collection NFT collection for a DeFi Platform, the collection is called DEFICHAMPS:

* I'd like each NFT holder also to get access to a "Data Stream" of their DeFi trade volumes/insights that are saved in my backend server and made available via an "authenticated" API only to verified NFT holders.
* I'd like the DeFi trade volumes/insights to be in near-real time and can use the NFT Token ID and Holder Address to customize the data.
* I'd like allow my NFT holders to feel that they are partial "owners" of this data that's linked to their NFT. Each NFT holder will be able to "unlock" and view this data linked to the NFT and be able to have this data be "portable", allowing the NFT holder to take their data to all DApps and apps compatible with the Itheum data brokerage protocol and unlock new personalized experiences unlocked by the original NFT.&#x20;
* I'd like my NFT to be exactly like any regular NFT but "plug into" the Itheum ecosystem of apps, infrastructure, and developers only when needed.
{% endhint %}

***

## Step 1: Prepare and Launch your Public Data Stream

Data NFTs, in essence, are regular NFTs that are "connected" to a "Data Stream."

<figure><img src="../../../.gitbook/assets/image (121).png" alt="" width="563"><figcaption></figcaption></figure>

This Data Stream can be static (data never changes) or dynamic, showing data is updating in real-time or during some schedule that triggers the data update (every hour, every day, every week, etc). They can be fully open and public or have "MultiversX Native Auth authenticated" and should serve as an HTTPS URL. The complete requirements for a Data Stream URLs are detailed here:  [data-stream-url-rules.md](../../../integrators/data-streams-guides/data-stream-url-rules.md "mention")\
\
Let's assume the Data Stream URL is actually just a backend authenticated API, similar to this sample API: [https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo)\
(It's important to note that this sample API gives you a `"Access Forbidden as this is a protected Data Stream. No credentials sent!"` message. This is expected as the API is protected by MultiversX Native Auth and is missing a access token, more on this later)\
\
In the user storage above, we are minting a 10k NFT collection. So we can have 10k variations of the same Data Stream URL. e.g.

| Token ID                | Data Stream URL                                                                                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| DEFICHAMPS-3d6635-01    | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft\_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-01</mark>    |
| DEFICHAMPS-3d6635-02    | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft\_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-02</mark>    |
| ...                     | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft\_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-...</mark>   |
| DEFICHAMPS-3d6635-10000 | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo?nft\_id=<mark style="color:yellow;">DEFICHAMPS-3d6635-10000</mark> |

But as the Data Stream URL (once encrypted) will need to be inserted as an on-chain NFT Attribute on each token, as you can see, it's probably not the most optimized to have a Data Stream URL for each NFT as this will require a lot more processing to encrypt and store during the mint process but also as it's not easy to know information like final NFT IDs during a mint.&#x20;

So, it's recommended that you have a _single, smart_ Data Stream URL that is the same for all NFT tokens but implements a "MultiversX Native Auth wrapper." Native Auth is simply a "signature" based authentication system where you can validate the "caller" wallet address. By doing this, the Data Stream can unpack the Native Auth token, get the caller address "identity," and use it to personalize the Data Stream response.&#x20;

The Data Stream also passes through the Data Marshal network, injecting additional metadata like NFT Token ID into your Data Stream URL. With both the metadata from the validated Native Auth token and the additional metadata from the Data Marshal, you will be able to have access to validated information like authenticated caller address, ownership validated Data NFT ID, chain ID, etc., and use this to "real-time" personalize each Data Stream URL for each NFT.&#x20;

So, with this approach, you can have the same Data Stream URL for all your tokens :

| Token ID                | Data Stream URL                                                                |
| ----------------------- | ------------------------------------------------------------------------------ |
| DEFICHAMPS-3d6635-01    | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo |
| DEFICHAMPS-3d6635-02    | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo |
| ...                     | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo |
| DEFICHAMPS-3d6635-10000 | https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo |

{% hint style="success" %}
How can you make your Public API MultiversX Native Auth Protected and be a compatible Data Stream URL? The good news is that it's not hard, and we have a detailed guide and code templates you can use to get this down. Head over here : [multiversx-native-auth-protected-api.md](../../../integrators/data-streams-guides/multiversx-native-auth-protected-api.md "mention")
{% endhint %}

At the end of this step, you should have a public, Native Auth-protected API that you can use as the Data Stream URL for all the NFT tokens in your collection. Your new API should be similar to `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo` \


Once you have this Data Stream URL, just one more step is required to make your new NFT collection, Data NFT-PH compatible.

## Step 2: Include on-chain Attributes onto your NFTs

{% hint style="warning" %}
It should be noted that using [itheum-enterprise.md](../../../product/itheum-enterprise.md "mention") to mint your Data NFT collection is probably the best option if you want the entire mint process handled for you via a user interface that is super easy to use and yet, powerful and flexible.&#x20;

Itheum Enterprise mints complete regular NFT collections, making them Data NFT compatible "out of the box." But it also offers many more features like seamless NFT collection curation (pause, freeze, wipe), control transferability rights of the NFTs (i.e., make them soulbound or control where they can be used for traded), and a load of other features that make managing (Data) NFTs seamless. But there are some limitations with the current version of Itheum Enterprise, where the product only allows for minting and managing NFT tokens and does not provide a way to run NFT launches or distributions via a candy machine tool to mint and distribute.

If you prefer to use or try Itheum Enterprise instead of making your own NFT collections Data NFT-PH compatible, then follow this guide: [guide-3-get-started-with-itheum-enterprise.md](../../../integrators/data-dex-guides/multiversx-blockchain/guide-3-get-started-with-itheum-enterprise.md "mention")

But, if you prefer to use your own NFT minting scripts or tools and NOT use Itheum Enterprise, then you can continue with the next part of this guide.
{% endhint %}



Adding Data NFT compatible to a regular NFT token is achieved by including some on-chain [Attributes](https://docs.multiversx.com/tokens/nft-tokens/#nftsft-fields) on your NFT tokens. It should be noted that these Attributes are on-chain and are "non-sensitive" (i.e. not sensitive data like keys or identity etc). All these Attributes are "included on each NFT token" and not on the "whole collection itself", so you have the ability to customize these "per NFT" minted.\


<table><thead><tr><th width="259">on-chain NFT Attribute</th><th>Notes</th></tr></thead><tbody><tr><td>data_stream_url</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>You must obtain a Data Marshal encrypted version of the Data Stream URL you setup in Step 1 of this guide.<br><br> <strong>learn how to get the encrypted version of your  data_stream_url in the next step</strong> </td></tr><tr><td>data_preview_url</td><td>A "default" preview url for your data, on Itheum's platform tools like the <a data-mention href="../../../product/data-nft-marketplace/">data-nft-marketplace</a> or <a data-mention href="../../../product/data-dex/">data-dex</a>or even the <a data-mention href="../data-nft-sdk/">data-nft-sdk</a> - we use this to request and show a "Data Preview" for new users. Ideally, this is a fully public URL with a "sample" of the real data and is used to provide new Data NFT users and consumers an idea of the type of data they can unlock by purchasing a Data NFT.</td></tr><tr><td>data_marshal_url</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>A "default" data marshal url for your Data NFT, see <a data-mention href="../../data-marshal-node-endpoints.md">data-marshal-node-endpoints.md</a> for more information.</td></tr><tr><td>creator</td><td><mark style="color:yellow;"><strong>Mandatory: Needs a valid value</strong></mark><br><br>The address of the primary NFT collection "Creator". If NFTs that are Data NFT-PH compatible are traded on Itheum's <a data-mention href="../../../product/data-nft-marketplace/">data-nft-marketplace</a>, this creator address immediately gets royalties distributed to it.</td></tr><tr><td>creation_time</td><td>Used in the same above Itheum's platform tools to improve user experience and transparency. </td></tr><tr><td>title</td><td>A "default" title for your Data NFT, used in the same above Itheum's platform tools to improve user experience.<br><br>A 10-60 alphanumeric-only title that describes your collection. e.g.<br><code>NFT boosts APR in ChampDEX; share trade insights via Data NFT stream.</code></td></tr><tr><td>description</td><td>A "description" title for your Data NFT,  Used in the same above Itheum's platform tools to improve user experience.<br><br>The description field can also be used to add any specific "terms of use" URL if needed.<br><br>A 10-400 alphanumeric-only title that describes your collection. e.g. <br><code>DefiChamps NFT holders unlock boosted APRs in the ChampDEX and can share ownership of their historic trade insights data via a Data NFT compatible portable data stream. For terms of use visit https://defichamps.nft/terms</code></td></tr></tbody></table>

**Can I save gas costs by reducing extra storage for each NFT token?**\
\
Although this is not advisable, Note that if you want to save Gas by limiting extra storage costs, you are free to send empty default values for all the attributes above that does have the <mark style="color:yellow;">**Mandatory: Needs a valid value**</mark> detail.



### **2.1) Get a Data Marshal Network-compatible encrypted Data Stream URL for the data\_stream\_url token Attribute?**

You can do this via a simple node.js script and by using our Data Marshal Network SDK.

Install the SDK:

```javascript
npm install --save @itheum/sdk-data-marshal-network
```

then write a simple node.js script (e.g. job.js) which has the following code and run it locally via `node job.js`

{% code overflow="wrap" lineNumbers="true" fullWidth="true" %}
```javascript
import { DataMarshal } from "@itheum/sdk-data-marshal-network";

// Initialization
const dataMarshal = new DataMarshal("devnet"); // or "mainnet"

// Get your encrypted Data Stream URL
// ... erd1qmsq6ej344kpn8mc9xfngjhyla3zd6lqdm4zxx6653jee6rfq3ns3fkcc7 here is the Creator and needs to be a valid MultiversX Address or the call will fail with an error simialr to 'Error: Issue with data marshal generating payload'
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

- messageHash is a unique hash you can use to identify your Data Stream URL
- dataStreamEncrypted is the value you need to use for data_stream_url on-chain NFT Attribute
*/
```
{% endcode %}

... now that your have an encrypted data\_stream\_url value, we can proceed with the next steps.\


### 2.2) Adding the on-chain Attributes on your NFT Collection tokens

Let's explore a few options for adding the above-mentioned on-chain Attributes to your NFT Collections tokens.



### A) New Mint: via a Smart Contract that mints your collection (NFT Minter / Candy Machine etc)

The best-case scenario is that you have NOT YET minted your NFT collection and are an NFT Minter (similar to [this](https://github.com/multiversx/mx-nft-collection-minter-sc))  or Candy Machine smart contract to mint your tokens. In the scenario, you will need to upgrade your Smart Contract's primary mint method to include similar code as below, with the ultimate goal of adding the on-chain Attributes to your NFT Collection's tokens.\


{% hint style="warning" %}
**Do you have your own NFT Attributes?** \
As you may have your own custom on-chain NFT attributes as well, note that you can also add these custom to your NFT tokens as well BUT ONLY AFTER the default Data NFT-PH attributes. i.e. the 7 Data NFT-PH attributes need to come first and in order (as shown in below code sample)\
\
**What if I add my attributes BEFORE the Data NFT-PH attributes?**\
For your NFT to be Data NFT-PH compatible, it MUST have the 7 Data NFT-PH attributes come first and in order. You can have as many of your own custom attributes as you want but they should only come AFTER the 7 Data NFT-PH attributes (as shown in below code sample)
{% endhint %}

{% hint style="danger" %}
Disclaimer: Please note that the sample code below is an "unaudited" and should only be used as a reference.
{% endhint %}

{% code lineNumbers="true" fullWidth="true" %}
```rust
pub struct DataNftPhAndCustomAttributes<M: ManagedTypeApi> {
  pub data_stream_url: ManagedBuffer<M>,
  pub data_preview_url: ManagedBuffer<M>,
  pub data_marshal_url: ManagedBuffer<M>,
  pub creator: ManagedAddress<M>,
  pub creation_time: u64,
  pub title: ManagedBuffer<M>,
  pub description: ManagedBuffer<M>,
  pub tier: u64 // this is your own custom NFT attribute, that MUST come AFTER the above 7
  // someOtherCustomAttrA:
  // someOtherCustomAttrB: 
}

// Public endpoint used to mint NFT as part of a NFT mint
#[payable("*")]
#[endpoint(mint)]
fn mint_token(
    &self,
    name: ManagedBuffer,
    media: ManagedBuffer,
    metadata: ManagedBuffer,
    data_marshal: ManagedBuffer,
    data_stream: ManagedBuffer, // this needs to be the Data Marshal Network encrypted data_stream_url
    data_preview: ManagedBuffer,
    royalties: BigUint,
    supply: BigUint, // for SFT, it can bu multiple
    title: ManagedBuffer,
    description: ManagedBuffer,
) -> DataNftPhAndCustomAttributes<Self::Api> {

    // validate Data NFT attribute info
    self.require_url_is_valid(&data_marshal); // should start with https:// and look like a valid URL with no invalid characters
    self.require_title_description_are_valid(&title, &description); // should be . title = 10-60 alphanumeric chars. description = 10-400 chars,urls allowed

    let caller = self.blockchain().get_caller();
    let current_time = self.blockchain().get_block_timestamp();

    // Add all Data NFT attributes
    let attributes: DataNftPhAndCustomAttributes<Self::Api> = DataNftPhAndCustomAttributes {
        data_stream_url: data_stream.clone(),
        data_preview_url: data_preview,
        data_marshal_url: data_marshal.clone(),
        creator: caller.clone(),
        creation_time: current_time,
        title,
        description,
        tier: 15 // this is your own custom NFT attribute, that MUST come AFTER the above 7
        // someOtherCustomAttrA:
        // someOtherCustomAttrB: 
    };

    let token_identifier = self.token_id().get_token_id(); // nft collection id

    let nonce = self.send().esdt_nft_create(
        &token_identifier,
        &supply,
        &name,
        &royalties,
        &self.create_hash_buffer(&data_marshal, &data_stream),
        &attributes,
        &self.create_uris(media, metadata),
    );

    self.send()
        .direct_esdt(&caller, &token_identifier, nonce, &supply);

    attributes
}
```
{% endcode %}

* In the code example above, `tier, someOtherCustomAttrA and someOtherCustomAttrB` are your own custom NFT attributes that come AFTER the 7 Data NFT-PH attributes.



### B) New Mint: via direct mint call transaction to the core protocol (Meta Chain)

Suppose you are not using an NFT Minter / Candy Machine Smart contract to mint your tokens and are minting your collection tokens via direct transactions sent to the blockchain. In that case, you can add the new on-chain NFT Attributes as shown below.

The following code snippets are from the MultiversX documentation; getting the latest code directly from their docs is advisable.

* **Creation of an NFT :** [https://docs.multiversx.com/tokens/nft-tokens/#creation-of-an-nft](https://docs.multiversx.com/tokens/nft-tokens/#creation-of-an-nft)

{% code fullWidth="true" %}
```javascript
NFTCreationTransaction {
    Sender: <address with ESDTRoleNFTCreate role>
    Receiver: <same as sender>
    Value: 0
    GasLimit: 3000000 + Additional gas (see below)
    Data: "ESDTNFTCreate" +
          "@" + <token identifier in hexadecimal encoding> +
          "@" + <initial quantity in hexadecimal encoding> +
          "@" + <NFT name in hexadecimal encoding> +
          "@" + <Royalties in hexadecimal encoding> +
          "@" + <Hash in hexadecimal encoding> +
          "@" + <Attributes in hexadecimal encoding> +
          "@" + <URI in hexadecimal encoding> +
          "@" + <URI in hexadecimal encoding> +
          ...
}
```
{% endcode %}

* **Change NFT Attributes :** [https://docs.multiversx.com/tokens/nft-tokens/#change-nft-attributes](https://docs.multiversx.com/tokens/nft-tokens/#change-nft-attributes)

{% code fullWidth="true" %}
```javascript
ESDTNFTUpdateAttributesTransaction {
    Sender: <address of an address that has ESDTRoleNFTUpdateAttributes role>
    Receiver: <same as sender>
    Value: 0
    GasLimit: 10000000
    Data: "ESDTNFTUpdateAttributes" +
          "@" + <token identifier in hexadecimal encoding> +
          "@" + <NFT or SFT nonce in hexadecimal encoding> +
          "@" + <Attributes in hexadecimal encoding>
}
```
{% endcode %}

_For more details about how arguments have to be encoded, check_ [_here_](https://docs.multiversx.com/developers/sc-calls-format)_._



### C) NFT Upgrade: Upgrade an existing NFT collection tokens to include the new on-chain token Attributes

If you have already minted your NFT collection and possibly also distributed the collection, you can still have a process to "recall and upgrade" your NFTs. You will need to have an "upgrade" smart contract where the NFT holders can deposit their tokens into it and, after that, have an endpoint to upgrade the tokens and add the new Attributes to the NFTs. The upgrade smart contract will be the owner of the NFT collection and should have the `ESDTRoleNFTUpdateAttributes` role to upgrade the Attributes.

Read more about Attribute upgrade on the [MultiversX documentation here](https://docs.multiversx.com/tokens/nft-tokens/#change-nft-attributes). After the NFT tokens have been upgraded with the new on-chain token Attributes, the original depositors will be able to withdraw them back into their wallets. The smart contract code to upgrade the token's attributes will be similar to the code snippet from the [#a-new-mint-via-a-smart-contract-that-mints-your-collection-nft-minter-candy-machine-etc](guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible.md#a-new-mint-via-a-smart-contract-that-mints-your-collection-nft-minter-candy-machine-etc "mention") section above, but keep in mind that for Attribute upgrades,  if you want to keep the old attributes you will have to pass them along with the new ones or else you will lose your existing attributes.



{% hint style="success" %}
Congratulations! your NFT collection is now Data NFT-PH compatible. A full list of benefits are provided on the section[#benefits-of-using-the-data-nft-ph-standard](../../../product/data-nft/data-nft-types/data-nft-ph-plug-in-hybrid.md#benefits-of-using-the-data-nft-ph-standard "mention")

Your Data NFTs will now seamlessly work across all of Itheum's ecosystem tools and services and empowers your NFT holders with Data Ownership!&#x20;
{% endhint %}
