# Guide 4: Use the Data NFT "Deputy" Feature to delegate access of your Data NFTs to a Smart Contract

The system works in an "Appointer > Delegator" design. The Appointer is a smart contract that will hold Data NFTs. It exposes a public `viewDeputyAddress` method that returns an Address of an appointed "deputy" that can Open the Data NFTs the Appointer smart contract holds. Here is a basic
