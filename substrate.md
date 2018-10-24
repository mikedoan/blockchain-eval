# Substrate Evaluation

**Summary -** Substrate is a chain layer which allows pluggable consensus, definition of storage through the seperation of "extrinsics" and abstracts the runtime design allowing for blockchain providers to decide which runtime best suits there application needs. It also has been built with light client protocol in mind with a number of storage and pruning options giving the ability to clearly seperated different actors requirements for infrastructure (e.g. participants can run a light client on a mobile device and validators can run full nodes with gauranteed performance and uptime). On top of this Polkadot sits as a relay chain (built on Substrate) which allows private chains to share infrastucture such as validators.

## Reference Material

### Blockchain Explorers
* [polkadash.io](http://polkadash.io/)
* [polkascan.io](https://polkascan.io/)
  * [BBQ Birch - Testnet](https://polkascan.io/n-pre/bbqbirch/)
* [poc-2.plokadot.io](https://poc-2.polkadot.io/#/explorer)
* [Substrate Explorer](https://polkadot.js.org/apps/next/#/explorer)

### Relevant Documentation
* [What is Substrate](https://www.parity.io/what-is-substrate/)
  * Substrate [Video](https://www.youtube.com/watch?v=iUMZyL5kTwc) [Slides](http://slides.com/paritytech/paritysubstrate#/)
    * [Potential Runtime Designs](http://slides.com/paritytech/paritysubstrate#/29) 
  * [Parity Substrate Wiki](https://wiki.parity.io/Parity-Substrate)
* [What is PolKadot](https://polkadot.network/#whatisit)
  * Polkadot Governance [Video](https://www.youtube.com/watch?v=VsZuDJMmVPY&t=24735s&list=PL6-IF807eaBG5sH-SQXlosqKRM2BZkrqw&index=4) [Slides](https://slides.com/paritytech/polkadot-governance#/)
  * [Polkadot Whitepaper](https://polkadot.network/PolkaDotPaper.pdf)
  * Polkadot [Video](https://youtu.be/lIghiCmHz0U?list=PLaZFi8ZkzUvKGyWTQ999rbHUXfDQv2LRF) [Slides](https://www.slideshare.net/gavofyork/polkadot-presentation)
  * [Gavin Wood Podcast on Polkadot, Sharding and Substrate](https://www.zeroknowledge.fm/46)
  * [Polkadot runtime Environment : Alternative Implementation Grant](https://docs.google.com/document/d/1iaIWmfV-uA7Uv1O4yt9G2t_86q18h_r7i5T1t-_EZ-s/edit) - [Github](https://github.com/w3f/Web3-collaboration/issues/12)
* [Token Economics - DOTS](https://polkadot.network/memorandum)
* [Secret Store](https://wiki.parity.io/Secret-Store.html) shard key generation
* [Parity Ethereum IPFS](https://wiki.parity.io/IPFS)
* [Cosmos vs Polkadot](https://medium.com/@davekaj/blockchain-interoperability-cosmos-vs-polkadot-48097d54d2e2)



### Relevant Code Links
**Key Repositories**
* [ParityTech](https://github.com/paritytech)
  * [Substrate](https://github.com/paritytech/substrate)
    * [Generalize the Consensus Infrastructure](https://github.com/paritytech/substrate/pull/883)
      * [Pluggable Consensus Import Queue](https://github.com/paritytech/substrate/issues/784)
  * [Polkadot](https://github.com/paritytech/polkadot)
  * [WASMI](https://github.com/paritytech/wasmi)

* [Web Assembly (WASM)](https://webassembly.org/)
  * [GO - support for WASM](https://github.com/golang/go/issues/18892)
  * [GO WAGON](https://github.com/go-interpreter/wagon)
  * [GO Perlin](https://github.com/perlin-network/life)
  * [Rust Parity Tech WASMI](https://github.com/paritytech/wasmi)

**Functional Breakdown**
* Persistence
  * Storage
    * [RocksDB](https://rocksdb.org/)
    * [DB Code](https://github.com/paritytech/substrate/tree/master/core/client/db)
    * Data Overview - Light Client 
      * Block Structure [Slide 17](http://slides.com/paritytech/paritysubstrate#/17) to [28](http://slides.com/paritytech/paritysubstrate#/28)
    * [decl_storage - macro](https://wiki.parity.io/decl_storage)
    * [Get and Set Storage](http://slides.com/paritytech/paritysubstrate#/14)
  * Light Client
    * [DB Code](https://github.com/paritytech/substrate/blob/master/core/client/db/src/light.rs)
    * [Light Client Code](https://github.com/paritytech/substrate/tree/master/core/client/src/light)
  * Node
    * [Client Code](https://github.com/paritytech/substrate/tree/master/core/client/src)
  * Validator
  * Archive Node
* Distribution
  * Discovery
  * Gossip
    * [libp2p](https://github.com/ethereum/wiki/wiki/libp2p-Whitepaper)
    * [Substrate Code - network libp2p](https://github.com/paritytech/substrate/tree/master/core/network-libp2p)
    * [Get and Set Storage](http://slides.com/paritytech/paritysubstrate#/14)
  * Message Format
    * [Substrate Primitives](https://github.com/paritytech/substrate/tree/master/core/primitives)
    * [Polkadot Parachain Primitives](https://github.com/paritytech/polkadot/blob/master/primitives/src/parachain.rs)
    * [Polkadot Collator - Logic](https://github.com/paritytech/polkadot/blob/master/collator/src/lib.rs#L17)
  * [Execution](http://slides.com/paritytech/paritysubstrate#/15)
    * [Runtime](https://wiki.parity.io/impl_stubs)
    * [impl-stubs](https://wiki.parity.io/impl_stubs)
    * [SRML](https://github.com/paritytech/substrate/tree/master/srml)
      * [SRML Node Template](https://github.com/paritytech/substrate-node-template)
  * Consensus
    * [Hybrid Consensus Slide](http://slides.com/paritytech/paritysubstrate#/17)
    * [Generalized Consensus Pull Request](https://github.com/paritytech/substrate/pull/883)
    * [Consensus Code](https://github.com/paritytech/substrate/tree/master/core/consensus)
    * [Rhododendron - Asynchronously safe BFT consensus, implementation in Rust](https://github.com/paritytech/rhododendron)
    * [Random Number Generation CSPRNG](https://en.wikipedia.org/wiki/Cryptographically_secure_pseudorandom_number_generator)
      * [Rust-Random](https://github.com/rust-random/rand)
    * Block Finality
      * [GRANDPA (GHOST-based Recursive Ancestor Deriving Prefix Agreement)](https://medium.com/polkadot-network/grandpa-block-finality-in-polkadot-an-introduction-part-1-d08a24a021b5)
        * [Finality GANDPA Code](https://github.com/paritytech/finality-grandpa)
        * [Substrate using GRANDPA](https://github.com/paritytech/substrate/blob/master/core/finality-grandpa/src/lib.rs)
* Security
  * Signing
    * [ED25519](https://ed25519.cr.yp.to/)
  * Hashing
    * [Substrate Code - hashing.rs](https://github.com/paritytech/substrate/blob/master/core/primitives/src/hashing.rs)
    * [Blake2](https://blake2.net/) [use in substrate](https://github.com/paritytech/substrate/search?q=blake2&unscoped_q=blake2)
    * [XXHASH](https://cyan4973.github.io/xxHash/) [use in substrate](https://github.com/paritytech/substrate/search?q=TWOX&unscoped_q=TWOX)
  * Privacy
* Governance
  * Staking
  * Voting
* Chaincode
  * See WASM above
  * [Rust Parity Tech WASMI](https://github.com/paritytech/wasmi)
  * [Use in Substrate Code](https://github.com/paritytech/substrate/search?q=wasmi&unscoped_q=wasmi)
* Deployment
  * Substrate
    * [Locally on Mac](https://github.com/paritytech/substrate#on-mac)
    * [From Code Base](https://github.com/paritytech/substrate#on-mac)
  * Polkadot
* Interledger
  * Message Format
  * Relay Chain
  * Consensus Process
* Developer Tools
  * API
    * [Polkadot Javascript API](https://polkadot.js.org/api/)
  * RPC
    * [Substrate Code](https://github.com/paritytech/substrate/tree/master/core/rpc)
  * CLI
    * [CLI](https://github.com/paritytech/substrate/tree/master/core/cli)
  * SDK
* Off Chain Orchestration
  * Oracles
  * Workflow
* Wallets
  * Feather
* Chain Tools
  * Governance
  * Token Economics
  * Token Standards
* Business Tools
  * Analytics
  * System Monitoring 
  * Deployment Tools

**Key Pull Requests or Features**

## Substrate Prototyping

**Deploying a Substrate Chain**
* [Overview](https://hackmd.io/y-E9Q9jTRreni6z9EU0kkA#)
* [Locally](https://github.com/paritytech/substrate#on-mac)
* [From Code Base](https://github.com/paritytech/substrate#on-mac)

**Deploying Polkadot**
* [Overview](https://github.com/paritytech/polkadot#4-hacking-on-polkadot)

**Deploying a simple contract**
* [Preparing to build on Polkadot](https://medium.com/polkadot-network/preparing-to-build-on-polkadot-349ff5002885)
* [Writing a WASM Contract](https://wiki.parity.io/WebAssembly-Home)

**Running a Transaction**
* [Balance Transfer via API](https://polkadot.js.org/api/examples/promise/07_transfer_dots/)