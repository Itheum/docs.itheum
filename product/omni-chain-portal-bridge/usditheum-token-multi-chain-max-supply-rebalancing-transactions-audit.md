# $ITHEUM Token Multi-Chain Max Supply Rebalancing Transactions Audit

## $ITHEUM Token Max Supply is Fixed to 1 Billion: How do we balance this across multiple blockchains?

{% hint style="warning" %}
Please note that this design has changed and is no longer relevant — please read section "Minting Max Supply on Solana and Moving Away From Burn <> Mint Design for Token Supply Balancing" below for more info.
{% endhint %}

The $ITHEUM token has a fixed supply of 1 Billion (1,000,000,000) and was initially minted on the MutiversX blockchain. This is the original token: [https://explorer.multiversx.com/tokens/ITHEUM-df6f26](https://explorer.multiversx.com/tokens/ITHEUM-df6f26)

As the $ITHEUM token is now a multi-chain token, which means it can exist on multiple blockchains, we need to ensure that the fixed max supply across ALL the blockchains for the tokens never exceeds 1 Billion. This balancing can be done manually or automatically based on how the token bridge technology works.&#x20;

At this stage, we only have a [MultiversX <> Solana bridge that uses an "LP Design"](../../legal/ecosystem-tools-terms/omni-chain-portal-bridge.md) and performs a manual token burning and minting to balance the fixed max supply to be 1 Billion across Multiversx and Solana. \
\
All mint and burn activity is transparently done and the audit log is maintained below for anyone in the community to monitor and audit as needed. Traspenrecy all the way!

## Who can burn? and where do the burn tokens come from?

* The only wallet that has the rights to burn tokens on MultiversX is this dedicated wallet: [https://explorer.multiversx.com/accounts/erd17exmcvh0wm2xx9ngas84vd3jyc4zgf6scg75tmncff6k3qnxux0qzw0mrf](https://explorer.multiversx.com/accounts/erd17exmcvh0wm2xx9ngas84vd3jyc4zgf6scg75tmncff6k3qnxux0qzw0mrf)
* When we burn tokens on MutliversX because we minted tokens on another chain (e.g. Solana), these tokens are burned from the **"Ecosystem" bucket,** as bridging is related to ecosystem growth.



## Multi-Chain Current Supply Balances

**Last Update: 2 Nov 2024**

| Blockchain | Current Supply    | Verify on Token Page                                                                                                                                               | Notes                                                                                                                                             |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| MultiversX | 960,000,000       | [https://explorer.multiversx.com/tokens/ITHEUM-df6f26](https://explorer.multiversx.com/tokens/ITHEUM-df6f26)                                                       | On MultiversX, the supply should show exactly as burning tokens are not allowed.                                                                  |
| Solana     | 40,000,000        | [https://explorer.solana.com/address/iTHSaXjdqFtcnLK4EFEs7mqYQbJb6B7GostqWbBQwaV](https://explorer.solana.com/address/iTHSaXjdqFtcnLK4EFEs7mqYQbJb6B7GostqWbBQwaV) | The current supply might show less than the target amount as on Solana anyone can burn tokens, but it should NEVER be more than the shown amount. |
| **TOTAL**  | **1,000,000,000** |                                                                                                                                                                    |                                                                                                                                                   |



## Mint and Burn Transactions - Audit

The following are the mint and burn transactions to balance the token supply to 1 Billion across Solana and MultiversX.

### Solana Mint Transactions:

| Date         | Action                                               | Solana Transactions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Total Minted on Solana | Notes                                                                                                                                                                                                 |
| ------------ | ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jul 16, 2024 | Minted initial supply (batch 1) of $ITHEUM on Solana | <p><a href="https://explorer.solana.com/tx/2bRUZ5HpnongTzgvHua6iXXzptifozWH6GFA1uTisWjr7rd4ER4vPXBb7BH62NNPaccyHqVhvyYpSy67dmTvtUpC">https://explorer.solana.com/tx/2bRUZ5HpnongTzgvHua6iXXzptifozWH6GFA1uTisWjr7rd4ER4vPXBb7BH62NNPaccyHqVhvyYpSy67dmTvtUpC</a><br><br><a href="https://explorer.solana.com/tx/eTzCkC8Xx2tS89BNGGuXwQyJn46RrVU8Enhu58xAg6ARszkevqY3or569PfoZZn21aRzQUW1QH2DW6zBTSCMpoD">https://explorer.solana.com/tx/eTzCkC8Xx2tS89BNGGuXwQyJn46RrVU8Enhu58xAg6ARszkevqY3or569PfoZZn21aRzQUW1QH2DW6zBTSCMpoD</a></p> | 20,000,000             | <p>The target supply was 20,000,000<br><br>But we did it in two batches to test the process. This is why 2 transactions are seen.</p>                                                                 |
| Nov 01, 2024 | Minted supply (batch 2) of $ITHEUM on Solana         | [https://explorer.solana.com/tx/2AYgEDYLpqLyUj2nkBorQFtyhhGmfJbKsYBh5F3UBmy6NzxmvRyUiJDay6828JhHNxPuGaLaAm3y16cewTpCHB3T](https://explorer.solana.com/tx/2AYgEDYLpqLyUj2nkBorQFtyhhGmfJbKsYBh5F3UBmy6NzxmvRyUiJDay6828JhHNxPuGaLaAm3y16cewTpCHB3T)                                                                                                                                                                                                                                                                                      | 20,000,000             | Mint these tokens to move more ITHEUM from MultiversX to Solana. Primarily to facilitate the lauch of NFMe ID Liveliness Staking on Solana and seed the staking rewards for people who mint NFMe IDs. |
|              |                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                        |                                                                                                                                                                                                       |

### MultiversX Burn Transactions:

| Date         | Action                               | MultiversX Transactions                                                                                                                                                                                                        | Total Burned on MultiversX  | Notes                                                                                                                                                                                                                              |
| ------------ | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jul 25, 2024 | Burn $ITHEUM on MultiversX (batch 1) | [https://explorer.multiversx.com/transactions/b31b7fe8bd23df8e1c382b4b943db655099328832f1dc24beb58382de96fd76a](https://explorer.multiversx.com/transactions/b31b7fe8bd23df8e1c382b4b943db655099328832f1dc24beb58382de96fd76a) | 20,000,000                  | <p>The burn happened 9 days after the mint on Solana as we had to test and create a secure process for future burns to happen transparently.<br><br>In the future, for mint/burn cycles, we will aim to do it on the same day.</p> |
| Nov 01, 2024 | Burn $ITHEUM on MultiversX (batch 2) | [https://explorer.multiversx.com/transactions/b99c32354170220fe68cf5ada779865eb9dcac950ace13c72fe435fb5ddd1129](https://explorer.multiversx.com/transactions/b99c32354170220fe68cf5ada779865eb9dcac950ace13c72fe435fb5ddd1129) | 20,000,000                  | As batch 2 of same amount was minted on Solana, we burned on the same amount of MVX on the same day.                                                                                                                               |
|              |                                      |                                                                                                                                                                                                                                |                             |                                                                                                                                                                                                                                    |



## Minting Max Supply on Solana and Moving Away From Burn <> Mint Design for Token Supply Balancing

{% hint style="warning" %}
Note that on 31 Jan 2025  — we moved away from the burn (MVX) <> mint (SOL) bridge design. Previously, as above, we would burn ITHEUM tokens in batches in MVX (i.e. -20M and -20M as above) and then mint the same amount on SOL (i.e. +20M and +20M as above) to keep the supply balanced between all chains to 1 Billion.\
\
But we have now minted the max supply on Solana as well and have locked it off in wallets to only be loaded into bridge liquidity as needed. (see point 3 below)\
\
**Why did we make this change?**\
To mint tokens on Solana on-demand, we had to keep the token"mintable" (on Solana, we have to keep the Mint Authority settings). This was the only we can mint tokens on demand, unfortunately, keeping the Mint Authority is largely frowned upon in Solana and is considered unacceptable. Most tools like DexScreener and RugCheck marked the ITHEUM token on Solana as "Highly Risky" as you can see screen shot below. This really impacted the confidence of our users on Solana and we had to fix this. This is the reason for this change which we will do transparently and also feel it's the best interests of our community as it increases project and token confidence.\
\
**Here are the details on the changes:**

1. 810,000,000 ITHEUM was newly minted on Solana on 31 Jan 2025. 40,000,000 ITHEUM was already minted previously. This makes the total supply on Solana 850,000,000 ITHEUM
2. 850,000,000 ITHEUM was minted instead of the max supply on 1 Billion ITHEUM as 150,000,000 ITHEUM was committed to be burned on MultiversX side as part of [phase-1-token-burn-program.md](../../protocol/token-burning/phase-1-token-burn-program.md "mention")
3. Excess tokens on Solana (i.e. supply that is NOT bridged from MVX to Solana via the [portal-traveler-test-the-itheum-omni-chain-portal-bridge.md](../../protocol/hackathons-and-dev-challenges/community-test-events/portal-traveler-test-the-itheum-omni-chain-portal-bridge.md "mention")) — are locked in 4 seperate wallets :
   1. DFzgZbGdKA2vxe679dV15oHPE2HCE9kdXiViJxfKo8Sm
   2. EfLr6Bb94uZ5xgqbtSiaarUfBVrprZvVjYWKJfwyydLm
   3. 3KuaEAxbGbJ1VXD1eS1N3jTbjfXQALGjTyAnJP9wsfjc
   4. BYvPrDMXqPTRbVdL8AiBcQZVtbcffK3URqQkHemNYhAq
4. Tokens from these wallets can be transparently monitored.&#x20;
5. Tokens from these wallets can only move to the Portal Bridge liquidity when needed (i.e. large amounts of ITHEUM tokens are being bridged from MVX to SOL)\
   \
   We are committed to transparency, shuld you have any questions — please reach our team on Discord: [https://itheum.io/discord](https://itheum.io/discord)
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Example of Token being Marked as Risky as it is mintable</p></figcaption></figure>



