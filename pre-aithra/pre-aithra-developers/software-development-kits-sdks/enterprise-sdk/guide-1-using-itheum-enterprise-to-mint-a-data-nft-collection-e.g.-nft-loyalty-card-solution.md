# Guide 1 : Using Itheum Enterprise to Mint a Data NFT Collection (e.g. NFT Loyalty Card Solution)

{% hint style="danger" %}
Itheum Enterprise is in "devnet" mode so you can't use it on the MutiversX Mainnet. If you want lauch your own Data NFTs on MutiversX Mainnet, we recommend that you use the Data NFT-PH standard as described in this guide [guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible.md](../data-marshal-network-sdk/guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible.md "mention")
{% endhint %}

This guide walks you through the entire process of using Itheum Enterprise and the Data NFT-Lease technology to Mint a Data NFT Collection that is used to power a complete enterprise-ready NFT Loyalty Card platform.

#### What is Data NFT-Lease?&#x20;

Itheum has 2 types of Data NFTs, the first is available on mainnet and called Data NFT-FT. These are fully transferable tokens that follow the SFT token design. They are intended to be a licensing mechanism for non-sensitive data assets like files and documents. It’s very easy to get started to mint and trade your data assets as Data NFT-FTs. But as the name indicates, they are “fully transferable” and are a licence type similar to perpetual licensing for data usage. But for more complex use-cases where you want to limit some transferability and oversee more control of the Data NFTs, you would use Data NFT-Lease. This standard follows the pure NFT pattern of tokenization of data licensing. It allows creators more flexibility on the use-cases that can be enabled by Data NFT technology. You will be able to create use-cases like loyalty cards, data vaults, identity platforms etc. Data NFTs part of the Data NFT-Lease design have the term “Lease” because of their ability to have their transferability controlled by the issuer as part of Itheum Enterprise, this means the tokens can be made “soulbound” based on various strategic requirements. This makes them “regulation friendly” if needed as well as being useful for sensitive use-cases (as you can prevent tradeability) or allow them to only be “leased” via some lending mechanism. This falls into alignment with more enterprise use-cases. Learn more here: [data-nft-lease.md](../../../data-nft/data-nft-types/data-nft-lease.md "mention")

#### What is Itheum Enterprise?

Itheum enterprise wraps the Data NFT-Lease technology to provide more governance and control over the NFT collections and also provide a mechanism for having protocol upgrades in the form of smart contract upgrades broadcast to all itheum enterprise users, who can then choose to opt-into specific upgrades.

Learn more here what itheum enterprise is aiming to solve here: [itheum-enterprise.md](../../../pre-aithra-r-and-d/itheum-enterprise.md "mention")

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* You need **@itheum/sdk-mx-data-nft v2.1.0** or above to follow this guide.
* This guide also is specific to the **MuiltiversX Blockchain** and provides code samples that use the **@multiversx/sdk-core** and **@multiversx/sdk-dapp** libraries to authenticate and sign and track on-chain transactions. Although, these libraries are optional and you can use any MultiversX tooling to interact with the blockchain.
* To open a Data NFT and view it's data using using the `Data NFT SDK`, you have implemented MultiversX Native Auth integration with Itheum as per this the guide [guide-2-unlocking-data-nfts-via-multiversx-native-auth.md](../data-nft-sdk/guide-2-unlocking-data-nfts-via-multiversx-native-auth.md "mention")
* You have control of the origin Data Stream publishing system (see Step 1 setup section below), as you will need to set HTTP Response Headers on the Data Stream.

***

In this guide, we will use Data NFT-Lease and Itheum Enterprise to deploy a loyalty card program.

The examples below assumes:

