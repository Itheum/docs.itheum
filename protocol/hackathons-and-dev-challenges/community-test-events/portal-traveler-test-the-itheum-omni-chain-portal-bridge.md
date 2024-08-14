# Portal Traveler 🌀 : Test the Itheum Omni-Chain Portal (Bridge)

## Introduction

Be part of the first cohort of users who test the Itheum Protocol Omni-Chain Portal! The Portal Traveler test event aims to stress test Itheum's Omni-Chain bridge, that enables for the bridging of $ITHEUM tokens and other protocol assets (e.g. Data NFTs) between blockchains. Testing during the phases detailed below will earn you BiTz XP points, which can unlock further rewards.

***

## Phase 1:

### Scope:

* Phase 1 of the test event will focus on the testing of the bridging of $ITHEUM tokens between MultiversX and Solana in a "devnet" environment (i.e. no real value/mainnet tokens used)
* Primarily aimed for BitZ XP Data NFT holders, don't have a BiTz XP Data NFT? no worries, you will be airdropped this Data NFT once the test event concludes along with BITz X points. Existing BitZ XP Data NFT holders will get boosted rewards.

### Test Dates:

* Start Data: 7 June (Friday) 2024
* End Date:  11 June (Tuesday) 2024

### Base Rewards:

* Completing all **Actions** steps below as detailed in the Test Steps below, will get you a total of 250 BiTz XP
* Completing all **Actions** steps multiple times (up to 5), will get you a bonus 100 BiTz XP per try. e.g. if you complete it an extra 5 times, your will get a extra 500 BiTz XP!
* Existing Mainnet BiTz XP holders, get a 2X boosted reward if they complete all steps, so you would get 500 BITz XP
  * To ensure you get your rewards and boosts, make sure you use your Mainnet wallet that holds the BiTz XP Data NFT. You can use this same wallet on devnet without an issue.
* BiTz XP rewards will be sent to the participating wallets within 15 days after Phase 1 End Date.

#### **Bonus Rewards for Repeating Actions:**&#x20;

* First 100 participants, get a BiTz XP Data NFT airdropped on both the MultiversX and Solana Mainnets! (yes, BiTz XP works on Solana as well!)
* Random 10 participants get 2000 $ITHEUM token airdrop
* Random 5 participants get 5 unique Data NFT Pack

#### Bonus Rewards for Reporting Bugs:

