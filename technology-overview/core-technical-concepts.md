# ⚙️ Core Technical Concepts

The architectural components described in the prior section support an ecosystem capable of enabling the minting and evolution of assets in LAOS. Crucially, the <mark style="color:green;">**trading**</mark> (and any other ownership-related concept) <mark style="color:green;">**can be managed either in the LAOS ownership chain, as well as in any other blockchain of choice;**</mark> both EVM and non-EVM cases are compatible, as long as they support smart contracts.&#x20;



## I. Universal Location

Universal Location emerged as a natural evolution of the MultiLocation standard that was already in use within the Polkadot ecosystem, and is now part of XCMv3, the third version of their <mark style="color:green;">**Cross-Consensus Messaging (XCM)**</mark> pattern.

As the Relay Chain serves as the consensus parent for all Parachains, it has been possible to design trustless message-passing patterns among Parachains, for example, by leveraging the light clients that collators of Parachains have from other Parachains.

MultiLocation assists this communication by identifying every single location that exists within the world of consensus systems that share a common parent, an example being all Parachains, as their finality derives from the consensus in the parent Relay Chain.

By contrast, Polkadot’s XCMv3 introduced <mark style="color:green;">**the concept of a Universal Location under which all systems which generate their own consensus exist**</mark>, and by extension, all possible locations within consensus. The Universal Location is the only location that has no parent. In typical filesystem formatting, the Universal Location can be thought of as the root, often represented by the starting ’/’ symbol of a path.



## II.Bridgeless Evolution&#x20;

The simplest usage of LAOS for developers that want the ownership of assets to be managed by a different blockchain (e.g. Ethereum) is to simply <mark style="color:green;">**mint assets in the origin blockchain, and use a LAOS MultiLocation string**</mark>, using the Universal Location ’/’ as root, to specify the tokenURI, effectively using to create a concrete implementation of pattern:&#x20;

&#x20;                                  _tokenURI: tokenId → LAOS MultiLocation_

All that DApps need to build applications that use this pattern is to <mark style="color:green;">**query a LAOS node to resolve tokenURIs and provide asset meta-data**</mark><mark style="color:green;">.</mark> This pattern basically links the asset metadata to an updatable slot governed by a consensus system, with transparency, traceability, and data availability for both current and past states. And it does so in a flow which, ultimately, does not require any trusted party.&#x20;

In this pattern, however, one transaction per asset mint is still required in the origin blockchain, potentially running into scalability issues or incurring in high gas prices.



## III. Full Bridgeless Minting and Evolution&#x20;

The previous pattern can be extended to make a fully optimal use of the origin blockchain, to the extreme that one single transaction to the origin blockchain is required, on deploy time. After this initial transaction, all minting and evolution can be <mark style="color:green;">**offloaded to LAOS.**</mark>

This overview will briefly address two main characteristics of this extension of bridgeless minting/evolution and their resulting flow. The linked technical whitepaper in the prior section is available for deeper reading on each.&#x20;

### a. Encoding & Decoding

The setup starts with the usage of a concrete pattern to generate ids for assets, enabling the encoding of a generic web3 address (w3a) into the asset id itself:

&#x20;                           _Enc : w3a, Ω → id_&#x20;

&#x20;                                            _Dec : id → w3a_&#x20;

### b. Smart Contract Logic&#x20;

The ERC721/1155 smart contract logic required in the origin blockchain must contain a minor code extension in the implementation of the _ownerOf_ (and related) methods, allowing to retrieve the initial owner from the asset id in case that the asset has not been traded yet.

The final ingredient required for bridgeless minting is implemented in LAOS, by simply using exactly the same encoder/decoder functions to name assets in the Evochains, and declaring assets in these particular collections as foreign assets. <mark style="color:green;">**In effect, all assets ever assignable to all potential initial owners are reserved on deploy, and the LAOS consensus system is assigned the responsibility to fill-in the corresponding initially-empty registers as assets are minted, and modify them as they are evolved.**</mark>