* You use the front-end focused SDK Core and SDK Dapp from MultiversX. But ideally you will use TypeScript and backend libraries that allow you to better do “bulk” transactions like “mint in bulk” etc.
* You have a backend in s place that will allow for Native Auth based access to Dynamic Data Streams
* The Data Stream URLs need to be publicly available and follow these rules - [https://docs.itheum.io/product-docs/integrators/data-streams-guides/data-stream-url-rules](https://docs.itheum.io/product-docs/integrators/data-streams-guides/data-stream-url-rules)
* You have your own NFT Images and Metadata files loaded into IPFS. e.g if you are minting 10k Data NFTs, you will need a combination of 10k Images and Metadata file hosted on IPFS (or a centralised location too if you are fine with it)
* You will be “pre-minting” Data NFTs. After this you can send them to a distributor smart contract to launch the collection as per your own rules for the launch

## Target User Story:

{% hint style="info" %}
As an integrator of Itheum web3 Data Brokerage infrastructure:

* I'd like to use the SDK to mint a collection of 5,000 unique Data NFTs.&#x20;
* Each item in the collection should have its own image (not the Itheum generative image service).&#x20;
* The Data Streams on each Data NFT is unique and should also be fully non-public and implement authentication via a `Bearer` token header (based on our backend authentication requirements).&#x20;
* The Data Stream should also be customizable, where they can read a session of a user (address, tokenID) and provide some level of runtime customization before streaming out.
{% endhint %}

Let’s get started.

## Step 1: Itheum SDK Installation

You need both the Itheum SDKs installed in your app.

{% code fullWidth="false" %}
```javascript
"@itheum/sdk-mx-data-nft": "^2.0.0-alpha.1",
"@itheum/sdk-mx-enterprise": "^0.0.1",
```
{% endcode %}

You also need these version (we’ve tested with these specific versions) and above

{% code fullWidth="false" %}
```javascript
"@multiversx/sdk-core": "^12.8.0",
"@multiversx/sdk-dapp": "2.19.2",
"@multiversx/sdk-network-providers": "^2.0.0",
```
{% endcode %}

## Step 2:&#x20;

Prepare your Data Streams, NFT Image Files, NFT Metadata files&#x20;

In this example, we choose to use centralized service URLs for everything.

Data Stream:

* A single backend server endpoint was used: [https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo)
* The route above is Native Auth token protected. The Data Marshal will verify ownership of the Data NFT and then forward the Native Auth token to the endpoint above, which can then validate it.
* The route above also uses the request headers passed in via the marshal, i.e. “itm-marshal-fwd-chainid” and “itm-marshal-fwd-tokenid” to make the stream dynamic based on token ID and chain ID. See below for an example of the raw stream contents once it’s connected to a Data NFT and opened in the Explorer App’s Data NFT wallet
* You can choose to follow this single backend server endpoint OR have separate Data Stream endpoints for each Data NFTs if you choose
* It’s HIGHLY recommended that you abstract it via a Domain Name (like above) so you can change the infrastructure as needed.

#### NFT Image and Metadata Files:

* We choose to use centralized, dynamic URLs for the image and metadata files. This way you can do things like dynamic image layers etc if you want. But the choice is yours, you can use static IPFS assets if you want.&#x20;

**Our Image Service:**\
[https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicImageDemo/GIFTXED1](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicImageDemo/GIFTXED1)

* The GIFTXED1 is actually the “token name” you pick when you mint the token. The number 1 on the end can be the incrementing number that makes the token name unique. Note that you CAN’t use the Data NFT Identifier on this as you won’t know it for “sure” until AFTER you mint the NFT. You could “guess" it based on auto incrementing Nonce but maybe this may have some issues related to it.
* In our example, based on the “token name” sent to the NFT image service, we get a unique image generated on the fly. E.g.\
  \
  ![](https://lh7-us.googleusercontent.com/OcUxmh15Ky4dk92_4lTxL1_u4T-AnJqpmVNrZsf_6fS2bGae97iIYWuxMNvZB2TbDv_UhDHxCd7gcgX_LF74cIm-25AbozSdt7FW4DC38OihJqkWY0lVHZ4ukFC00lxkwV8buIMj4A9ZFGhYR3CTRZI)

**Our Metadata Service:**\
Similar to the image, we use a dynamic URL based on the “token name”: [https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTXED1\
\
](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTXED1)Note that there are some “minimum” attributes you need to have in your file to make it compatible with other Data NFTs. here is the minimum file format - [https://github.com/Itheum/sdk-mx-data-nft#traits-structure\
\
](https://github.com/Itheum/sdk-mx-data-nft#traits-structure)But you can checkout the above [https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTXED1](https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTXED1) for a sample as well

## Step 3: Import the libs you need and init them

Firstly, it’s very important to login via a wallet that you want to be “Admin” of a new Minter Contract and your new NFT collection.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
import { Address, Transaction } from "@multiversx/sdk-core/out";
import { refreshAccount } from "@multiversx/sdk-dapp/utils/account";
import { NftMinter, ContractConfiguration } from "@itheum/sdk-mx-data-nft";
import { Factory, DeployedContract } from "@itheum/sdk-mx-enterprise";

const factory = new Factory("devnet");
const { address } = useGetAccount(); // this is your address. I.e. “Admin” and it’s used in many places below
```
{% endcode %}

## Step 4: Using Itheum Enterprise to get whitelisted

Use the below commands to check if you are whitelisted. If you are not and whitelisting is turned on, then reach out to the itheum foundation to get whitelisted.

Note that Itheum Enterprise let’s you deploy Data NFT-Lease “Minters”

{% code lineNumbers="true" fullWidth="true" %}
```javascript
const requireWhitelisting = await factory.viewWhitelistEnabledState();

// if requireWhitelisting is true, then you need to make sure your admin address is whitelisted. If it’s false, then whitelisting is turned off and anyone can continue

// Check if you are whitelisted (SKIP THIS IF WHITELISTING IS NOT REQUIRED)
const isWhitelisted = await factory.viewAddressIsWhitelisted(new Address(address));
console.log("Is whitelisted: ", isWhitelisted);
```
{% endcode %}

## Step 5: Check for the latest software versions available and deploy a specific version of a Minter contract

The factory can provide various versions of the Minter contract, these are most likely to be backwards compatible versions of the same contract and it’s usually advisable to ALWAYS use the latest version. But the choice is yours as it’s a decentralised system and you get to decide what version you want, accept the risks and proceed.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
// View versions available for deployment in the factory
const versions = await factory.viewVersions();
console.log("Versions: ", versions); // [‘0.0.1’]

// we can deploy 0.0.1 version if we want, let’s do that now
const minterVersion = "0.0.1"
try {
    const txToIssue: Transaction = factory.deployContract(new Address(address), minterVersion);

    await refreshAccount();

    const { sessionId, error } = await sendTransactions({
        transactions: txToIssue,
        transactionsDisplayInfo: {
        processingMessage: "Deploying new Enterprise Minter",
        errorMessage: "Minter deploying error",
        successMessage: "Minter deployed successfully",
      },
      redirectAfterSign: false,
    });
// if no error, then it’s a success
} catch (e) {
    console.error(e);
}
```
{% endcode %}

## Step 6: Find your Minters and Initialize a DataNFT object to work with your Minters

You can deploy many Minters if you want from your same Admin account, although this is not a good idea as it can pollute the blockchain. If you have multiple minters, find your Minters and use one to initialise a DataNFT instance to continue working with your Minter and the NFT collection it oversees

{% code lineNumbers="true" fullWidth="true" %}
```javascript
// Find your minters
const deployedContracts: DeployedContract[] = await factory.viewAddressContracts(new Address(address));
console.log("Deployed contract: ", deployedContracts);
// you will get an array of minter contracts you own [{owner: ‘erd1...xxx’, address: ‘erd1..yyy’, version: ‘0.0.1’}]

// owner is your Admin address? I.e. the owner of the Minter
// address is your Minter contracts address
// version is the version of code you are running 

const minterSCAddressToWorkWith = ‘erd1..yyy’;

// Initialize the NFT Minter
const deployedMinterContractAddress = new Address(minterSCAddressToWorkWith);

// the environment: 'devnet' etc ... should be the same as in factory
const nftMinter = new NftMinter("devnet", deployedMinterContractAddress);
// nftMinter is now an instance of the minter so you can run actions on it
```
{% endcode %}

## Step 7: Deploy your “base” Data NFT-Lease collection

We are now ready to deploy our Data NFT base collection. It’s a “base” collection as it wont have any tokens inside it.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
const newCollectionName = ‘LoyaltyXV1’; // name of your NFT collection
const newCollectionTicker = ‘DATALT1’; // ticker for your NFT collection. No spaces and less than 10 chars;
const secondsBetweenMint = 5; // apply some “delay” between mints in seconds. I.e. wait 5 seconds to mint again
const enabledAntiSpamTax = false; // turn this off to disable any minting anti-spam tax
const whoShouldGetRoyalties = new Address(‘erd1...zzz); // this is a address you own that will get all royalties once you claim it

const txToIssue: Transaction = nftMinter.initializeContract(
    new Address(address),
    newCollectionName,
    newCollectionTicker,
    secondsBetweenMint,
    enabledAntiSpamTax,
    whoShouldGetRoyalties
);

await refreshAccount();
```
{% endcode %}

## Step 8: View your “base” Data NFT-Lease collection’s configuration at anytime

You can view key settings of your minter + collection like so. You can run this at any time to check the on-chain settings for your minter + collection.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
// Check settings and configuration
const viewConfigurations: ContractConfiguration = await nftMinter.viewContractConfiguration();
setSdkResponses(`My minter configuration is: ${JSON.stringify(viewConfigurations)}`);

// initially, it will look similar to this
/*
administratorAddress: "erd1qmsq6ej344kpn8mc9xfngjhyla3zd6lqdm4zxx6653jee6rfq3ns3fkcc7" 
claimsAddress: "erd1qmsq6ej344kpn8mc9xfngjhyla3zd6lqdm4zxx6653jee6rfq3ns3fkcc7" 
isContractPaused: true 
isTaxRequired: false 
isWhitelistEnabled: true 
maxRoyalties: 8000 
minRoyalties: 0 
mintTimeLimit: 5 
mintedTokens: 0 
rolesAreSet: false 
tokenIdentifier: "DATALT1-4e6fb5"
*/


// isContractPaused is true, this means the minter is paused for your protection
// isWhitelistEnabled is true, which means only whitelisted addresses can mint
// tokenIdentifier if you base NFT collections identifier
```
{% endcode %}

## Step 9: It’s recommended to “prevent transferability” initially.

As a 1st step, we will make the NFT collection non-transferable. You can always change this later and make it fully transferable or you can pick specific smart contracts or addresses that can send and receive your tokens. E.g. only allow tokens to be traded on the Itheum Data DEX so it can benefit from live data stream checks, or allow for tokens to be sent to a distributor contract or an escrow contract to allow for movement between a user’s wallets or to a lending contract. Or you can remove all restrictions and make the tokens fully transferable.

But let’s begin by making the tokens non-transferable by calling the setLocalRoles method.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
try {
    const txToIssue: Transaction = nftMinter.setLocalRoles(new Address(address));

    await refreshAccount();

    const { sessionId, error } = await sendTransactions({
        transactions: txToIssue,
        transactionsDisplayInfo: {
        processingMessage: "set local roles for minter",
        errorMessage: "Set local roles error",
        successMessage: "Set local roles success",
        },
        redirectAfterSign: false,
    });
} catch (e) {
    console.error(e);
}
```
{% endcode %}

## Step 10: Whitelist yourself or another address you own to mint tokens

The model used for Data NFT-Lease collections is the pre-mint method, where you can per-mint tokens and then send them to a distribution contract to launch them based on rules you may have. Let’s assume you want to pre-mint a 5k collection. You 1st need to whitelist a wallet that can call the mint. This can be your current minter “admin” if you want to keep it simple, or it can be some other wallet.

In the example below, let’s 1st check the current minting whitelist and then whitelist own selves (admin) to mint

{% code lineNumbers="true" fullWidth="true" %}
```javascript
// check at any time on who can mint. You will get a array of addresses
const result = await nftMinter.viewWhitelist();
setSdkResponses(`Current minting whitelist is : ${result.toString()}`); // initially, this will be empty

// let’s whitelist ourselves (i.e. erd1...xxx)

try {
  const addressesToWhitelist = [‘erd1...xxx’]; // erd1...xxx will be able to mint
  const addressStringsToArray = addressesToWhitelist;
  const txToIssue: Transaction = nftMinter.whitelist(new Address(address), addressStringsToArray);

  await refreshAccount();

  const { sessionId, error } = await sendTransactions({
    transactions: txToIssue,
    transactionsDisplayInfo: {
    processingMessage: "Whitelisting for mint",
    errorMessage: "Whitelisting for mint error",
    successMessage: "Whitelisting for mint success",
  },
    redirectAfterSign: false,
  });
  } catch (e) {
    console.error(e);
  }

```
{% endcode %}

## Step 11: View if the contract is paused and UnPause the contract

Before you start minting, you will need to unpause the minter contract. In the below example, we check if the contract is paused and then unpause it if needed. You can also learn how to “pause” the contract during emergencies.

<pre class="language-javascript" data-line-numbers data-full-width="true"><code class="lang-javascript">// View contract pause state
const result = await nftMinter.viewContractPauseState();
setSdkResponses(`Minter pause state is : ${result}`);

<strong>// we can unpause (or pause) as needed like so
</strong>try {
  let txToIssue: Transaction | null = null;

  const setPause = false; // here we want to unpause

  if (setPause) {
    txToIssue = nftMinter.pauseContract(new Address(address));
  } else {
    txToIssue = nftMinter.unpauseContract(new Address(address));
  }

  await refreshAccount();

  const { sessionId, error } = await sendTransactions({
    transactions: txToIssue,
    transactionsDisplayInfo: {
    processingMessage: "Toggling pause state for minter",
    errorMessage: "Toggling pause state error",
    successMessage: "Toggling pause state success",
  },
    redirectAfterSign: false,
  });
} catch (e) {
  console.error(e);
}
</code></pre>

## Step 12: You are now ready to “Mint”!

You can now start to pre-mint your NFT collection. There are few things to note here:

* You should mint in batches. If you are minting a 5k collection. Maybe mint in 50 token batches so you can monitor the process
  * You also DO NOT need to pre-mint everything. If your total collection is 5k but you only need 500 in the 1st distribution. Just mint 500 to begin with, you can also mint the rest later.
* The below example is using SDk Core and Front End minting. This is not recommended as it will be slow as you need to sign each transaction individually.&#x20;
  * With our SDK you could use TypeScript as well and do batch transactions. Recommended.
  * Or if you want to use a Python script, you could interact directly with the Minter smart contract’s mint method. But this is a bit messy as using the SDK will handle all the validation and complexities around using the Data Marshal.

Below we provide 2 examples of using front end code which we have confirmed works… but also a typescript example with batch minting.

### Using Front End Code for Minting:

{% code lineNumbers="true" fullWidth="true" %}
```javascript
try {
  const nftBatchMintStartIndex = 1; // start with 1. As described in step 2, this is the “incrementing” number we use to make unique image, metadata URLs and token name and tickers 

  if (nftBatchMintStartIndex > 0) {
    const tknIdx = nftBatchMintStartIndex;

  const txToIssue: Transaction = await nftMinter.mint(
    new Address(address),
    `GIFTXED${tknIdx}`, // Short token Name (between 3 and 20 alphanumeric characters - no spaces)
    "https://api.itheumcloud-stg.com/datamarshalapi/router/v1", // The Data Marshal endpoint
    "https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo", // The Data Stream URL
    "https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/Random/nopreview.png", // The Public Preview URL
    500, // Royalty in % with 2 trailing zeros (e.g. 1500 is 15% or 500 would be 5% or 0 would be 0%. Max is 5000 of 50%)
    `GiftX Edition 1 Card No ${tknIdx}`, // Title (between 10 and 60 alphanumeric characters with spaces allowed)
    `Itheum GiftX Card Super Rare 1st Edition Card No ${tknIdx}`, // Description (between 10 and 400 alphanumeric characters with spaces allowed)
    {
      imageUrl: `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicImageDemo/GIFTX_ED_${tknIdx}`,
      traitsUrl: `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTX_ED_${tknIdx}`,
    }
  );

  await refreshAccount();

  // Note: if the transaction fails due to the gas limit you can apply your own gas limit before signing.
  // txToIssue.setGasLimit(100000000);

  const { sessionId, error } = await sendTransactions({
    transactions: txToIssue,
    transactionsDisplayInfo: {
      processingMessage: "Minting NFT",
      errorMessage: "Minting NFT error",
      successMessage: "Minting NFT success",
    },
    redirectAfterSign: false,
    });
  }
} catch (e) {
  console.error(e);
}
```
{% endcode %}

### Using below is a Back End TypeScript Code for Batch Minting:

{% code lineNumbers="true" fullWidth="true" %}
```javascript
import { NftMinter } from "@itheum/sdk-mx-data-nft/out";
import { DeployedContract, Factory } from "@itheum/sdk-mx-enterprise/out";
import { Account, Address } from "@multiversx/sdk-core/out";
import { ApiNetworkProvider } from "@multiversx/sdk-network-providers/out";
import { UserSecretKey, UserSigner } from "@multiversx/sdk-wallet/out";
import * as fs from "fs";

const pemFilePath2 = "../wallet2.pem"; // this is your "admin" wallet that has the rights to "mint"
const networkProvider = new ApiNetworkProvider("https://devnet-api.multiversx.com", {
  timeout: 10000,
});
const nftMinterDeployerPem = fs.readFileSync(pemFilePath2);
const nftMinterDeployer = UserSecretKey.fromPem(nftMinterDeployerPem.toString());
const nftMinterDeployerAddress = nftMinterDeployer.generatePublicKey().toAddress();
const nftMinterDeployerSigner = new UserSigner(nftMinterDeployer);

async function main() {
  // Sync your account
  let nftMinterDeployerAccount = new Account(nftMinterDeployerAddress);
  let nftMinterDeployerAccountOnNetwork = await networkProvider.getAccount(nftMinterDeployerAddress);
  nftMinterDeployerAccount.update(nftMinterDeployerAccountOnNetwork);

  // Initialize the Itheum Factory
  const factory = new Factory("devnet");

  // Check your deployed contract address
  const deployedContract: DeployedContract[] = await factory.viewAddressContracts(nftMinterDeployerAddress);
  console.log("Deployed contract: ", deployedContract);

  // Initialize the NFT Minter
  const deployedMinterContractAddress = new Address(deployedContract[0].address);

  // the environment: 'devnet' etc ... should be the same as in factory
  const nftMinter = new NftMinter("devnet", deployedMinterContractAddress);

  // Mint multiple NFTs
  const txsToSend = [];

  // let's mint a batch of 5
  for (let i = 0; i < 5; i++) {
    // Hover mint to see more options to use your own image and metadata
    const tx = await nftMinter.mint(
    nftMinterDeployerAddress,
    `GIFTXED${i}`,
    "https://api.itheumcloud-stg.com/datamarshalapi/router/v1",
    "https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicSecureDataStreamDemo",
    "https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/Random/nopreview.png",
    500,
    `GiftX Edition 1 Card No ${i}`,
    `Itheum GiftX Card Super Rare 1st Edition Card No ${i}`,
    {
      imageUrl: `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicImageDemo/GIFTX_ED_${i}`,
      traitsUrl: `https://api.itheumcloud-stg.com/datadexapi/bespoke/dynamicMetadataDemo/GIFTX_ED_${i}`,
    }
    );

    tx.setNonce(nftMinterDeployerAccount.getNonceThenIncrement());
    const signature = await nftMinterDeployerSigner.sign(tx.serializeForSigning());

    tx.applySignature(signature);
    txsToSend.push(tx);

    console.log(tx.getHash().toString());
  }

  // send all transactions
  networkProvider.sendTransactions(txsToSend);
}

main();
```
{% endcode %}

## Step 13: Controlling “Transferability” of your tokens

In the previous step, as you mint the tokens are sent to the minter’s wallet. As the tokens are currently fully non-transferable, the tokens will remain in the minter's wallet. This is most likely NOT what you want. In reality, you will probably want take your collection into one of the following launch paths:

Let’s assume you batch minted 5k NFTs and they are in the Minter’s wallet

Launch Path 1 (strategic launch, incremental open market trade):

* You want to move the 5k tokens into a “distribution” contract and plan your launch event
* Your launch event controls where the tokens can be traded in a strategic way
  * You want to “prevent” users trading it peer-to-peer
    * But only allow for users to move it between their wallets via a “escrow broker” service
  * You begin to only allow trading of tokens in the Itheum Data DEX as it offers “uptime checks on Data Streams” and some guardrails on how “max price” (to prevent pump and dumps), how many you can buy per tx etc
  * After some observation, you then want to allow for trade to happen on XOXNo and FrameIt
  * Eventually, you can make the collection fully transferable and then let the tokens be traded anywhere and peer to peer

To launch as above, we can use the following methods in the SDK. Based on the current setup so far, the NFT collection already prevents “peer-to-peer” movements of tokens. So let’s do the following:

### A) Enable the tokens to be traded on the itheum Data DEX

We know that on [devnet](https://test.datadex.itheum.io/), the Data DEX smart contract is erd1qqqqqqqqqqqqqpgqrwtl03qdxjv2e52ta5ry4rg0z7l95neqfsxsp4y4xh

{% code lineNumbers="true" fullWidth="true" %}
```javascript
try {
  const txToIssue: Transaction = nftMinter.setTransferRole(new Address(address), new Address(‘erd1qqqqqqqqqqqqqpgqrwtl03qdxjv2e52ta5ry4rg0z7l95neqfsxsp4y4xh’));

  await refreshAccount();

  // Note: if the transaction fails due to gas limit you can apply your own gas limit before signing.
  txToIssue.setGasLimit(100000000);

  const { sessionId, error } = await sendTransactions({
    transactions: txToIssue,
    transactionsDisplayInfo: {
    processingMessage: "Set transfer roles",
    errorMessage: "Set transfer roles error",
    successMessage: "Set transfer roles success",
  },
    redirectAfterSign: false,
  });
} catch (e) {
  console.error(e);
}
```
{% endcode %}

Users can now go to the Data DEX, view their Data NFTs in their wallet and openly trade them as needed in the Data DEX.

### B) Enable the tokens to be traded on FrameIT

Let’s now assume that you want your Data NFTs to be traded on FrameIT and we want to test this on devnet. E.g. This is FrameIT’s devnet app and a sample Data NFT collection listed for testing [https://test.frameit.gg/marketplace/DATALT1-4e6fb5](https://test.frameit.gg/marketplace/DATALT1-4e6fb5). We know their smart contract is erd1qqqqqqqqqqqqqpgq3zvkz6k08c0dgqqqwnlyqkx6dej4hwqvae0s8ugk7m

So all we need to do now is to enable this smart contract as in the previous code sample.

{% code fullWidth="true" %}
```javascript
nftMinter.setTransferRole(new Address(address), new Address(‘erd1qqqqqqqqqqqqqpgq3zvkz6k08c0dgqqqwnlyqkx6dej4hwqvae0s8ugk7m’));
```
{% endcode %}

Once you do this, the Data NFTs are freely tradable on FrameIT (and the Data DEX as well)

### C) Eventually, remove all restrictions and make all tokens traded openly.

Now, let’s assume that you want to remove ALL restrictions on Data NFTs and allow the user to trade them wherever they want and also via peer to peer mechanisms, do do this, you just need to remove ALL specific smart contracts that have been assigned the setTransferRole.

To do this, we first need to get a list of addresses that have this role. We can do that like so:

{% code lineNumbers="true" fullWidth="true" %}
```javascript
const viewRoles: string[] = await nftMinter.viewTransferRoles();
setSdkResponses(`Who has transfer role : ${viewRoles.toString()}`);

// this will return an array of addresses like so
// [erd1qqqqqqqqqqqqqpgq68c98qym5tpu2n6g2hq8wx9l0q9sqqt8w3wqp9gq96, erd1qqqqqqqqqqqqqpgqrwtl03qdxjv2e52ta5ry4rg0z7l95neqfsxsp4y4xh, erd1qqqqqqqqqqqqqpgq3zvkz6k08c0dgqqqwnlyqkx6dej4hwqvae0s8ugk7m]
```
{% endcode %}

We can now use the below method, to remove all these addresses one by one.

{% code lineNumbers="true" fullWidth="true" %}
```javascript
try {
  // remove these 3 addresses one by one
  // [erd1qqqqqqqqqqqqqpgq68c98qym5tpu2n6g2hq8wx9l0q9sqqt8w3wqp9gq96, erd1qqqqqqqqqqqqqpgqrwtl03qdxjv2e52ta5ry4rg0z7l95neqfsxsp4y4xh, erd1qqqqqqqqqqqqqpgq3zvkz6k08c0dgqqqwnlyqkx6dej4hwqvae0s8ugk7m]
  const txToIssue: Transaction = nftMinter.unsetTransferRole(new Address(address), new Address(‘erd1qqqqqqqqqqqqqpgq68c98qym5tpu2n6g2hq8wx9l0q9sqqt8w3wqp9gq96’));

  await refreshAccount();

  // Note: if the transaction fails due to gas limit you can apply your own gas limit before signing.
  txToIssue.setGasLimit(100000000);

  const { sessionId, error } = await sendTransactions({
    transactions: txToIssue,
    transactionsDisplayInfo: {
    processingMessage: "Unset transfer roles",
    errorMessage: "Unset transfer roles error",
    successMessage: "Unset transfer roles success",
  },
    redirectAfterSign: false,
  });
} catch (e) {
  console.error(e);
}
```
{% endcode %}

Once you do this, your Data NFTs will become FULLY transferable and tradable everywhere

### Launch Path 2 (full open market trade):

* You want to make the tokens FULLY tradable peer-to-peer, OTC or on any marketplace. This is a fully public launch
  * You want to move the 5k tokens into a “distribution” contract and plan your launch event. After this, the tokens are fully on the public market as there are no restrictions&#x20;

To enable this path, you just need to follow C) step above.
