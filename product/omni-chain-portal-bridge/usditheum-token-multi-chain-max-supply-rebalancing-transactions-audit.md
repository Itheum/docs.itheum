# $ITHEUM Token Multi-Chain Max Supply Rebalancing Transactions Audit

## $ITHEUM Token Max Supply is Fixed to 1 Billion: How do we balance this across multiple blockchains?

The $ITHEUM token has a fixed supply of 1 Billion (1,000,000,000) and was initially minted on the MutiversX blockchain. This is the original token: [https://explorer.multiversx.com/tokens/ITHEUM-df6f26](https://explorer.multiversx.com/tokens/ITHEUM-df6f26)

As the $ITHEUM token is now a multi-chain token, which means it can exist on multiple blockchains, we need to ensure that the fixed max supply across ALL the blockchains for the tokens never exceeds 1 Billion. This balancing can be done manually or automatically based on how the token bridge technology works.&#x20;

At this stage, we only have a [MultiversX <> Solana bridge that uses an "LP Design"](../../legal/ecosystem-tools-terms/omni-chain-portal-bridge.md) and performs a manual token burning and minting to balance the fixed max supply to be 1 Billion across Multiversx and Solana. \
\
All mint and burn activity is transparently done and the audit log is maintained below for anyone in the community to monitor and audit as needed. Traspenrecy all the way!

## Who can burn? and where do the burn tokens come from?

* The only wallet that has the rights to burn tokens on MultiversX is this dedicated wallet: [https://explorer.multiversx.com/accounts/erd17exmcvh0wm2xx9ngas84vd3jyc4zgf6scg75tmncff6k3qnxux0qzw0mrf](https://explorer.multiversx.com/accounts/erd17exmcvh0wm2xx9ngas84vd3jyc4zgf6scg75tmncff6k3qnxux0qzw0mrf)
* When we burn tokens on MutliversX because we minted tokens on another chain (e.g. Solana), these tokens are burned from the **"Ecosystem" bucket,** as bridging is related to ecosystem growth.



## Multi-Chain Current Supply Balances

**Last Update: 25 July 2024**

| Blockchain | Current Supply    | Verify on Token Page                                                                                                                                               | Notes                                                                                                                                             |
| ---------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| MultiversX | 980,000,000       | [https://explorer.multiversx.com/tokens/ITHEUM-df6f26](https://explorer.multiversx.com/tokens/ITHEUM-df6f26)                                                       | On MultiversX, the supply should show exactly as burning tokens are not allowed.                                                                  |
| Solana     | 20,000,000        | [https://explorer.solana.com/address/iTHSaXjdqFtcnLK4EFEs7mqYQbJb6B7GostqWbBQwaV](https://explorer.solana.com/address/iTHSaXjdqFtcnLK4EFEs7mqYQbJb6B7GostqWbBQwaV) | The current supply might show less than the target amount as on Solana anyone can burn tokens, but it should NEVER be more than the shown amount. |
| **TOTAL**  | **1,000,000,000** |                                                                                                                                                                    |                                                                                                                                                   |



## Mint and Burn Transactions - Audit

The following are the mint and burn transactions to balance the token supply to 1 Billion across Solana and MultiversX.

### Solana Mint Transactions:

| Date         | Action                   | Solana Transactions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Total Minted on Solana | Notes                                                                                                                                 |
| ------------ | ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Jul 16, 2024 | Minted $ITHEUM on Solana | <p><a href="https://explorer.solana.com/tx/2bRUZ5HpnongTzgvHua6iXXzptifozWH6GFA1uTisWjr7rd4ER4vPXBb7BH62NNPaccyHqVhvyYpSy67dmTvtUpC">https://explorer.solana.com/tx/2bRUZ5HpnongTzgvHua6iXXzptifozWH6GFA1uTisWjr7rd4ER4vPXBb7BH62NNPaccyHqVhvyYpSy67dmTvtUpC</a><br><br><a href="https://explorer.solana.com/tx/eTzCkC8Xx2tS89BNGGuXwQyJn46RrVU8Enhu58xAg6ARszkevqY3or569PfoZZn21aRzQUW1QH2DW6zBTSCMpoD">https://explorer.solana.com/tx/eTzCkC8Xx2tS89BNGGuXwQyJn46RrVU8Enhu58xAg6ARszkevqY3or569PfoZZn21aRzQUW1QH2DW6zBTSCMpoD</a></p> | 20,000,000             | <p>The target supply was 20,000,000<br><br>But we did it in two batches to test the process. This is why 2 transactions are seen.</p> |
|              |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                        |                                                                                                                                       |
|              |                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |                        |                                                                                                                                       |

### MultiversX Burn Transactions:

| Date         | Action                     | MultiversX Transactions                                                                                                                                                                                                        | Total Burned on MultiversX  | Notes                                                                                                                                                                                                                              |
| ------------ | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Jul 25, 2024 | Burn $ITHEUM on MultiversX | [https://explorer.multiversx.com/transactions/b31b7fe8bd23df8e1c382b4b943db655099328832f1dc24beb58382de96fd76a](https://explorer.multiversx.com/transactions/b31b7fe8bd23df8e1c382b4b943db655099328832f1dc24beb58382de96fd76a) | 20,000,000                  | <p>The burn happened 9 days after the mint on Solana as we had to test and create a secure process for future burns to happen transparently.<br><br>In the future, for mint/burn cycles, we will aim to do it on the same day.</p> |
|              |                            |                                                                                                                                                                                                                                |                             |                                                                                                                                                                                                                                    |
|              |                            |                                                                                                                                                                                                                                |                             |                                                                                                                                                                                                                                    |



