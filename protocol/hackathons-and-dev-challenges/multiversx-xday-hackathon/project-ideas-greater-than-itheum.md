# Project Ideas > Itheum

Here are some ideas to get your "creative juices" flowing. Note that these are just ideas and not "instructions," so use these to get some inspiration for your original ideas!



## Dev Tooling and Infrastructure&#x20;

<details>

<summary>Build a Browser Plugin "Data Wallet"</summary>

Build a "Data Wallet" browser plugin using our SDK that lets users have the Data NFTs they own conveniently available as they browse the web. Allow interaction between the host site a user is on and the plugin, allowing a "host site" request and access for data from within Data NFTs if the user allows it.

</details>

<details>

<summary>Build a Mobile App "Data Wallet" (and stream local data into a Data NFT)</summary>

Build a simple "Data Wallet" mobile app using our SDK that lets users have the Data NFTs they own conveniently available as they need it. A multi-platform mobile app using a framework like React Native or Flutter will be perfect for a simple app to work across Android and iOS.&#x20;

Bonus points if you can also use our SDK to implement a "Mint This into a Data NFT," where the user can seamlessly connect to another app on the device (e.g., Health app on iOS or Google Fit app on Android), takes in a snapshot of the user's health and wellness data, uploads that to a Data Stream ([centralized](../../../pre-aithra/pre-aithra-integrators/data-streams-guides/amazon-web-services-aws/) or [decentralized](../../../pre-aithra/pre-aithra-integrators/data-streams-guides/akord-arweave-blockchain.md)) and then mints this into a Data NFT the user owns.&#x20;

</details>

<details>

<summary>Enable "Swap and buy" Data NFTs with EGLD or Any ESDT Token</summary>

Currently, you can only procure access to a Data NFT on the Data DEX by using $ITHEUM tokens. Build a custom "swap and buy" Data NFT Marketplace app or plugin where users can procure Data NFTs using EGLD or any other ESDT. You can use tools like Ashswap aggregator or other "real-time" swap options. Basically, a user with EGLD/ESDT can see and execute a "real-time" swap and procure option to obtain a Data NFT.

</details>

<details>

<summary>Build a Seamless Decentralized Storage Solution for Itheum on Arweave</summary>

