# Data Marshal Network

As we test and ship devnet versions to mainnet, the release version notes appear below. You may see .patch versions appear and not rounded versions. i.e. V3.4.3 and not V3.4.0, this just means that there were patches on devnet that were added to a base version target before shipping to mainnet/production.

***

## V3.7.0 (Brontes)

**Main Features / Changes**

* Data NFT watermarking now supports Solana address as "creator"

**Bug Fixing / Other Updates**

* N/A

***

## V3.6.0 (Brontes)

**Main Features / Changes**

* Solana Support! Compresses Data NFT support has been added so the Marshal nodes can no broker data on the Solana chain.

**Bug Fixing / Other Updates**

* Improvement for how Sentry reports errors and other fixes

***



## V3.4.3 (Brontes)

**Main Features / Changes**

* Support for ipfs:// and ipns:// data stream URLs. Swap IPNS and IPFS base links hashes through a default gateway for fast live streaming of the data.
* Add a timeout for uptime checks so it resolves with better UX on frontends.
* When it sees the nestedIdxToStream param, it defaults to Nested Streams. This is helpful if a data stream is on IPFS or IPNS and can't set the response headers. But this is ONLY partial nested stream support as the primary manifest is fully viewable not protected with the nested stream rules. See next point for the "right" way to enable nested streams via a URL param:
* We also support full nested stream workflow by using a question string param that can be added instead of a header. This query string is dmf-nestedstream=1. [Read more](https://docs.itheum.io/product-docs/developers/software-development-kits-sdks/data-nft-sdk/guide-3-using-nested-streams-to-access-nested-data-assets-from-a-primary-data-stream#step-1-configure-data-stream-origin-backend-for-nested-streams)
* Support for Data NFT-PH is here! [See guide](https://docs.itheum.io/product-docs/developers/software-development-kits-sdks/data-marshal-network-sdk/guide-1-make-your-regular-nft-collection-to-be-data-nft-ph-compatible)

**Bug Fixing / Other Updates**

* MAJOR: Fixed header forwarding issue that broke MultiversX Native Auth protected data stream on mainnet/production.
* Add a timeout for uptime checks so it resolves with better UX on frontends.

***

## V3.3.0 (Brontes)

**Main Features / Changes**

* Deputy / Deputy Appointer Feature,&#x20;
* 10 origins allowed for NativeAuth token

**Bug Fixing / Other Updates**

* Nested Stream fix for forwardAllHeaders
* Sentry only in Prd and send all exceptions to sentry
