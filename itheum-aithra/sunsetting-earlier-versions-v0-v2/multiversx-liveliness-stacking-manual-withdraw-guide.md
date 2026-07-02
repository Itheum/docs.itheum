# MultiversX Liveliness Stacking - Manual Withdraw Guide

### The product UI is No Longer Supported

As per [.](./ "mention"), the MultiversX (and Solana) NFME ID + Liveness Staking/Bonding product reached **EOS (End of Support) on Jan 15, 2026**. We had [notified the community on Oct 25. 2025](https://x.com/itheum/status/1981690229648966023?s=20) that they must use the product UI [https://datadex.itheum.io](https://datadex.itheum.io/) to withdraw their tokens before the EOS date. This notification was given on all our social channels (X etc) and community channels (Telegram, Discord etc). The EOS notices was also given on our app's home screen header:

<figure><img src="../../.gitbook/assets/image (191).png" alt=""><figcaption></figcaption></figure>

Given the EOS (End of Support) on Jan 15, 2026 has passed, we are now unable to guarantee that the product UI [https://datadex.itheum.io](https://datadex.itheum.io/) will continue to work, we will try our best to keep it running for as long as possible but due to technical drift of the underlying MultiversX blockchain tech stack, it's not guaranteed to work anymore (as we have had many issues with standard network infra like RPCs, wallets etc in the past). We are also in the midst of building and launching new technology products so we also cannot guarantee the security of the EOS Data DEX product anymore, as such, if we can't support and secure the tech we may decide to take it down permanently at anytime as per standard industry standards to remove unsupported software from public use/risk.&#x20;

### But I may still have ITHEUM tokens locked in Liveliness, How can I withdraw this?

The good news is that Itheum is a decentralized protocol so our underlying technology is powered by public smart contracts and you will be able to directly interact with them to prove ownership of your tokens and withdraw them out. To make it easier for you, we have written detailed steps and provided some helper scripts on how this can be done. Note that it MAY require a BIT of technical skills on your computer to get it to work, if you are uncomfortable with this, we'd recommend you work with a friend or family member who may have tech skills to help.\
\
**Here are the steps you need to follow:**

#### **Step 1:**

To proceed you first need to know which **Wallet** you bonded with and which **Data NFT (nonce)** you bonded with. This maybe very easy to find...&#x20;

There are 2 ways to do this:\
\
**Non-Technical Way:**\
You already know which wallet address you used for sure, so you just need to find the Data NFT (nonce) you bonded with. If you are unsure of the Nonce you can check the MultiversX Explorer for SFTs from our Data NFT collection that sit in your wallet. If you only have 1 bond, then you can get the nonce easily. This e.g. below shows a Devnet Data NFT, but finding one on your Mainnet wallet should be very similar. Example:\
[https://devnet-explorer.multiversx.com/nfts/DATANFTFT-e0b917-01d1/transactions](https://devnet-explorer.multiversx.com/nfts/DATANFTFT-e0b917-01d1/transactions) - here we see the `token_identifier` and the `nonce` . i.e. nonce is "**465**" from the "**DATANFTFT-e0b917**" collection is the token identifier,  owned by (you) **erd1f02qxj7zcds358dlytw25ggtcwvuwd054c7mgk8hnnqwqq0hnp4sad5209**"

<figure><img src="../../.gitbook/assets/image (193).png" alt=""><figcaption></figcaption></figure>



**Technical Way:**\
If you have many Data NFTs ( they are actually SFTs) and cant remember which SFT was used to bond, we have 2 `Shell scripts` you can use to try and find it. This may require you to have a bit of technical experience.

**Script 1: If you have `mypx (multiversX Python CLI), python3, curl and a shell script` installed you can use this script to find your bonds:** [**https://github.com/Itheum/data-assets/blob/main/Scripts/LivelinessSelfWithdrawHelp/query-address-bonds.sh**](https://github.com/Itheum/data-assets/blob/main/Scripts/LivelinessSelfWithdrawHelp/query-address-bonds.sh)

_(download above shell script to our computer)_

Run it like so:\
`./query-address-bonds.sh erd1f02qxj7zcds358dlytw25ggtcwvuwd054c7mgk8hnnqwqq`\
`0hnp4sad5209`

In the example above, note that you need to replace _erd1f02qxj7zcds358dlytw25ggtcwvuwd054c7mgk8hnnqwqq_ is the wallet you bonded with.&#x20;

Once you run the above command, you will see an output like this:

<figure><img src="../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>

These list all the active bonds you have! and for each bond you can easily see the "nonce" e.g. 618 and "token\_identifier"



**Script 2: If you DON'T have `mypx`. But have `python3, curl and a shell script` installed (these are very standard tools in most computers) you can use this script to find your bonds:** [**https://github.com/Itheum/data-assets/blob/main/Scripts/LivelinessSelfWithdrawHelp/query-address-bonds-raw.sh**](https://github.com/Itheum/data-assets/blob/main/Scripts/LivelinessSelfWithdrawHelp/query-address-bonds-raw.sh)&#x20;

_(download above shell script to our computer)_

Run it like so:\
`./query-address-bonds-raw.sh 4bd4034bc2c3611a1dbf22dcaa210bc399c735f4ae3db458f79cc0e001f7986b`

In the example above, note that _4bd4034bc2c3611a1dbf22dcaa210bc399c735f4ae3db458f79cc0e001f7986b_ is actually the hex version of your address _erd1f02qxj7zcds358dlytw25ggtcwvuwd054c7mgk8hnnqwqq so you need to convert it._ You should convert your own address!

To convert your address to hex. Go to [https://utils.multiversx.com/converters](https://utils.multiversx.com/converters) and use the "**Convert a bech32 address to a hexadecimal address**" tool for this.

<figure><img src="../../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

Next, once you run the above command, you will see an output like this:

<figure><img src="../../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

These list all the active bonds you have! and for each bond you can easily see the "nonce" e.g. 618 and "token\_identifier"

#### **Step 2:**

Next, now that you know the `token_identifier` and the `nonce` of the bond you want to withdraw, you can issue a "withdraw" transaction from the MultiversX wallet to get your ITHEUM tokens. You can do this on any of the main MultiversX wallets (Browser Wallet, Web Wallet etc) and your tokens are immediately returned!&#x20;

Let's assume your wallet is _**erd1f02qxj7zcds358dlytw25ggtcwvuwd054c7mgk8hnnqwqq0hnp4sad5209**_ and is on the **MultiversX Browser Plugin wallet** and you want to withdraw your "**650**" bond.

Here is how you do it:

{% hint style="info" %}
Note: The address _**erd1qqqqqqqqqqqqqpgq9yfa4vcmtmn55z0e5n84zphf2uuuxxw9c77qgqqwkn** in the_ **Receiver** field below is the **official** **Itheum Liveliness Smart Contract.**
{% endhint %}

**A) Login to your wallet that owns the Bond.**

**B) Click on "Send" and enter the details:**

**Receiver:** _**erd1qqqqqqqqqqqqqpgq9yfa4vcmtmn55z0e5n84zphf2uuuxxw9c77qgqqwkn**_

**Data:** we need to convert this string: "withdraw@DATANFTFT-e936d4@650" to look like this hex value and then input it: _**withdraw@444154414e465446542d653933366434@028a**_

Here is how:

\~ Go to [https://utils.multiversx.com/converters](https://utils.multiversx.com/converters)

\~ Convert _DATANFTFT-e936d4_ to _444154414e465446542d653933366434_ using "**Convert a string to a hexadecimal encoded string**"&#x20;

<figure><img src="../../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

Convert _650_ to _028a_ using "**Convert a decimal to a hexadecimal**"&#x20;

<figure><img src="../../.gitbook/assets/image (199).png" alt=""><figcaption></figcaption></figure>

Now you can construct this **Data** string:\
&#xNAN;_**withdraw@444154414e465446542d653933366434@028a**_

Make sure you DON'T have any spaces etc. it needs to be be exact! or it will fail.

Paste this value into **Data.**

\~ **Amount:** 0 (EGLD) - _DO NOT send any EGLD!!!_

\~ Next expand **Fee** and set **Gas Limit**: 100,000,000

If you don't set this Gas Limit, the transaction will fail!

The below image is using Devnet and shows xEGLD (the devnet version of EGLD), but you can do the same with Mainnet and select EGLD.

<figure><img src="../../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure>

Then hit "**Send**" or "**Send EGLD**" (depending on your wallet)&#x20;

Once you do this, the transaction should SUCCEED if the Bond was found + active and the ITHEUM tokens will be returned to your wallet.

In case you hit any issues, make sure you double check that you have parsed the data correct as above, used a correct  `token_identifier` and  `nonce`  that you used the right wallet to sign the send the transaction. Make sure you follow the exact instructions as above and it will work.

For comparison and debugging, here is an example of a SUCCESS _withdraw_ transaction for your comparison:\
[https://explorer.multiversx.com/transactions/a608caa66d7b2a3533a9f48f258b408ce1e5cd1378dede52a64f979d8a5c37d3](https://explorer.multiversx.com/transactions/a608caa66d7b2a3533a9f48f258b408ce1e5cd1378dede52a64f979d8a5c37d3)

And that is it! Best of luck...
