# Data NFT SDK

## V2.5.0

**Main Features / Changes**

* getOwners() method for Data NFT and Data SFTs. Call to get all current owners of this the collection in question.
* New owner attribute for DataNft class, if the request has it, it populates it

**Bug Fixing / Other Updates**

* Updated tests
* Use BigNumber defaults for specific numbers to improve stability of code
* Updated MVX libs that seemed to have an Axios critical issue

***

## V2.4.0

**Main Features / Changes**

* "Data NFT Minter" (Data NFT-LEASE used for Itheum Enterprise) ABI updated with SC updates on devnet
* Show taxToken information on requirements endpoints
* Gas limit updates to endpoints that were breaking due to low gas
* Seperate and show SftMinterRequirements and NftMinterRequirements

**Bug Fixing**

* Fixed tests

***

## V2.1.0

**Main Features / Changes**

* \[BREAKING CHANGE] sdk-core upgraded to 12.9.0. This brings in a breaking change to Transaction imports. Update you sdk-core to resolve it.

**Bug Fixing**

* TBC

***

## V2.0.0

**Main Features / Changes**

* Alpha version of Itheum Enterprise support and was used for early testing internally and by a partner

**Bug Fixing**

* General cleanup of code and docs

***

## V1.2.0

**Main Features / Changes**

* Nested Stream support is here!
* Automated documentaion generation actions via JSDoc

**Bug Fixing**

* General cleanup of code and method signatures and docs

***

## V1.1.0

**Main Features / Changes**

* Full Native Auth Support
* Multi Token for createFromAPI and createManyFromApi

**Bug Fixing**

* General cleanup of code and method signatures and docs

***

## V1.0.0

This release is still in beta mode as it has breaking changes and alos introduces Native Auth.

**Main Features / Changes**

* MultiversX Native Auth support for view data via a seperate viewDataViaMVXNativeAuth method. This flexible ethods works with the latest data marshal that support opening a file via Native Auth and also passing on Native Auth tokens to the Origin Data Stream server (if you want to implement "private" data stream)
* Better validation: ensureNetworkConfigSet hook on methods to ensure this is done before any actions happen and break client experience
* \[BREAKING CHANGE] : Better validation: viewData does deep validation on input params to better guide the user on how to carry out this method.&#x20;
* \[BREAKING CHANGE] : Better validation: primary mint does deep validation on input params to better guide the user on how to carry out this method. Also validates the uptime of URLs and enforces the correct HTTP status code requirements and security protocol (e.g. https)
* \[BREAKING CHANGE] : createManyFromApi updated to allow for multiple data NFT collections. e.g. you can send a nonce array AND an optional custom collection string to locate these nonces. This is to make early support for "Itheum enterprise" launching soon
* All README and method docs updated

**Bug Fixing**

* General code improvements, unit test improvements etc

***

## V1.1.0

**Main Features / Changes**

* In Mint, imgUrl can also be a centralized location (non-IPFS) and it now support "bring your own" (you no longer have to use the Itheum provided generative image service)
* In Mint, if you "bring your own" imgUrl you also need to bring your own Traits file that meets the protocol standard
* viewData support for fwdHeaderKeys, fwdAllHeaders and fwdHeaderMapLookup - which can be used implement MultiversX Blockchain NativeAuth protection in the origin Data Stream server (i.e. auth protected Data Streams)
* SDK works with explicit config over implicit env variables (remove ENV dependency)

**Bug Fixing**

* Improve READE and fix issues with code examples
