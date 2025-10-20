# APR for Liveliness 🎖️: Test the Bonding + Staking Rewards Module

.&#x20;

{% hint style="info" %}
This Event has been concluded.
{% endhint %}

## **Program Overview**

## Introduction

Be part of the first cohort of users who test the Itheum Protocol Staking Program! This test event aims to stress test Itheum's new staking mechanism that allows gaining an APR for bonding ITHEUM tokens to Data NFTs.&#x20;

### Scope:

* The test event will focus on the testing of the staking mechanism of ITHEUM tokens in a "devnet" environment (i.e., no real value/mainnet tokens used).

### Test Dates:

* Start Data: 31 July (Friday) 2024
* End Date:  5 August (Tuesday) 2024

### Base Rewards:

* 100,000 $ITHEUM shared pool for this test event for those who complete the <mark style="background-color:orange;">**Actions**</mark> and <mark style="background-color:blue;">**Tasks**</mark> to a fully satisfactory level
* Completing all **Actions** steps below as detailed in the Test Steps below, will also get you a total of 800 BiTz XP

### Bonus Rewards:

* Major bonus rewards in $ITHEUM for reporting "mission critical" bugs related to security, business logic, APR or rewards calculations (Note that they need to be confirmed by our team to be an issue before rewards are sent)

