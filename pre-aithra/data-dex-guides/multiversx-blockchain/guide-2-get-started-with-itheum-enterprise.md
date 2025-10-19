# Guide 2: Get Started with Itheum Enterprise

{% hint style="warning" %}
This feature is in Beta and only available on devnet.
{% endhint %}

[itheum-enterprise.md](../../pre-aithra-r-and-d/itheum-enterprise.md "mention") is a product that "wraps" around the [data-nft-lease.md](../../data-nft/data-nft-types/data-nft-lease.md "mention") type of Data NFTs, but provides a powerful yet simple user interface, full flexibility, and control over your Data NFT-LEASE collection. It provides a seamless way to mint your own NFT collection, attach data to your NFTs (i.e. make them Data NFTs), and then curate, administer and manage your NFT collection - an end-to-end lifecycle for Data NFT management.\
\
In this guide, we will explore how you can get started with Itheum Enterprise by using the "Management Dashboard", a "no-code" app to interact with the Itheum Enterprise product.

***

> :checkered\_flag: <mark style="color:yellow;">🏎️</mark> <mark style="color:yellow;"></mark><mark style="color:yellow;">**Ready to start? Here are a few assumptions and pre-conditions**</mark>

* Itheum Enterprise is in "private beta" mode, so you need to be whitelisted to try it out. Reach out to us on [tech-support-discord](../../tech-support-discord/ "mention")
* This guide also is specific to the **MuiltiversX Blockchain** and will require to have a wallet from the   [supported-wallets](../../supported-wallets/ "mention") to interact with the blockchain.
* The Management Dashboard App will allow you to "deploy" your Data NFT Collection and then curate/manage multiple Data NFTs, if you'd like to mass-mint a large amount of Data NFTs, then you would need to use a "minting script" that can use the [data-nft-sdk](../../software-development-kits-sdks/data-nft-sdk/ "mention") (How you can write this "minting script" is detailed in the guide [guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md](../../software-development-kits-sdks/enterprise-sdk/guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md "mention")

***

In this detailed SDK guide, we will walk you through the process of:

1. Deploying your own Data NFT-Lease Minter smart contract using Itheum Enterprise.
2. Minting a Custom Data NFT Collection using Itheum Enterprise.
3. Curating Data NFTs using Itheum Enterprise.

But to make the guide more practical, let's first detail the a real-world user story that we will aim to achieve by following this guide.\
\
[#in-a-hurry-watch-a-demo-video-of-this-guide](guide-2-get-started-with-itheum-enterprise.md#in-a-hurry-watch-a-demo-video-of-this-guide "mention") if you want a quick intro to getting started with Itheum Enterprise.\


## Target User Story:

{% hint style="info" %}
As an integrator of the Itheum web3 Data Brokerage infrastructure:

* I'd like to use the Management Dashboard App & the [data-nft-sdk](../../software-development-kits-sdks/data-nft-sdk/ "mention") to mint a 5,000 Data NFT collection using Itheum Enterprise.&#x20;
* This collection should have its own image (not the Itheum generative image service).&#x20;
* The Data Stream on the Data NFTs should also be public but protected by implementing authentication via a`Bearer` token header (Using MultiversX Native Auth - see [multiversx-native-auth-protected-api.md](../../data-streams-guides/multiversx-native-auth-protected-api.md "mention")).&#x20;
* The Data Stream should also be "personalized", where they can read a session of a user (address, NFT Token ID) and provide some level of runtime customization before streaming the data out. (e.g. NFT trade history or address on-chain behaviour. etc.)
{% endhint %}

***

## Step 1: Access Itheum Enterprise

We will now start by accessing the Management Console App.

