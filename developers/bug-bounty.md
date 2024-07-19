# 🐞 Bug Bounty

Itheum is a fully open source, omni-chain protocol that's powered by multiple open source smart contracts and dapps.

A bug bounty program is being put into place to enable social developers and engineers to responsibly disclose security issues in exchange for a reward.

## Rewards by Threat Level

Rewards are distributed according to the impact of the vulnerability based on the [Immunefi Vulnerability Severity Classification System V2.3.](https://immunefi.com/immunefi-vulnerability-severity-classification-system-v2-3/) This is a simplified 5-level scale, with separate scales for websites/apps, smart contracts, and blockchains/DLTs, focusing on the impact of the vulnerability reported.

All bug reports must include a Proof of Concept (PoC) demonstrating how the vulnerability can be exploited to impact an asset-in-scope to be eligible for a reward. Critical and High severity bug reports should also include a suggestion for a fix. Explanations and statements are not accepted as PoC and code is required.

Payouts are handled by the **Itheum** team directly and are denominated in USD. However, payouts are done in **ITHEUM**.

## Rewards

The reward amounts are being finalized, but reach out to us **bugbounty@itheum.io** in the meantime for reward amount specifics.&#x20;

## Bounty Submission

Email us on **bugbounty@itheum.io**

## Assets in Scope

### MultiversX

<table><thead><tr><th>Target</th><th>Type</th><th data-hidden></th></tr></thead><tbody><tr><td><a href="https://github.com/Itheum/core-mx-bridge-sc">https://github.com/Itheum/core-mx-bridge-sc</a></td><td>MultiverX Bridge Deposit Smart Contract</td><td></td></tr><tr><td><a href="https://github.com/Itheum/core-mx-life-bonding-sc">https://github.com/Itheum/core-mx-life-bonding-sc</a></td><td>Token bonding for Liveliness to mint Data NFTs</td><td></td></tr><tr><td><a href="https://github.com/Itheum/itheumcore-elrond-data-nft-marketplace">https://github.com/Itheum/itheumcore-elrond-data-nft-marketplace</a></td><td>Data NFT marketplace (Data Market)</td><td></td></tr><tr><td><a href="https://github.com/Itheum/core-mx-data-nft-minter-nft-sc">https://github.com/Itheum/core-mx-data-nft-minter-nft-sc</a></td><td> Data NFT Minting Smart Contract</td><td></td></tr></tbody></table>

### Solana

<table><thead><tr><th>Target</th><th>Type</th><th data-hidden></th></tr></thead><tbody><tr><td><a href="https://github.com/Itheum/core-sol-bridge-sc">https://github.com/Itheum/core-sol-bridge-sc</a></td><td>Solana Bridge Deposit Program</td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

## Out of Scope & Rules

**The following vulnerabilities are excluded from the rewards for this bug bounty program:**

* Attacks that the reporter has already exploited themselves, leading to damage
* Attacks requiring access to leaked keys/credentials
* Attacks requiring access to privileged addresses

**Smart Contracts and Blockchain**

* Basic economic governance attacks (e.g. 51% attack)
* Lack of liquidity
* Best practice critiques
* Sybil attacks
* Centralization risks

**The following activities are prohibited by this bug bounty program:**

* Any testing with mainnet or public devnet contracts; all testing should be done on private testnets
* Attempting phishing or other social engineering attacks against our employees and/or customers
* Any testing with third party systems and applications (e.g. browser extensions) as well as websites (e.g. SSO providers, advertising networks)
* Any denial of service attacks
* Automated testing of services that generates significant amounts of traffic
* Public disclosure of an unpatched vulnerability in an embargoed bounty