* "Backend" Bugs: Any bugs reported that are related to the "backend" (relayers or smart contracts) that our confirmed by our team, will get you 750 BiTz XP each. "backend" bugs are usually discovered when you monitor the MultiversX Smart Contract and Solana Program as you test the app, and discover some anomalies in the amount of tokens you bridge. When you submit your bug report, please provide as much context and evidence (Transaction links, screen shots etc)
  * MultiversX Bridge Smart Contract: [https://devnet-explorer.multiversx.com/accounts/erd1qqqqqqqqqqqqqpgq2ydact8802td4n7k5zu86zdjz7r65esaw3wq2884uu](https://devnet-explorer.multiversx.com/accounts/erd1qqqqqqqqqqqqqpgq2ydact8802td4n7k5zu86zdjz7r65esaw3wq2884uu)
  * Solana Bridge Program: [https://explorer.solana.com/address/biTbWdTDYmv9ykUoXxFWdNAR38Qwe9HGVWaPJ4hRMk7?cluster=devnet](https://explorer.solana.com/address/biTbWdTDYmv9ykUoXxFWdNAR38Qwe9HGVWaPJ4hRMk7?cluster=devnet)
* "Frontend" Bugs: These are bugs that are on the UI, the UI is a work in progress there there may be plenty of "small to medium" issues, but if you discover any major issue and it's confirmed by our team will get you 200 BiTz XP each

{% hint style="info" %}
**Submit your bug reports using this** [**feedback form**](https://forms.gle/utFkSfQyHbfjWdWv9)
{% endhint %}



### Test Scope:

#### Setup:

<mark style="background-color:green;">**Step 1:**</mark> Setup a MultiversX Wallet. Only [DeFi Wallet ](../../../integrators/supported-wallets/multiversx-defi-wallet.md)is supported for this test event. Put your wallet in "DEVNET" mode if required (but this should happen automatically when you use the Portal as it's setup in DEVNET mode only).

<mark style="background-color:green;">**Step 2:**</mark> Setup a Solana Wallet like Phantom, and put your [Phantom wallet in "devnet" mode](https://www.youtube.com/watch?v=6o9lAZv2zAs)

<mark style="background-color:green;">**Step 3:**</mark> Get some dEGLD (DEVNET EGLD), which is required for gas payment on MultiversX. Go here, [https://devnet-wallet.multiversx.com](https://devnet-wallet.multiversx.com/), login with your wallet from Step 1, and use the "Faucet" to get dEGLD. Alternately, you can use [https://r3d4.fr/faucet](https://r3d4.fr/faucet) to get dEGLD (Note! this is a 3rd party site so proceed with caution)

<mark style="background-color:green;">**Step 4:**</mark> Get some DEVNET SOL, which is required for gas payment on MultiversX. Go here: [https://faucet.solana.com/](https://faucet.solana.com/), paste your address from Step 1 and request SOL

<mark style="background-color:green;">**Step 5:**</mark> Get DEVNET ITHEUM tokens, Go here: [https://test.datadex.itheum.io/](https://test.datadex.itheum.io/), login with your wallet from Step 1, Click on "Dash" on the top menu, and click on the "Send me ITHEUM" button to get 1,000 ITHEUM tokens.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

<mark style="background-color:green;">**Step 6:**</mark> Head over to the Omni-Chain Portal: [https://alpha-devnet.portal.itheum.io/](https://alpha-devnet.portal.itheum.io/) and click on "Bridge $ITHEUM", login with your wallets from Step 1 and Step 2

<mark style="background-color:green;">**Step 7:**</mark> You should now see the following interface:

<figure><img src="../../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Actions:

{% hint style="info" %}
1. The following actions can be repeated as per Base Reward section above to get reward multipliers.&#x20;
2. The below assumes you begin the test with 1,000 $ITHEUM tokens on MultiversX DEVNET.
3. Before you begin the next actions, note down all your balances on both blockchains and at the end of all actions, confirm the balances are correct and as expected.
{% endhint %}

<mark style="background-color:orange;">**Action 1:**</mark> Bridge $100 ITHEUM from MultiversX to Solana, wait 2-5 Epochs and confirm your tokens have moved chains (i.e. $100 deducted from your balance on MultiversX and credited on Solana)

<mark style="background-color:orange;">**Action 2:**</mark> Bridge $150 ITHEUM from MultiversX to Solana, wait until the transaction is successfully complete but do NOT wait until the tokens actually bridge by waiting 2-5 Epochs like in above action, instead, immediately move onto next action.

<mark style="background-color:orange;">**Action 3:**</mark> Bridge remaining ITHEUM (e.g. $750 ITHEUM) from MultiversX to Solana, wait 2-5 Epochs and confirm your tokens from Action 2 and 3 have moved chains.

_Now all your 1,000 $ITHEUM should be on the Solana chain, and we will test a bridge back._

<mark style="background-color:orange;">**Action 4:**</mark> Bridge $100 ITHEUM from Solana to MultiversX , wait 2-5 Epochs and confirm your tokens have moved chains (i.e. $100 deducted from your balance on Solana and credited on MultiversX) - [_Getting a Request Blocked Warning by Phantom Error?_](portal-traveler-test-the-itheum-omni-chain-portal-bridge.md#getting-a-request-blocked-warning-by-phantom-error)

<mark style="background-color:orange;">**Action 5:**</mark> Bridge $150 ITHEUM from Solana to MultiversX, wait until the transaction is successfully complete but do NOT wait until the tokens actually bridge by waiting 2-5 Epochs like in above action, instead, immediately move onto next action.

<mark style="background-color:orange;">**Action 6:**</mark> Bridge remaining ITHEUM (e.g. $750 ITHEUM) from Solana to MultiversX, wait 2-5 Epochs and confirm your tokens from Action 5 and 6 have moved chains.

_Now all your 1,000 $ITHEUM should be back on the MultiversX chain, you can now repeat Actions._



**Got Questions? Head over to our Discord :** [**itheum.io/discord** ](https://itheum.io/discord)



#### Getting a Request Blocked Warning by Phantom Error?

{% hint style="warning" %}
Are you seeing this below warning by Phantom?&#x20;

This is because the _https://alpha-devnet.portal.itheum.io_ domain is flagged a s "new domain" by Phantom and it is giving you this wanting as a precaution. Also note that as you are on Solana "devnet", no mainnet access is happening. If you are still concerned about safety, we recommend that you use a new Solana wallet just for this test, and ensure it's connected to "devnet".\
\
<img src="../../../.gitbook/assets/image (2) (1) (1) (1).png" alt="" data-size="original">
{% endhint %}

