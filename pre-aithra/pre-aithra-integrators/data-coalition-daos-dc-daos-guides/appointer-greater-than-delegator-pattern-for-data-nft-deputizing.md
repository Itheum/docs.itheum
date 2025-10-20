# Appointer > Delegator Pattern for Data NFT "Deputizing"

This pattern is core to how [data-coalition-daos-dc-daos.md](../../pre-aithra-r-and-d/data-coalition-daos-dc-daos.md "mention")work, but fundamentally this pattern can be used by any Smart Contract to enable it to "manage" Data NFTs on behalf of someone else who owns the Data NFTs, whilst allowing an external (approved) entity to open the Data NFTs to view the Data Stream.

[data-nft](../../data-nft/ "mention")s are minted by multiple entities; individuals, enterprises or 3rd party app developers using the [data-nft-sdk](../../pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/ "mention"). Ultimately, all these Data NFTs end up in "end-user wallets" (externally owned wallets). These Data NFTs can then be listed on NFT marketplaces and other NFT platforms by transferring your Data NFTs to these 3rd party Smart Contracts to give them "temporary ownership". However, given the specific method the Data Marshal Network uses to authenticate ownership of a Data NFT expects the "true" owner to make the "open this Data NFT" request, it's not possible for a Smart Contract with "temporary ownership" to open a Data NFT. It's also NOT useful for a Smart Contract to open a Data NFT as it cannot do anything with the data in its execution environment.&#x20;

{% hint style="success" %}
What would be useful is if the Smart Contract could specify a 3rd Party "end-user wallet" (externally owned wallet) to be able to open the Data NFT and do something useful with the Data. In this aspect, the Smart Contract "Appoints" an external "Deputy" addresses and appoints it to be able to open any Data NFT in the Smart contract possession.

**This is exactly what is possible thanks to the Appointer > Delegator Pattern for "Deputizing"**
{% endhint %}

### Th**is pattern enables some powerful new use cases for Data NFTs:**

