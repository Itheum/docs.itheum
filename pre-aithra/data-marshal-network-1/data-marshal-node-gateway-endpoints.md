# Data Marshal Node Gateway Endpoints

The Data Marshal is the node that brokers the trade of data between a Data Creator and a Data Consumer. Learn more about the [Data Marshal here](../data-marshal-network.md)

When you mint a Data NFT via the [Data DEX DApp](https://stg.datadex.itheum.io/) (devnet) or via the [Data NFT SDK,](../software-development-kits-sdks/data-nft-sdk/) you will be asked for a Data Marshal gateway endpoint as one of the minting parameters. \
\
For example, as you follow this [detailed guide for Minting Data NFTs via the Data NFT SDK](../software-development-kits-sdks/data-nft-sdk/guide-1-minting-a-custom-data-nft-collection-with-authenticated-data-streams-via-sdk.md), you will see the following code snippet.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
const mintTransaction: Transaction = await dataNftMinter.mint(
    new Address(address),
    "MY_GM_DATA", // Short token Name (between 3 and 20 alphanumeric characters - no spaces)
    "https://data_marshal_URL.com", // The Data Marshal gateway endpoint (see below for options for devnet vs mainnet)
    "https://data_stream_URL.com/protected_data_stream", // The Data Stream URL
    "https://data_preview_URL.com", // the public Data Preview URL
    1500, // // Royalty in % with 2 trailing zeros (e.g. 1500 is 15% or 500 would be 5% or 0 would be 0%. Max is 5000 of 50%)
    5000, // Collection size (supply)
    "My Gaming Data", // Title (between 10 and 60 alphanumeric characters with spaces allowed)
    "My PlayStation gaming data in JSON format", // Description (between 10 and 400 alphanumeric characters with spaces allowed)
    antiSpamTax, // Live Anti Spam Tax value
    {
      nftStorageToken: "XXX" // nft.storage API token
    }
);
```
{% endcode %}

On line 4, you will see that you need to provide a Data Marshal gateway endpoint.\
\
You can use the following endpoints depending on your environments and use cases that you are building for.

<table><thead><tr><th width="156">Data Marshal Node Type</th><th>Mainnet Endpoint</th><th>Devnet Endpoint</th><th>Features</th><th>Limitations</th></tr></thead><tbody><tr><td>Achilles</td><td>https://api.itheumcloud.com/datamarshalapi/achilles/v1</td><td>https://api.itheumcloud-stg.com/datamarshalapi/achilles/v1</td><td>Data brokering, Native Auth, Nested Streams, High Scalability</td><td>Only supports Data Streams with maximum size of 4.5MB</td></tr><tr><td>Brontes</td><td>https://api.itheumcloud.com/datamarshalapi/brontes/v1</td><td>https://api.itheumcloud-stg.com/datamarshalapi/brontes/v1</td><td>Data brokering, Native Auth, Nested Streams, Support Data Streams over 4.5MB</td><td>Limited Scalability</td></tr><tr><td>Router<br><br><strong>[Recommended]</strong><br><br>The router is recommended as it will use the most up to data Data Marshal </td><td>https://api.itheumcloud.com/datamarshalapi/router/v1</td><td>https://api.itheumcloud-stg.com/datamarshalapi/router/v1</td><td>Same as Brontes</td><td>Same as Brontes</td></tr></tbody></table>