One of the most requested features from Itheum users is a "seamless and secure" way to self host data and for generating a Data Stream that can be used in Data NFT minting. We offer manual solutions to generate Data Stream as per [these guides](../../../pre-aithra/pre-aithra-integrators/data-streams-guides/) but we want to improve the user experience by automating tools for this. \
\
The solution can enable the user to connect to their Arweave storage account, upload their files, and then seamlessly generate a "Data Stream" URL, which can be used to mint a Data NFT. You can explore tools like [Akord](https://akord.com/) (we also have a [manual guide for Akord](../../../pre-aithra/pre-aithra-integrators/data-streams-guides/akord-arweave-blockchain.md) that you can read). Bonus points for any integration with Akord's "Vaults" that store encrypted data.

</details>

<details>

<summary>Explorer Additional Decentralized Storage Solutions for Itheum</summary>

In our question to empower users with "true ownership" of their data and as in the above idea for Arweave support, Itheum wants to make as many Decentralized Storage options available to our users via seamless integration. Ultimately, all you need to mint Data NFTs are "Data Streams", and technically, these Data Streams can come from any storage location as long as it follows the Data Stream URL rules. \
\
Along with Arweave above, explore, recommend and builds some tools that can integrate with platforms like:

* IPFS
* FileCoin
* BNB GreenField
* DFINITY (Internet Computer)&#x20;
* Or... use tools like [4EverLand](https://www.4everland.org/) that supports multiple platforms.

</details>

<details>

<summary>Enable "Token Streams" Based Trade of Data NFTs</summary>

Build a custom "swap and buy" Data NFT Marketplace app or plugin that allows Data NFT owners to trade their Data NFTs with others and where all trade happens in "token streams." This kind of "token stream" marketplace will protect buyers if the Data Creator stops hosting the Data Stream and will boost the activity with the Data Marketplace. You can explore tools like [CoinDrip](https://coindrip.finance/) or build your own.

</details>

<details>

<summary>Innovative New Data Wallet Experiences</summary>

Innovate and design new Data Wallet experiences for the tokens on the Itheum ecosystem, enhancing user engagement and functionality.

</details>

***

## #BuildOnItheum Project Ideas

Along with the app specific ideas below, check out the dev tooling and infrastructure ideas above to also get inspiration.

<details>

<summary>Build a  "Intelligence Bounty" Web3 system for On-Chain Investigators</summary>

We need more Data Creators on the Itheum platform. Data Creators publish apps like [MultiversX Bubbles](https://explorer.itheum.io/multiversx-bubbles), [Infographics](https://explorer.itheum.io/multiversx-infographics), and an upcoming Music series. These Data Creators ideally want to know "what you want" so they can generate content "for you."

As an example, the Data Creator behind MultiversX Bubbles, who is an on-chain investigator, would be able to generate a custom Data NFT with on-chain investigation insights that is centred around a specific event, for example, the Hatom Project launch.

It would be amazing to have an [Intelligence Bounty system like Akhram](https://decrypt.co/149042/arkhams-dox-to-earn-platform-offers-bounty-on-415-million-ftx-mystery) built as a separate web3 project (using smart contracts) that allows the community to raise bounties and have other users stake against their to show support for a bounty idea. Itheum Data Creators can then fulfil these bounties and mint Data NFTs to try and claim the bounties.

You can also make this a general-purpose "data bounty" system for the community to request any original data and have others stake on it to support the idea. This will attract Data Creators who publish Data NFTs in order to claim the bounty.

</details>

<details>

<summary>Build a "Digital Bookshelf" for PDF eBooks</summary>

The Itheum platform seamlessly support PDF eBooks to be minted as Data NFTs. An example of such an eBook is the [MultiversX Infographics Data NFT](https://explorer.itheum.io/multiversx-infographics). \
\
Mint a [Nested Streams](../../../pre-aithra/pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/guide-3-using-nested-streams-to-access-nested-data-assets-from-a-primary-data-stream.md)-based DApp experience that can point to a "courseware or book series" and mint this as a single Data NFT. For example, you can have a catalog of PDFs related to a specific topic, available as a single Nested Stream-based Data NFT. This will be similar to the [Music Player Nested Stream Data NFT detailed in this guide](../../../pre-aithra/pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/guide-3-using-nested-streams-to-access-nested-data-assets-from-a-primary-data-stream.md), but this will be for eBooks.\
\
\> Check out this [demo video to get you started](https://www.youtube.com/watch?v=ieY3cr3dwCU)

</details>

<details>

<summary>Build a Ticketing App using Itheum Enterprise</summary>

[itheum-enterprise.md](../../../pre-aithra/pre-aithra-r-and-d/itheum-enterprise.md "mention") will be launches within the shortly. Use the [enterprise-sdk](../../../pre-aithra/pre-aithra-developers/software-development-kits-sdks/enterprise-sdk/ "mention") to build a ticketing app; allowing the issuance of a ticket as a Data NFT that includes the generation of a barcode for permissioned entry a stream of data and rewards linked to the Data NFT as a Data Stream.

</details>

<details>

<summary>Build a " Multiple Data NFT Exploration Canvas" App</summary>

Currently, a user can only open and view content of a simple Data NFT using some free apps on [Itheum Explorer](https://explorer.itheum.io/). Build an "explorer canvas" that lets you "merge" the content of multiple, similar Data NFTs and view them together.&#x20;

For example, a Data Creator we work with, xFondres will publish multiple ESDT-based analytics JSON datasets (the raw data he used to generate the [ESDT Bubble Data NFT is available here](https://explorer.itheum.io/multiversx-bubbles)). Build an app or "canvas" that lets you add and remove Data NFTs and collectively visualize them. Links to the test Data NFTs from xFondres will be published soon.

</details>

<details>

<summary>Provide Access a Data NFT's Data using Zero Knowledge Proofs</summary>

This is an advanced idea but has massive real-world disruption if you can achieve it.

Build a Personal Data Vault on Itheum Enterprise (launching soon), where users upload encrypted data into a "soulbound Data NFT" that cannot be sold. For example, you can store encrypted KYC details or personal details like date of birth, etc. If the user visits some DApp that has integrated Itheum, and the site requests a zero-knowledge proof on some data stored inside their Data Vault. For example, the site can ask, "are you over 18?", and a response is provided to the site based on the encrypted data in the Data Vault.

</details>



Do you have other ideas you want to add to this list? [Join and Discord and share your ideas](../../../pre-aithra/pre-aithra-developers/tech-support-discord/)
