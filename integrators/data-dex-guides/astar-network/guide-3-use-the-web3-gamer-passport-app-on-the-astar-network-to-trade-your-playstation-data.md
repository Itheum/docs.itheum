---
description: >-
  The "Web3 Gamer Passport" app has been integrated into a demo EVM version of
  the Data DEX on the Astar Network Blockchain. This guide will walk you through
  the workflow to trade Sony Playstation gamer
---

# Guide 3: Use the “Web3 Gamer Passport” App on the Astar Network to trade your PlayStation Data

Let’s get familiar with using our Data NFTs wallet, minting Data NFTs, and listing them onto the peer-to-peer Data NFT Marketplace. Let’s begin.

&#x20;**Prerequisites:**

* You must complete [Guide 1](guide-1-get-started-with-the-data-dex-on-astar-network/) before continuing with this Guide 3. It will also help if you complete [Guide 2](guide-2-procure-data-nfts-from-the-peer-to-peer-data-nft-marketplace-on-astar-network.md) to understand the Data NFT Marketplace features.

Let's get started...

***



**Step 1)** Swap to your “Data Seller” account on MetaMask. Following the previous guides, your wallet will have SBY (Astar Network Shibuya tokens) and ITHEUM Testnet tokens.

\
**Step 2)** In the “App Marketplace” section of the portal, click on “Join Now” on the “Sony Playstation Web3 Gamer Passport” tile.

<figure><img src="https://lh5.googleusercontent.com/1eqCbhWqbw-2Ad-dx-1KVDSvifdbuY2zTPo08ffCfscIPZxgioZliddn1_TILCQJXtqgSBT6pVbgwMfDOj-DLiESni2qGYPHrmMcpB5qPeVxQeZMp9Wf4hEWl-BGE8oT9DWlXMaRThcab7Q15n0dwXE" alt=""><figcaption></figcaption></figure>



**Step 3)** Follow the workflow and make your selection as needed.

<figure><img src="https://lh5.googleusercontent.com/KyV56_hv72-Du1wUBTfJezWmRkyhAM2nhByeu2NE0m6yTEgeJLAYcIP5HB4G0Lc867QBE3pdAh_9l4Q2cD-9ckDgFJW96obptUfm0D0BI0lUpx7Mp3UfMrlHslw_dUoxjXRJpinU6otDRX9yxXpdHkU" alt="" width="375"><figcaption></figcaption></figure>



**Step 4)** In Step 1, you can link your real Playstation Account via your NPSSO and PSN Username.

<figure><img src="https://lh6.googleusercontent.com/vFrvA3YIiM1wj_Na_Lc0jYbrIKR6P4ejzQl5XabqKB3SkqlAdOM9OqS19OrUQLPtM7VVJXDr1cqYnbcdXvumFPdoE6DTow-uiBMtLe0MyLhG-AthPrraycLm_EE-9qD-L-63tDYDDGfv95VDmcU7-lA" alt="" width="375"><figcaption></figcaption></figure>