* [data-coalition-daos-dc-daos.md](../../pre-aithra-r-and-d/data-coalition-daos-dc-daos.md "mention") - DAOs that manage your data
* **Data Leasing platforms** - Smart Contract platforms that can lease data for you (monthly subscriptions, pay-per-use, etc) by deputizing a 3rd party to use the data.
* **Complex Data NFT liquid staking/re-staking/**&#x66;ractionalization **platforms** - send your Data NFTs to a 3rd party Smart Contract which then delegates it to other Smart Contracts for nested usage of your Data NFTs (e.g. fractionalization of data ownership, liquid staking / re-staking of Data NFTs)
* ... and many more.

***

### Step by Step Guide on How can we use this Pattern:

#### **Step 1: Setup Appointer Smart Contract (SC):**

* As detailed above, the system works in an "Appointer > Delegator" design. The **Appointer** is a Smart Contract that will hold Data NFTs. This is the **Appointer Smart Contract.**
* The Appointer Smart Contract is ANY Smart Contract that exposes a specific public `viewDeputyAddress` method that returns an Address of an appointed "Deputy" that can Open the Data NFTs the Appointer Smart Contract holds (this is the ONLY requirement to make any Smart Contract an **Appointer**). Here is a basic [SC template for the Appointer](https://github.com/Itheum/core-mx-deputy-appointer-interface-sc) Smart Contract you can use for reference or as a base to build on top of.

#### **Step 2: Nominate a "Deputy"**&#x20;

* The Deputy is just an end-user wallet" (externally owned wallet) that will be able to use the [data-nft-sdk](../../pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/ "mention")or other Itheum Protocol tooling to "open and view data" of the Data NFTs held inside the **Appointer Smart Contract.**&#x20;

#### **Step 3: The Deputy uses the** [data-nft-sdk](../../pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/ "mention")**to "open" the Data NFT**

* The deputy can now programmatically open a Data NFT that is stored inside the Appointer Smart Contract. It does this by using the Data NFT SDK. _To understand this, let's go step-by-step on how to implement and test..._

1. Launch the Appointer SC as above.
2. Mint a Data NFT on devnet ([test.datadex.itheum.io](http://test.datadex.itheum.io/)), log in, and go to `Mint > Mint Data NFT` form. Here is a [test Data Stream you can use](https://raw.githubusercontent.com/Itheum/data-assets/main/Health/H1__Signs_of_Anxiety_in_American_Households_due_to_Covid19/preview.json) OR use any other Data Stream you want.
3. Move the test Data NFTs to your Appointer SC.
4. Set a `deputyAddress` on the Appointer SC. _Check the basic_ [_SC template for the Appointer_](https://github.com/Itheum/core-mx-deputy-appointer-interface-sc) _Smart Contract._&#x20;
5. You then use the wallet of `deputyAddress` to open the Data NFT of the Appointer SC.
6. Install the latest version of the [data-nft-sdk](../../pre-aithra-developers/software-development-kits-sdks/data-nft-sdk/ "mention") - and use this code sample for how to get your Deputy to open the Data NFT

{% code overflow="wrap" lineNumbers="true" fullWidth="true" %}
```javascript
// "@itheum/sdk-mx-data-nft": "2.7.0" (or above)
// "@multiversx/sdk-dapp": "2.28.0"

// import { DataNft, ViewDataReturnType } from "@itheum/sdk-mx-data-nft";
// import { useGetLoginInfo } from "@multiversx/sdk-dapp/hooks";
// const { tokenLogin } = useGetLoginInfo();

  async function fetchViaDeputyPersona() {
    const deputyAppointerSCAddress = "erd1qqqqqqqqqqqqqpgqd2y9zvaehkn4arsjwxp8vs3rjmdwyffafsxsgjkdw8";

    const _dataNfts = [];
    const nfts = await DataNft.ownedByAddress(deputyAppointerSCAddress, ["DATANFTFT-e0b917"]);

    _dataNfts.push(...nfts);

    const dataNft = _dataNfts[0]; // assuming we just had one Data NFT on the SC (for quick testing)

    if (!(tokenLogin && tokenLogin.nativeAuthToken)) {
      throw Error("No nativeAuth token");
    }

    const arg = {
      mvxNativeAuthOrigins: [decodeNativeAuthToken(tokenLogin.nativeAuthToken).origin],
      mvxNativeAuthMaxExpirySeconds: 3600,
      fwdHeaderMapLookup: {
        "authorization": `Bearer ${tokenLogin.nativeAuthToken}`,
      },
      asDeputyOnAppointerAddr: deputyAppointerSCAddress, // SC DOES expose viewDeputyAddress
    };

    const res = await dataNft.viewDataViaMVXNativeAuth(arg);

    if (!res.error) {
      if (res.contentType.search("application/json") >= 0) {
        const purifiedJSONStr = DOMPurify.sanitize(await (res.data as Blob).text());
        res.data = JSON.stringify(JSON.parse(purifiedJSONStr), null, 4);
      }

      console.log("WORKS! +++++++++++");
      console.log(res.data);
      console.log("+++++++++++");
    } else {
      console.error(res.error);
    }
  }
```
{% endcode %}

7. The SDK's `asDeputyOnAppointerAddr` param is optional,  if you leave it out, then you (as the Deputy) need to OWN the Data NFT to open it.
8. Here are some potential errors you can get:
   1. There is an issue with the Appointer SC interface. i.e. public `viewDeputyAddress`
   2. The Appointer SC did NOT nominate your logged-in wallet as the Deputy
   3. &#x20;The Appointer SC does not have the Data NFT you are trying to open

{% hint style="info" %}
As you can see, this enables some powerful use cases for Itheum Data NFTs. Give it a go and reach out to us if you need any help
{% endhint %}
