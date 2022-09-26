# Design

### Backend

The backend consists of many smart contracts (programs that run on the Ethereum blockchain) that execute the ad bidding platform's logic and rules, resulting in state changes on the underlying blockchain. Smart contracts are developed in Solidity and deployed as part of the setup and configuration of the ad-bidding platform. The EVM interprets state changes on the global state machine and executes the logic defined in smart contracts. The high-level smart contracts are compiled into bytecode, which the EVM can then execute.

Composable NFTs representing _Adasset_ for the ad-auction platform is a key design component. It is defined based on ERC 998 token standard that stores and keeps track of child tokens (ERC 721) representing the individual ad-containers within a scene or game. The token standard is defined to encapsulate multi-resources whereby the output depends on context. Ex: a 2D and 3D image of an advertised product will be represented as different resources within the token. Moreover, mimetic metadata principle is followed whereby layers of metadata are defined such that visual or tech functions updates are handled as in-token ‘update’.

Microservices powered APIs are also part of the backend infrastructure, which will provide off-chain functionality required by the front end applications.

### Blockchain Network

The smart contracts and distributed state are encapsulated in the blockchain, which is a globally distributed and deterministic state machine maintained by a peer-to-peer network of nodes. The standards of consensus that the peers in the network follow are governed by the state changes on this state machine.&#x20;

### Frontend&#x20;

The front-end applications defines the user interface logic and communicates with the backend APIs and on-chain hosted smart contracts.

For the smart contracts on-chain, the front-end application must interact with one (or more) of the nodes since each node in the network contains a copy of the smart contracts and all of the distributed states. The node infrastructure is managed by a third-party service provider such as Infura or Alchemy, and the communication layer between the front end and the service provider is based on JSON RPC.

The frontend application also integrates with Metamask and other wallets to make key management and transaction signing simpler for users.

### Decentralized storage

Given that the user pays every time they add new data (a state change) to the blockchain, we must be careful about what data we store on-chain since it can quickly become extremely expensive. In this design, IPFS as a decentralized off-chain data storage solution is used for data storage related to bids, ad slots, media assets, etc. The IPFS system uses a peer-to-peer network to distribute and store data. Decentralization principles are violated when front-end code is hosted on cloud platforms like Azure or AWS. As a result, IPFS or Swarm as a decentralized storage solution will be used to store and host front-end for the distributed application.

### Querying and indexing  the blockchain state

Reading data from smart contracts on the blockchain must be well designed for a distributed app to work properly. To query and listen to smart contract events, the Web3.js library will be used. Such events will be emitted whenever a specified state change occurs, and the front-end code will listen for these events to be fired by the smart contracts and perform the appropriate actions. In some cases, the aforementioned technique can result in unnecessary complexity (example, for the bidding process). In such circumstances, the Graph will be used as an off-chain indexing solution. Specific smart contracts will be configured for indexing, including which events and function calls to listen for, as well as how to convert incoming events into entities that the front-end application can query and consume. The Graph indexes blockchain data, allowing us to query on-chain data with low latency in the application logic.

### &#x20;

