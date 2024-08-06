# Data Creator Staking

## Introduction

**Data Creator Staking module enables creators and consumers to earn by participating in the ITHEUM ecosystem.**

**Upon creating a Data NFT or NFMe ID Vault, the user will be able to see it in the bonding page. They will also be able to see statistics of the staking program.**

Max APR is set to 20%. The APR is dependent on the following

1. Combined Bonds staked(of the creator).
2. Global Total Bonded, by all users.
3. Stake start and end block of bonded Data NFTs.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXfQrFgvhAOeltP-K354G1EPsvtyE9oZ2R2hf8x1dhna66Q3RMs6HURLVqVpZECbnzQI4jxjyuSotnPa8bduamDEyB9N7wmtmsgmHK64BtvcVqa-1b6Vzxj3pJXp-ouH-9kxQRxj5BKIXKBSeY4kl0yeUrbr?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

The user can create an NFMeID Vault. If the user has no default primary, then the newly minted NFMeID will be set to the Primary. The user can choose to top-up their stake on the Primary Data NFT. This will also affect the combined liveliness and as a result the total annual rewards. Also note that when a user does a top-up, they autoclaim rewards they have accumulated till that point.

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXdLNH1PjN3HraCFgxI3b2uaxVlCLVb6ZXrk0H1irAYItbI4bhhQG-Ie-sLT-zzsZG7VYgoDgyuZdUqV0osnPat8t16kd4TlSuvpqrHBQ65xw1xKOPqyaHc2JPNCoM4H5wah0WIHmi_r4Fj0xuaYacvcZYw?key=OH8fLwS95lQR9XaMw4LPAg" alt=""><figcaption></figcaption></figure>

## Rewards Pool per block

The rewards per block are currently set to .1 ITHEUM per block. These rewards are distributed to users depending on their combined liveliness per block.

## Combined liveliness

Combined liveliness takes into account the weight of the bonds per Data NFT and the Liveliness of each Data NFT. This can be calculated by the formula below.&#x20;

_(Bond1\*LivelinessOfBond\_1+Bond3\*LivelinessOfBond\_3+Bond3\*LivelinessOfBond\_3…+ BondN\*LivelinessOfBond\_N)/(Bond\_1+Bond\_2+Bond\_3…+Bond\_N)_

## APR Calculation

APR is calculated by the below formula.

_APR = Blocks per year\*Rewards per block\*100/Total combined stake_

## Rewards

Rewards are calculated by the formula below.

_Rewards = Total rewards per year \* Total Personal bond/Total Combined Stake \* Multiplier_

Where the multiplier is a function of the combined liveliness.&#x20;

_Multiplier = Combined liveliness/100_

If however the combined livelines is above 95% then the user can receive their full rewards.

\
