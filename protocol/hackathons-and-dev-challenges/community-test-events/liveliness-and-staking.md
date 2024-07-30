# Liveliness and Staking

## Introduction

Be part of the first cohort of users who test the Itheum Protocol Staking Program! This test event aims to stress test Itheum's new staking mechanism that allows gaining an APR for bonding ITHEUM tokens to Data NFTs.&#x20;



### Scope:

* The test event will focus on the testing of the staking mechanism of ITHEUM tokens in a "devnet" environment (i.e., no real value/mainnet tokens used).

### Test Dates:

* Start Data: 31 July (Friday) 2024
* End Date:  5 July (Tuesday) 2024

#### Bonus Rewards for Reporting Bugs and product exploration:

* "Backend" Bugs: Any bugs reported that are related to the "backend" (Smart contracts)&#x20;
* "Frontend" Bugs: These are bugs that are on the UI.

Any major bug discovered(related to APR or rewards calculations, security issues) will be rewarded with Bonus ITHEUM.

{% hint style="info" %}
**Submit your bug reports using this** [**feedback form**](https://forms.gle/utFkSfQyHbfjWdWv9)
{% endhint %}

### Test Scope:

#### Setup:

<mark style="background-color:green;">**Step 1:**</mark> Setup a MultiversX Wallet. Only [DeFi Wallet ](../../../integrators/supported-wallets/multiversx-defi-wallet.md)is supported for this test event. Put your wallet in "DEVNET" mode if required (but this should happen automatically when you use the Portal as it's setup in DEVNET mode only).

<mark style="background-color:green;">**Step 2:**</mark> Get some dEGLD (DEVNET EGLD), which is required for gas payment on MultiversX. Go here, [https://devnet-wallet.multiversx.com](https://devnet-wallet.multiversx.com/), login with your wallet from Step 1, and use the "Faucet" to get dEGLD. Alternately, you can use [https://r3d4.fr/faucet](https://r3d4.fr/faucet) to get dEGLD (Note! this is a 3rd party site so proceed with caution)

<mark style="background-color:green;">**Step 3:**</mark> Get DEVNET ITHEUM tokens, Go here: [https://test.datadex.itheum.io/](https://test.datadex.itheum.io/), login with your wallet from Step 1, Click on "Dash" on the top menu, and click on the "Send me ITHEUM" button to get 1,000 ITHEUM tokens.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

#### Actions:

{% hint style="info" %}
1. The following actions can be repeated.
2. The below assumes you begin the test with 1,000 $ITHEUM tokens on MultiversX DEVNET.
3. Before you begin the next actions, note down all your balances on both blockchains and at the end of all actions, confirm the balances are correct and as expected.
{% endhint %}

<mark style="background-color:orange;">**Action 1:**</mark> Browse to [https://test.datadex.itheum.io/mintdata](https://test.datadex.itheum.io/mintdata) and mint a Data NFT. You can obtain data stream URLs from [https://github.com/Itheum/data-assets](https://github.com/Itheum/data-assets).

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd9Je8hXvCFFnUSfU9GgLFfoe1VpigKkKEH0FdqpnUWyq8snX3xcFN7z4CObDrofq1tjkF4KQsAV7d9BwH1CDZhVZ-eBi0SFiu5X7MJQQrHvGxhdWtbS7kJ8hqsjwLhqOH8x3QUjv8EJnVCqY-10lSxNHY?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 2:**</mark> Once the Data NFT is minted, browse to Wallet -> Bonding: [https://test.datadex.itheum.io/datanfts/wallet/bonding](https://test.datadex.itheum.io/datanfts/wallet/bonding). Review your combined liveliness.

**Task 1:** Take a screenshot similar to the example below.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXc94VGjuCa8eliMGu3YKY1IB98eK0Or6HNaJZhkNFf_56ajgVkyMVPGsohrvjMDobPXTrE6ybSYUMMq1aD_dW8Iabxn5yPIrH9y_M62LIBM309c2p825Zzl2beHa65i4IFvX27EisZT7xqlwCqboGVgx09B?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 3:**</mark> Create an NFMe.ID. Browse to [https://test.datadex.itheum.io/mintdata](https://test.datadex.itheum.io/mintdata) and create a NFMe.ID VaultData NFT.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdpCdz4fwHx63iOwo3IXgrvgisUjW0IDvF4vdn_Qz4sQMbl6c7RjJjQjPmHjV0QEDHWBOZSyQXDM9VRDZote8xMBdzELGOmZIE11uFFnHUtKxqmCTseBAkcoxybrMpzidUctlN7b2NMe7qpaznCUBvmK3g?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 4:**</mark> Once the Data NFT is minted, browse to Wallet -> Bonding: [https://test.datadex.itheum.io/datanfts/wallet/bonding](https://test.datadex.itheum.io/datanfts/wallet/bonding). Review your combined liveliness, which will be based on your Data NFTs with bonds.

**Task 2:** Take a second screenshot, similar to the example below.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfhlrC_WFufpJUK4yfX2ugDiHvYnJps8rwFzBKS5XSWHGE26uZfkRqEk8B2Y0AtwkJkgiuh9ywwhgWl2bVSaX3oB9GgLcQ4qhUT5fl9hNoFgpHwPi0idxkadCPEiJQ7HC6u2FFKjEycNjvS6s8BhHgrQw7z?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 5:**</mark> Set your NFMe.ID vault as your Primary NFMe.ID. Top up your NFMe.ID vault with 100 ITHEUM.

**Task 3:** Take a third screenshot, similar to the example below after the top-up.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHaMtARsCb_1tYjxhkoiKKdBr58hpHVEOoh6W-Heng1U-D2jNxwOeNYBSCskHI5T_kJMB-aSOHLQmse_bvZI1n8IFNF-_zdmeETwaZhw2RPps_bb06RP1WvyUGzFY5RFWWWSxiThFmzmy82uMxtq_XkSg?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

<mark style="background-color:orange;">**Action 6:**</mark> Reveiw Livelines, and Rewards after a couple of days.

**Task 4:** Come back in 2 days, and perform the below

1. Take a screenshot of the balance, and report your UTC time from [https://www.timeanddate.com/worldclock/timezone/utc](https://www.timeanddate.com/worldclock/timezone/utc)&#x20;
2. Note down your ITHEUM balance in the top right corner.&#x20;
3. Claim your rewards and review the balance.