**How Can I Get My NPSSO?**\
An NPSSO is like a token that can be exchanged for other session tokens. Here is how you can obtain it.\
\
In your web browser, visit [the PlayStation homepage](https://www.playstation.com/), click the "Sign In" button, and log in with a PSN account.

#### Retrieve your NPSSO token[​](https://psn-api.achievements.app/authentication/authenticating-manually#retrieve-your-npsso-token)

In the same browser that you used to log in (due to a persistent cookie), visit [this page](https://ca.account.sony.com/api/v1/ssocookie). You will see a JSON response that looks something like:

`{ "npsso": "<64 character token>" }`

\
Copy this as it’s your NPSSO. If you see an error response, try using a different browser.



**Before you proceed, It’s essential to understand a few critical details and decide how to proceed.**

1. The Web3 Gamer Passport uses an unofficial Sony Playstation API, as no Official Sony Playstation API is available yet. We are seeking to work with Sony to obtain this.
2. The unofficial Sony Playstation API utilizes an NPSSO to generate a session to have time-limited access to your data.&#x20;
3. The Web3 Gamer Passport app DOES NOT store your NPSSO or PSN username, it utilizes this to obtain a long-lived session token, and this is stored in the location your pick in the Data Sovereignty Preferences section of the workflow (e.g., North America)
4. The session token is used to obtain a snapshot of your PlayStation Network (PSN) gaming data, and the Web3 Gamer Passport app also de-identifies the data by removing any details about your identity and account. The final de-identified data stream will look similar to this : [https://api.itheumcloud-stg.com/hosteddataassets/playstation\_gamer\_1\_data\_passport.json](https://api.itheumcloud-stg.com/hosteddataassets/playstation\_gamer\_1\_data\_passport.json)

\
**I am comfortable with this:**

If you are comfortable with the above details, enter your NPSSO and PSN Username and proceed with the workflow form to trade your actual PlayStation data.

\
**I am NOT comfortable with this:**

You can still proceed with this workflow with a dummy PlayStation Network gamer account. Click on this button to proceed.

<figure><img src="https://lh6.googleusercontent.com/bgAQCaKKCE4Laar2XB1gSBaM27iCAC17xzVmN7op7MdP93vuux7qhPN0ukzlmHzN43MlmrOg50AYijvbCXCOD6dIfZwFrUFUuSTx6-tlcwbLKZNKH3g37hak0aEz8AS2NQe1QTf8WcR81fnKJRn9aUY" alt="" width="375"><figcaption></figcaption></figure>



**Step 5)** Once you reach the final step, you will be provided with the option to proceed to "Mint my Data NFT". Clicking on this will take you to the Data NFT Minting form.

<figure><img src="https://lh4.googleusercontent.com/cWLYWkDHJx3Lywk9-NqayRgHlRTCHNv7yG_Br2JMsXQOSOXZduCbcMr5i_W8fzabi-TyLIfSAczImyYZ4q9Lgb5xOY8F0q31x2kC7sL4tTsof9DLJv_ZYhrqNgCNEi8Wy6IyD4-fznxO3XaX7NfZn9k" alt="" width="375"><figcaption></figcaption></figure>



**Step 6)** The Data NFT Minting form should be pre-filled with the metadata and information needed to mint your Data NFT.&#x20;

You can change the details as needed.

<figure><img src="https://lh4.googleusercontent.com/A5fHfYP6m_zqSybkkRSuy80mc-pE529J98CZQTzhTDWz3ukUUvcilwtmOdOMqsDArDdbbZweEcS4XSKCau352ZbOJ2502iEbjVuYFWP2lkWwC5jdUeZ_UPgFL2ePQBsLAofar23Gvovc39XD9LVnqQs" alt=""><figcaption></figcaption></figure>



**Step 7)** Please note that enabling "Make tradable" will immediately place your Data NFT on the public Data NFT Marketplace for open trade. You can turn this off if you want to use your Data NFT in your Crypto Wallet as a form of "Data Vault" that you can use to give consented access in 3rd party dDapps that use the Itheum SDK to request access to your Data NFT (that's in a Data Vault configuration as it's not tradeable)

After you have read and agreed to the Terms of Use, click "Mint your Data NFT" to begin the Data NFT minting.

<figure><img src="https://lh6.googleusercontent.com/6pw59lnb-9VNDfnp8NuGviOduOJ-tBmkmTP3wyPoM3GQmEjKBIwZAzWcSoWQ79_6KcEgCPpxi08Ns037ih_eRC3Hgo7F0ii_GuY1oRyAi00rlUQp6zyQuB1DmGU7prb0EnRk5Y3sSgvd1OtBcc_Rzao" alt=""><figcaption></figcaption></figure>



**Step 8)** sign the transaction to finalize the Data NFT minting on the Blockchain when prompted.

<figure><img src="https://lh6.googleusercontent.com/y0v2ejrW_tbJkFnOoRhrhXTGReTqzfxPbWenTFe5ReBEMKmZOudA-OA6z2YGDY87ZvxuIFiXzp8pD6WWsF-3uTpNx__3XNvpzGy3AF2elx9pbRWhY8YAIyziKvcG4GACrVbMr7tiwf4sHx3zfTEC-4g" alt=""><figcaption><p>The image you see is a unique generative image that is based on the signature of the data you are minting as a Data NFT.</p></figcaption></figure>





**Step 9)** Progress updates can be seen on every step of the minting process and once it’s complete, you will be presented with an option to “Visit your Data NFT Wallet to see it!” so you can see your newly minted Data NFT.

<figure><img src="https://lh4.googleusercontent.com/Za9v6YcuPMSmsDB2L4WNtcXHM9RivAowuX2GB8rww1R71ClFA4Ue8Od9LqDRn9HRoiAOP6nlbDOD6e-kxYyw4qIdljY561mRiaWbuYTnGFuPRfw1zbDm2cdqnmj-mnlj20xyhu3hLzmg1dcX7inWv7Y" alt="" width="375"><figcaption></figcaption></figure>

And that’s it! You are now the proud owner of an absolutely unique Data NFT that sits in front of your PlayStation Gaming data. A web3 licence for the consented use of your data.

<figure><img src="https://lh6.googleusercontent.com/0WLPd3KIADhLW9yC9U_lhCy2n4yfSJu5TLs2TsPrOEjf_6VDou__vco_HC-pUylJt-j6uBTQ7lxwH4cIFzlchvEiKfg_tBoTiTtOyy5jpQrDqBZdF-2Qt6O4nEx2GXxrEXj585qWxAkNs4gN2HykmnU" alt=""><figcaption></figcaption></figure>
