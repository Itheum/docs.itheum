---
description: >-
  Data NFT-PH: "Extend" your own NFT collection into a "hybrid" Data NFT
  collection
---

# Data NFT-PH (Plug-In Hybrid)

### What is Data NFT-PH?

Just like how a Plug-In Hybrid EV Car allows you to switch between fuel and electric modes, the Data NFT-PH is for projects that want to launch their own fully controlled NFT collections independently via an NFT Launchpad, CandyMachine Smart Contract or via a regular mint but would like to provide a "plug-in" interface for their regular NFTs also to be used as "hybrid Data NFTs", whereby increasing the utility of their NFTs by tapping into the Itheum data brokerage ecosystem of tools and incentives.

### How does it work?&#x20;

#### Setting Up:

It's pretty simple! A regular NFT collection must include a few "custom metadata attribute fields" on their token's NFT Metadata file (which is stored in IPFS, Arweave etc). If these "custom metadata attribute fields" are present on an NFT's Metadata file, they can "plug into" the entire Itheum ecosystem of tools (i.e., Data DEX, Data NFT marketplace, Itheum Explorer, SDKs, etc.). These "custom metadata attribute fields" can be added during the genesis mint of each token, or if you are using a "dynamic NFT Metadata service", it can also be added at any time as needed. Converting an NFT to a Data NFT-PH does NOT impact any regular behavior of the NFT, and it is still under the control of the original project owner and can be used and traded anywhere regular NFTs are accepted.

#### Ongoing Operation:

A key "custom metadata attribute field" is the **Data Stream URL** that the Data Marshal network will "stream" out to verified NFT token holders, and this is how an NFT "becomes" a Data NFT when in the Data NFT-PH mode. Initially, there is no "fee" for using the Data NFT-PH via the Data Marshal network. Still, at a future date, there may be a "pay per use" subscription or similar fee model, where if a regular NFT is used as a Data NFT in any supported protocol tool, the project that minted the NFT collection with Data NFT-PH support will need to pay some fees. This "fee" is part of Itheum's protocol fee that gets funneled back into the Itheum ecosystem participants to ensure the protocol is self-sustaining in the long term. In the situation where the NFT project wants to "exit" the Data NFT-PH system or take a break from it, they can remove the "custom metadata attribute fields" on the tokens (if they are using a dynamic NFT metadata service) or stop paying the "pay per use" fee by "unsubscribing". The NFTs then gracefully continue to operate in the regular NFT mode.

### Use cases:

Existing NFT collections seek multiple ways to engage their community to hold the base NFT and are constantly battling to find new utilities for their NFTs to keep them relevant and in demand. You can think of Itheum's Data NFTs as dynamic "building blocks" and, therefore, can be used by anyone in the community to create new and exciting use cases, creating a dynamic and ever-evolving utility for the native NFT collection. Projects that use Data NFT-PH can also tap into the Itheum ecosystem and community, further expanding their project's reach and NFT utility.

**Let's understand this better with an example:**

Project X is a DeFi protocol that launches an NFT collection to incentivize holders with perks and benefits within their DeFi protocol. If you hold an NFT from this collection, you can visit the tools built by Project X and get access to gated content or features. Project X now wants to extend the utility of the NFT collection and launches a Data Stream service that links each NFT to a custom stream of data, e.g., the NFT holder's trade history or trade insights. Project X then adds the "custom metadata attribute fields" to the NFTs and makes each NFT a Data NFT-PH by inserting the Data Stream Service into the Data Stream URL custom metadata attribute field. By converting their NFT to a Data NFT-PH, each NFT can leverage all of Itheum's ecosystem tools and incentives and tap into a whole new realm of utility. The specific benefits are described in the next section:

### Benefits of using the Data NFT-PH standard:

* The Data NFT-PHs can also be used and traded on the [Data DEX / Data NFT Marketplace](https://datadex.itheum.io/datanfts/marketplace/market).
* Developers in the ecosystem can build Data Widgets on [Itheum Explorer](https://explorer.itheum.io/) to visualize the data on each NFT.&#x20;
* 3rd party projects can use the Itheum [software-development-kits-sdks](../../pre-aithra-developers/software-development-kits-sdks/ "mention") to use the Data NFT as "dynamic building blocks" to build new dApps and experiences that combine multiple Data NFTs. Imagine 3rd party developers using your NFTs as "data" building blocks in their own apps!
* The Data NFTs can be used in Data Coalition DAOs and future staking programs that Itheum will launch to incentivize Data NFT usage.
* The Data NFTs become part of the challenges run by [itheum-xpand-dao](../../../protocol/governance/itheum-xpand-dao/ "mention") where Itheum runs accelerators to incentivize 3rd party developers to use ecosystem Data NFTs as "building blocks". Imagine regular innovation where 3rd party developers are constantly looking to build new and exciting utility-driven experiences using your Data NFTs.
* The long-term plan is to make all Data NFTs omni-chain. However, this is still in the early stages of design; this will involve allowing Data NFTs in MultiversX to "shadow" Data NFTs on other chains like Ethereum and Solana. This is for NFT collections to reach as large an audience as possible. As Data NFTs utilize the [data-marshal-network.md](../../data-marshal-network.md "mention") network as a "middleware," such omni-chain Data NFT collections are possible, and we will aim to extend this support for Data NFT-PHs.
* Benefit from all future tooling and product innovations from Itheum.

As you can see, by "extending" your NFT collection into a Data NFT-PH collection, you can significantly increase the utility of your base NFT collection and piggyback into the Itheum ecosystem of continuous dynamic utility that expands across multiple domains and eventually other chains.

### Ready to use Data NFT-PH?

It's straightforward to do this; your first step is to read this [guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible.md](../../pre-aithra-developers/software-development-kits-sdks/data-marshal-network-sdk/guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible.md "mention")and reach out to our team on [tech-support-discord](../../pre-aithra-developers/tech-support-discord/ "mention"), where we can help.
