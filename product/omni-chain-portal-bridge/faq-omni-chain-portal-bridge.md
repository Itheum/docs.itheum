# FAQ - Omni-Chain Portal Bridge

1. **What can I bridge with the current Omni-Chain Portal Bridge?**

Bridge Itheum Protocol token assets like $ITHEUM between MultiversX and Solana (other chains coming). Currently, you can only bridge the $ITHEUM token, but in the future, we are looking at the bridging of other token assets like Data NFTs.&#x20;

2. **What is an LP (Liquidity Pool) Bridge? and how is this different from other regular bridges in the ecosystem?**

Brides are very high-risk apps and there are many ways to design and operate a bridge between blockchains. Most of the existing bridges use a "Mint<>Burn" design, where the bridge has permission to mint tokens on one chain and burn the same amount of tokens on the other blockchain. This is an ideal design as the Max Supply of the tokens is always balanced and it makes it easier to use on-chain metrics to audit the bridge (by making sure the max supply is the same when summed across the chains). But the "Mint<>Burn" design is very risky, as it usefully involves you having to have a "bridge wallet" that has full mint/burn rights over the core token, and if the bridge wallet is breached, the attacker can mint or burn infinite tokens causing repairable damage to the project and community. "Mint<>Burn" design bridges are good if the bridge is decentralized as it is then harder to attack, but if it is not decentralized, then we recommend a more secure style bridge.

One such secure design style is called an LP (Liquidity Pool) bridge, where a fixed amount of tokens is manually minted when needed and then loaded into "one side" of the bridge (usually the new chain you want to support, i.e. Solana) and then users can bridge any amount of tokens, so long as it stays below the LP amount. With this style of bridge, if it were to get attacked, the attacker can only gain access to any remaining LP that's on the bridge and cannot mint or burn infinite tokens and the damage can be contained.

The Itheum Omni-Chain Portal Bridge is an LP (Liquidity Pool) Bridge

3. **How much LP did you mint on Solana and how can I keep track of the LP mints that happen on Solana?**

One "UX" issue with an LP (Liquidity Pool) Bridge is that you have to manually mint tokens on one chain and then make sure to manually balance the overall tokens on other chains to ensure that the MAX supply of the tokens are always balanced.\
\
When the bridge launched on 16 July 2024, we minted **20M tokens on Solana** and we will be burning 20M tokens on MultiversX (ETA for this to happen before the end of July 2024).

You can transparently follow the  Mint / Burn transactions on [usditheum-token-multi-chain-max-supply-rebalancing-transactions-audit.md](usditheum-token-multi-chain-max-supply-rebalancing-transactions-audit.md "mention")

4. **is the bridge centralized or decentralized and what are the plans in the future?**

The current bridge is an early version and is centralized and run by the core team. But we intend to move the underlying architecture to use open and decentralized bridging messaging infra like Accelar or Wormhole, unfortunately, as the MultiersX blockchain currently does not support any such bridge infra tools, we had no choice but to build our own. But once the infra is available, we intend to move to this as the backend and make any bridging technology itheum uses decentralized and therefore more secure for our users.

5. **How is the $ITHEUM Max Supply of 1 Billion always "balanced" between the chains?**

The supply is manually balanced and is transparently done with the transactions publicly displayed here for anyone to audit : [usditheum-token-multi-chain-max-supply-rebalancing-transactions-audit.md](usditheum-token-multi-chain-max-supply-rebalancing-transactions-audit.md "mention")

6. **What is an "Epoch"? and how long does it take to bridge tokens between MultiversX and Solana?**

The bridge uses the concept of Epochs to work, think of an Epoch as a "time interval" where certain actions happen, in a blockchain for example, you can collect a bunch of transactions in a fixed Epoch (time interval - e.g. 15 mins) and then process them at once to create a block.\


The Itheum portal bridge used a 3 min Epoch, where transactions are collected in an Epoch and then generally processed in 2-5 Epochs after that. So in total it can take around 3-6 EPOCHs, and each epoch is 3 mins, so your tokens should transfer between 9 - 18 minutes. Sometimes it will be faster and at times with high congestion, it can be slow.

7. **How can I check the live status of the bridge (is it up or down now)?**

You can check if the bridge is in a good operating state by monitoring the Itheum status page at [https://stats.uptimerobot.com/D8JBwIo983](https://stats.uptimerobot.com/D8JBwIo983)

Or you can monitor the specific bridge direction status here:

* MultiversX to Solana: [https://stats.uptimerobot.com/D8JBwIo983/797251801](https://stats.uptimerobot.com/D8JBwIo983/797251801)
* Solana to MultiversX: [https://stats.uptimerobot.com/D8JBwIo983/797251803](https://stats.uptimerobot.com/D8JBwIo983/797251803)

8. How can I get support if my transaction is on Hold or not showing?

There is a dedicated support process for bridge users, you can learn more here [portal-bridge-support.md](../../developers/tech-support-discord/portal-bridge-support.md "mention")