1. Log into the Data DEX using your wallet:
   1. Mainnet: [https://datadex.itheum.io](https://test.datadex.itheum.io/)
   2. Devnet: [https://test.datadex.itheum.io](https://test.datadex.itheum.io/)
2. Once you have logged in, head over to the Itheum Enterprise section.
   1. Mainnet:  [https://datadex.itheum.io/enterprise](https://datadex.itheum.io/enterprise)
   2. Devnet: [https://test.datadex.itheum.io/enterprise](https://test.datadex.itheum.io/enterprise)
3. User will be able to view initial enterprise settings and can initiate a new minter contract.

Note: The minter contract will be used to launch the actual Data NFT collection.

<figure><img src="../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

## Step 2: Deploy your own Data NFT-Lease Minter Smart Contract

1. Check "I have read and agree to the terms of use".
2. Click on "Deploy new Minter".
3. Sign the transaction.

<figure><img src="../../../.gitbook/assets/image (126).png" alt=""><figcaption></figcaption></figure>

## Step 3: Setup your new Data NFT-Lease Collection

1. In the next part of the wizard the enter the details of your collection.
2. Enter the necessary fields and click on launch.&#x20;
3. Confirm the transaction in the wallet.

Note: It is not mandatory to set a mint **Tax**. However if it is set then every time a Data NFT is minted, the specified amount of tokens will be collected as a "fee" or "tax" by you. This is useful if you have "on-demand" batch or single mints, where you allow the public to mint-on-demand and want to set a "tax/fee" to prevent spamming of minting. But in most use-cases, you will be minting the entire collection yourself before you distribute it, and should therefore set the mint Tax to 0.

<figure><img src="../../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

## Step 4: Mint Data NFT collection

1. **Unpause** the Minter first. The Minter has to be unpaused to enable minting of data NFTs. The admin can choose to **Pause** the minter contract later on if required (Pausing can be used prevent any unauthorized or accidental minting).
2. Under "**Transfer Control**" click on "**Enable**" to enable the collection to be **Transferrable**. This is another requirement to enable minting of Data NFTs within the collection. This is required to ensure that once the Mint is complete, the NFT tokens end up in your minter wallet, after which you can choose how you would like to distribute them. You can always **Disable** transferability at a later time or after the mint is complete to make the entire Data NFT collection non-transferable.

<figure><img src="../../../.gitbook/assets/image (129).png" alt=""><figcaption></figcaption></figure>

3. Add addresses under "**Allow Address To Transfer**". This allows a contract/address to transfer the Data NFT. By using this feature, you can control who can accept or transfer Data NFTs. This feature is useful if  (after minting and distribution) you want to make your Data NFTs "conditionally" transferable. i.e. tradable on selected NFT marketplaces etc
4. Add Address under "**Add Address to whitelist**". This will permit addresses to invoke the minter to mint new Data NFTs. We can add a bulk minting address here that can utilize a "minting script" that uses the [data-nft-sdk](../../software-development-kits-sdks/data-nft-sdk/ "mention") to bulk mint a whole collection in one-go or in batches (How you can write this "minting script" is detailed in the guide [guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md](../../software-development-kits-sdks/enterprise-sdk/guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md "mention")

<figure><img src="../../../.gitbook/assets/image (131).png" alt=""><figcaption></figcaption></figure>

5. Finally you should enter a wallet address where **Creator Royalties** will be received when your Data NFTs are traded. These royalties will be sent to the designated address when you "self-claim" the royalties at anytime.

<figure><img src="../../../.gitbook/assets/image (132).png" alt=""><figcaption></figcaption></figure>

6.  Now we are set to create an actual Data NFT or mint NFTs in bulk.

    * When minting a single Data NFT, mainly for test purposes, users will be required to enter details of the single Data NFT and click on "Click here to mint". Once the transaction is signed the Data NFT will be minted.
    * Outside of "test" purposes, if you want to mint you final Data NFT collection, you will most likely use minting script that uses the [data-nft-sdk](../../software-development-kits-sdks/data-nft-sdk/ "mention") to bulk mint a whole collection in one-go or in batches (See here : [guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md](../../software-development-kits-sdks/enterprise-sdk/guide-1-using-itheum-enterprise-to-mint-a-data-nft-collection-e.g.-nft-loyalty-card-solution.md "mention")
      * When using a "minting script" as per the guide above, you will need to initialize the Data NFT SDK to use your new "Minter Smart Contract" address, after which you can programatically interact with your Data NFT collection using code and bulk mint as per your requirements.



    <figure><img src="../../../.gitbook/assets/image (133).png" alt=""><figcaption></figcaption></figure>

## Step 5: Curate your Data NFTs

With the Itheum Enterprise Management Console app, users can **freeze** specific Data NFTs. Once the Data NFT is frozen the the holder will not be able to transfer the specific NFT from their wallet. This is useful for any regulation or compliance needs.

1. Head on to the **Curate Your Data NFTs** section on datadex.itheum.io/enterprise.
2. Select the specific Data NFT you wish to freeze and click on "**Freeze**".
3. Confirm the transaction in the wallet.

Once the transaction is concluded the Data NFT will be frozen and non-transferrable from the user account.

<figure><img src="../../../.gitbook/assets/image (134).png" alt=""><figcaption></figcaption></figure>

Once the Data NFT is frozen there are 2 action that can be performed on the Data NFT. The admin can either choose to U**nfreeze** the Data NFT or **Wipe** that specific data NFT. This is useful for any regulation or compliance needs.

If the admin chooses to **unfreeze** the Data NFT, then it would return to a normal state and be transferrable as usual.

If the admin chooses to **Wipe** a Data NFT, then the specific Data NFT will be purged from the NFT Collection (but note that as it's using Blockchain technology, the NFT cannot be "deleted" completely, it simple is removed from circulation and is in a purged and unrecoverable state). In order to **Wipe** a data NFT the following steps are to be executed.

1. Firstly **Freeze** a Data NFT
2. Once frozen the admin will be able to see an option to **Wipe**.
3. Click on **Wipe** For that specific Data NFT and confirm the transaction.

Note: Once a Data NFT has been Wiped there is no way to recover the item.&#x20;

<figure><img src="../../../.gitbook/assets/image (135).png" alt=""><figcaption></figcaption></figure>

***

## In a Hurry? Watch a Demo Video of this Guide

{% hint style="warning" %}
Itheum Enterprise is still in "beta," so many new features and UI updates are being released weekly, so the user interface in this demo video may appear different from what is available in the live software. We recommend you follow the written guide above for the latest version of the user interface and feature set options.
{% endhint %}

{% embed url="https://www.youtube.com/watch?v=x9pdCjNlpl0" %}