{% hint style="info" %}
**Submit your bug reports using this** [**feedback form**](https://forms.gle/utFkSfQyHbfjWdWv9)
{% endhint %}

###

### Test Scope:

#### Setup:

<mark style="background-color:green;">**Step 1:**</mark> Setup a MultiversX Wallet. Only [DeFi Wallet ](../../../pre-aithra/supported-wallets/multiversx-defi-wallet.md)is supported for this test event. Put your wallet in "DEVNET" mode if required (but this should happen automatically when you use the Portal as it's setup in DEVNET mode only).

<mark style="background-color:green;">**Step 2:**</mark> Get some dEGLD (DEVNET EGLD), which is required for gas payment on MultiversX. Go here, [https://devnet-wallet.multiversx.com](https://devnet-wallet.multiversx.com/), login with your wallet from Step 1, and use the "Faucet" to get dEGLD. Alternately, you can use [https://r3d4.fr/faucet](https://r3d4.fr/faucet) to get dEGLD (Note! this is a 3rd party site so proceed with caution)

<mark style="background-color:green;">**Step 3:**</mark> Get DEVNET ITHEUM tokens, Go here: [https://test.datadex.itheum.io/](https://test.datadex.itheum.io/), login with your wallet from Step 1, Click on "Dash" on the top menu, and click on the "Send me ITHEUM" button to get 1,000 ITHEUM tokens.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt="" width="375"><figcaption><p>Get your devnet $ITHEUM from the faucet</p></figcaption></figure>

#### Actions:

{% hint style="info" %}
1. The following actions can be repeated.
2. The below assumes you begin the test with 1,000 $ITHEUM tokens on MultiversX DEVNET.
3. Before you begin the next actions, note down all your balances.
4. Note that the last step, you will need to come back in 2 days to "claim your rewards" based on the staking rewards. It's important you give these 2 day interval as we need to verify the balances as per your test.
{% endhint %}

<mark style="background-color:orange;">**Action 1:**</mark> Browse to [https://test.datadex.itheum.io/mintdata](https://test.datadex.itheum.io/mintdata) and mint a Data NFT.\
\
Make sure you click on the "**Any Data Stream as a Data NFT-FT**" option.

<figure><img src="../../../.gitbook/assets/image (163).png" alt=""><figcaption></figcaption></figure>

In the first step of the minting form, you can use any Test URLs from here:

| Data Stream URL                                                                                                                                                                                                                                        | Data Preview URL                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/M1\_\_FBI\_Firearm\_Background\_Check\_Data/pdf/dataset.pdf](https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/M1__FBI_Firearm_Background_Check_Data/pdf/dataset.pdf)     | [https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/M1\_\_FBI\_Firearm\_Background\_Check\_Data/pdf/preview.pdf](https://raw.githubusercontent.com/Itheum/data-assets/main/Misc/M1__FBI_Firearm_Background_Check_Data/pdf/preview.pdf)     |
| [https://raw.githubusercontent.com/Itheum/data-assets/main/Health/H2\_\_Visualizing\_the\_History\_of\_Pandemics/dataset.jpeg](https://raw.githubusercontent.com/Itheum/data-assets/main/Health/H2__Visualizing_the_History_of_Pandemics/dataset.jpeg) | [https://raw.githubusercontent.com/Itheum/data-assets/main/Health/H2\_\_Visualizing\_the\_History\_of\_Pandemics/preview.jpeg](https://raw.githubusercontent.com/Itheum/data-assets/main/Health/H2__Visualizing_the_History_of_Pandemics/preview.jpeg) |

Use these URLs as to go through the minting process (as below) and mint your Data NFT and confirm it's in your wallet.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9Je8hXvCFFnUSfU9GgLFfoe1VpigKkKEH0FdqpnUWyq8snX3xcFN7z4CObDrofq1tjkF4KQsAV7d9BwH1CDZhVZ-eBi0SFiu5X7MJQQrHvGxhdWtbS7kJ8hqsjwLhqOH8x3QUjv8EJnVCqY-10lSxNHY?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 2:**</mark> Once the Data NFT is minted, browse to **Wallet -> Bonding**: [https://test.datadex.itheum.io/datanfts/wallet/bonding](https://test.datadex.itheum.io/datanfts/wallet/bonding).&#x20;

Review your combined liveliness.

<mark style="background-color:blue;">**Task 1:**</mark> Take a screenshot similar to the example below that shows "Y**our Liveliness Rewards**" and "**Your Data NFT Creator Liveliness Bonds**"

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXc94VGjuCa8eliMGu3YKY1IB98eK0Or6HNaJZhkNFf_56ajgVkyMVPGsohrvjMDobPXTrE6ybSYUMMq1aD_dW8Iabxn5yPIrH9y_M62LIBM309c2p825Zzl2beHa65i4IFvX27EisZT7xqlwCqboGVgx09B?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 3:**</mark> Create an **NFMe.ID Vault Data NFT** by going to [https://test.datadex.itheum.io/mintdata](https://test.datadex.itheum.io/mintdata) and clicking the button below to pre-populate the minting from with **NFMe.ID Vault Data NFT** metadata.

As per previous action step, mint your **NFMe.ID Vault Data NFT** and confirm it's in your wallet.

<figure><img src="../../../.gitbook/assets/image (164).png" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 4:**</mark> Once the **NFMe.ID Vault Data NFT** is minted, browse to Wallet -> Bonding: [https://test.datadex.itheum.io/datanfts/wallet/bonding](https://test.datadex.itheum.io/datanfts/wallet/bonding). Review your combined liveliness, which will be based on your Data NFTs with bonds.

<mark style="background-color:blue;">**Task 2:**</mark> Take a screenshot similar to the example below that shows your new "Y**our Liveliness Rewards**" and "**Your Data NFT Creator Liveliness Bonds**"

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfhlrC_WFufpJUK4yfX2ugDiHvYnJps8rwFzBKS5XSWHGE26uZfkRqEk8B2Y0AtwkJkgiuh9ywwhgWl2bVSaX3oB9GgLcQ4qhUT5fl9hNoFgpHwPi0idxkadCPEiJQ7HC6u2FFKjEycNjvS6s8BhHgrQw7z?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 5:**</mark> Set your **NFMe.ID Vault Data NFT** as your Primary NFMe.ID (click on "Make this your Primary NFMe.ID" button).&#x20;

Top up your **NFMe.ID Vault Data NFT** with 100 ITHEUM.

<mark style="background-color:blue;">**Task 3:**</mark> Take a screenshot similar to the example below that shows your new "Y**our Liveliness Rewards**" "**Your NFMe.ID Vault Data NFT**", and "**Your Data NFT Creator Liveliness Bonds**"

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHaMtARsCb_1tYjxhkoiKKdBr58hpHVEOoh6W-Heng1U-D2jNxwOeNYBSCskHI5T_kJMB-aSOHLQmse_bvZI1n8IFNF-_zdmeETwaZhw2RPps_bb06RP1WvyUGzFY5RFWWWSxiThFmzmy82uMxtq_XkSg?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 6:**</mark> Come back in **2 DAYS** and review Liveliness and Rewards after a couple of days.

<mark style="background-color:blue;">**Task 4:**</mark>  Do all the below items (note that your will need a BEFORE vs AFTER screenshot, so you need two in total)

1. BEFORE SCREENSHOT: Take a screenshot similar to the example above that shows your "Y**our Liveliness Rewards**", "**Your NFMe.ID Vault Data NFT**", and "**Your Data NFT Creator Liveliness Bonds**" &#x20;
2. Report your UTC time from [https://www.timeanddate.com/worldclock/timezone/utc](https://www.timeanddate.com/worldclock/timezone/utc)&#x20;
3. Note down your $ITHEUM balance in the top right corner of the app, so we can verify that your $ITHEUM balance goes up when your claims your rewards
4. Click on "Claim rewards" button in "Y**our Liveliness Rewards**" box, and review the $ITHEUM balance and confirm your new balance is correct with the claimed rewards.
5. AFTER SCREENSHOT: Take a screenshot similar to the example above that shows your new "Y**our Liveliness Rewards**", "**Your NFMe.ID Vault Data NFT**", and "**Your Data NFT Creator Liveliness Bonds**" &#x20;

**Got Questions? Head over to our Discord :** [**itheum.io/discord** ](https://itheum.io/discord)



