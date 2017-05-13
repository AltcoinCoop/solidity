# Getting started with Solidity development - OS X

## Learning Contracts & Solidity

### Core Docs
* Read all the pages here like twice:
https://solidity.readthedocs.io/en/develop/  
https://www.youtube.com/watch?v=8jI1TuEaTro  
* Solidity changelog (new features, bug fixes, etc...)
https://github.com/ethereum/solidity/blob/develop/Changelog.md
 
### Blogs & Guides
https://github.com/fivedogit/solidity-baby-steps/tree/master/contracts/  
https://www.ethereum.org/token    
https://www.ethereum.org/crowdsale  
https://www.ethereum.org/dao  
https://medium.com/zeppelin-blog/the-hitchhikers-guide-to-smart-contracts-in-ethereum-848f08001f05  
https://hackernoon.com/getting-started-as-an-ethereum-web-developer-9a2a4ab47baf  
https://github.com/ConsenSys/Tokens
https://github.com/ConsenSys/MultiSigWallet

### Forums & Community
https://ethereum.stackexchange.com/  
https://gitter.im/ethereum/home  
https://www.reddit.com/r/ethereum/  
https://stackoverflow.com/questions/tagged/ethereum  

### Contracts Repos
https://github.com/ethereum/dapp-bin  
https://github.com/ethereum/dapp-bin/tree/master/getting%20started  

---

## Dev tools - OS X

### geth
https://geth.ethereum.org/  
```
$ brew tap ethereum/ethereum    
$ brew install ethereum  
$ geth --version  
```

### solcjs
```
$ npm install -g solc 
$ solcjs --version
```

### solc
http://solidity.readthedocs.io/en/develop/installing-solidity.html  
Follow instructions to build from source  
```
$ solc --version  
```

### Truffle
https://github.com/trufflesuite/truffle  
```
$ npm install -g truffle
$ cd <new-project-folder>
$ truffle init // for contracts only proj
$ truffle init webpack // for a contracts + web dapp proj
```

### Dapple
https://github.com/dapphub/dapple   

### Webpack-based dev seed
https://github.com/uzyn/ethereum-webpack-example-dapp  

### Testrpc
https://github.com/ethereumjs/testrpc  
```
$ sudo npm install -g ethereumjs-testrpc
$ testrpc
```

Testrpc dcoker
```
$ docker run -d -p 8545:8545 ethereumjs/testrpc:latest
```

### Intellij Solidity syntax support
https://plugins.jetbrains.com/plugin/9475-intellij-solidity  

### Remix
https://github.com/ethereum/remix  
Online solidity compiler 
https://ethereum.github.io/browser-solidity/

```
$ git clone https://github.com/ethereum/remix
$ cd remix
$ npm install
$ npm start
```

### OpenZepellin
Open source solidity libs and basic contracts
https://github.com/OpenZeppelin/zeppelin-solidity
http://zeppelin-solidity.readthedocs.io/en/latest/
https://openzeppelin.org/

Truffle integration - use npm to install zepellin contracts

### Test Networks

* Rinkeby (modern)  
https://www.rinkeby.io/  -> connect yourself  
Download the json file and follow the instructions  

https://faucet.rinkeby.io/
Get ether by creating a bpublic gist with your rinkeby account public key

### Running geth in a container
https://github.com/ethereum/go-ethereum/wiki/Running-in-Docker

### Block Explorers & Network Stats
https://etherchain.org/  
https://ethstats.net/  
https://live.ether.camp/  
https://etherscan.io/ 

---

## Basic Concepts
* contracts
* account types - external or contract. Has an address and a balance. External accounts have key paris
* transactions - tpyes: contract creation, move funds to an account, call a contract method
* message calls - calldata area, used in transactions
* delegate calls - using caller context for library / util functions
* Gas - gas price and gas amount set by transaction initiator. Used for code execution
* Events & Logs
* EVM - stack-based machine, contract storage and memory (runtime env)
* throw
* Suicide
* Get block number
* Constant fucntions
* Obtaining contract address
* Global variables - msg, tx, block
* Getting call data from the Message global var - msg.value, msg.sender, msg.data
* Working with transactions - tx.*  
* Working with Gas - msg.gas,  tx.gasprice - gas caller is willing to pay 
* this === address
* The unamed function with optional payability

## Gas
* Estimating transaction gas cost:
```
solc --gas MetaCoin.sol
```

## EVM Considirations
* use explicit data type instead of var - for (var i=0; i < items.length;i++) - i is compiled to an uint8. If items.length > 255 then the loop will never terminate and deplate gas. Use explicit type instead without the var. e.g. - for (uint i=0; ...)
* Avoid loops wherever possible - if a transaction exceeds its gas limit then it is rolled back but the gas is still paid. If a block reaches its gas limit then...
* There are 20 kinds of overflow/underflow when working with the supported integeral data types - use safe math. e.g. SafeMath.sol
* An attacker can reliably and easily make ANY call from inside your code to fail. The EVM call stack is limited to 1024 method calls. An attacker can always call a method 1023 times and call any contract's method on the 1024-th call - causing an overflow error in the next call made from implementation of the method. e.g. causing a send to always fail. As a workaround - use pull and not push to distirbute funds
* Be aware of solidity bugs and issues - Soldity/EVM is a young tech (not yet v1.0)
https://github.com/ethereum/solidity/issues/

## Fundemental Design Tradeoffs
* Mistakes can be very costley. Unlike web apps, deployed contracts are hard to modify 
* Modular vs. Monolith - upgradeable vs. less complex, easier to test and to reason about
* Code Resuse vs. Duplicate - should you trust other people contracts ?

---
## Data Structures, Libraries and Utils

### Built-in data types
* basic data types
* structs
* mappings - associative arrays with all non-existing items map to 0/null
* state vars

### Std
https://github.com/ethereum/solidity/tree/develop/std

### Additional Data Structures
https://github.com/ethereum/dapp-bin/tree/master/library  

### key-value Stores
https://github.com/ConsenSys/dapp-store-contracts  

### Live Libs Project
https://github.com/consensys/live-libs

---

## Testing 
* Testing with testrpc
* Testing with testrpc and truffle
```
https://github.com/ethereumjs/testrpc
http://truffleframework.com/docs/getting_started/javascript-tests
```
* Testing a private test network
* Testing with a public testnet
* Security audits options
* Testing with docker
* Coverage tool https://github.com/JoinColony/solcover
* Testing Rollout - testrpc, testnet, beta on privte net, beta on public net, relase public net

https://github.com/Capgemini-AIE/ethereum-docker  

## Debugging, Logging & Events

* Events use cases intro - https://media.consensys.net/technical-introduction-to-events-and-logs-in-ethereum-a074d65dd61e

## Disassembliy and Decompilers
https://etherscan.io/opcode-tool?a=0x9e1b57fc92eba6434251a8458811c32690f32c45  

## Additional Contracts Examples - learn from code
https://github.com/melonproject/melon/tree/master/contracts
https://github.com/gavofyork/melon/tree/master/contracts
https://github.com/ethereum/dapp-bin/tree/master/getting%20started  

## Additional Tools
https://github.com/raineorshine/solgraph

## Community Standards
* ERC20 - standard coin: https://github.com/ethereum/EIPs/issues/20

## Coding Style Guide
http://solidity.readthedocs.io/en/latest/style-guide.html

---

## Security - Considirations, Patterns & Best Practices
https://solidity.readthedocs.io/en/develop/security-considerations.html
https://github.com/ethereum/dapp-bin/tree/master/standardized_contract_apis  

* Beware of external contracts calls - they can call back to your contract and change its control flow
* Private data is viewable by anyone
* All your public contract methods may be called maliciously
* Bug bounty hunt your contracts on a test network and perform security audits with highly reputable 3rd parties
* Follow platform security notifications: https://blog.ethereum.org/category/security/

https://medium.com/zeppelin-blog/onward-with-ethereum-smart-contract-security-97a827e47702

### Security Audits
https://medium.com/zeppelin-blog/blockchain-capital-token-audit-68e882d14f0
https://medium.com/zeppelin-blog/cosmos-fundraiser-audit-7543a57335a4

### Additional Security Resources
http://chriseth.github.io/notes/talks/safe_solidity/#/
https://blog.ethereum.org/2016/06/10/smart-contract-security/
https://blog.ethereum.org/2016/06/19/thinking-smart-contract-security/

----

## Design Patterns

### Factory
A contract for registration of contract addresses deployed by an external account address   

### Pre, Mutate & Interact
* Arguably a result of the famous DAO bug
* Check all pre-conditions first before modifying any state. Interact with external contracts only after state is modified

### Throw Loudly
* Any pre-condition failure should throw excplicitally, beofore any state modificaiton is performed
* Test and throw for each pre-condition seprately
* Use this consistnelty in all code instead of conditional executaiton after a pre-condition check in an if statement
 
### Auto Bug Bounty
* Build invariants calculation into your contract - contract state is valid while all invariants hold
* Let researches try to corrupt your invariants for an award on a private copy of your contract
https://medium.com/zeppelin-blog/onward-with-ethereum-smart-contract-security-97a827e47702
https://github.com/OpenZeppelin/zeppelin-solidity/blob/master/contracts/Bounty.sol

### Standard, Basic and Crowdsale Tokens
* Standard interface and contract to allow dapps and wallets to communicate with contracts that have tokens.
http://zeppelin-solidity.readthedocs.io/en/latest/standardtoken.html

### Multi-sig Wallets
It is recommended that contracts that store large ammounts of funds will not be controlled by one account (pub/priv key paris) but by a mutli-sig wallet or by a key escrew service.

### Avoiding Magic Numbers
* Convert magic numbers such as 15 days to a contract constant

### Withdraw 
* Don't send money - let other widthdraw what they are authorized to get - favor pull vs. push payments. Issues with send: https://github.com/ConsenSys/Ethereum-Development-Best-Practices/wiki/Fallback-functions-and-the-fundamental-limitations-of-using-send%28%29-in-Ethereum-&-Solidity#abuse

### Time
* block.timestamp === Now() - epoch time in secs - can be manipulated by miners. Don't use this.
* Block numbers and average block time as approximate time units - block.number - assumes a constant rate of block generation in the future which may not be accurate - use with care. https://ethereum.stackexchange.com/questions/413/can-a-contract-safely-rely-on-block-timestamp

### Fallback
* Fallback function called when ether is sent using .send() to a contract's address
* Must use under 2,300 gas - enough only for logging - don't do more stuff here

### Circut Breaker
Designing for failure and worse-case scenarios

### Risk Management
* Rate limiting
* Max usage / Lockouts

### Design Patterns Resources
https://github.com/ethereum/wiki/wiki/Useful-%C3%90app-Patterns  
https://github.com/ConsenSys/Ethereum-Development-Best-Practices/wiki/Dapp-Architecture-Designs  
https://www.youtube.com/watch?v=XkJ8mg-R7C0  
https://github.com/ConsenSys/gnosis-contracts  
https://github.com/ConsenSys  
https://github.com/toadkicker/solidity-patterns  
https://github.com/ConsenSys/smart-contract-best-practices

---

## Crowd Funding Patterns

### Crowd Funding Campaigns - design and implementation examples
* Golem Campaign    
https://blog.golemproject.net/the-golem-crowdfunding-summary-8a3504375aa7  
https://blog.golemproject.net/gnt-crowdfunding-contract-in-pictures-d6b5a2e69150  
https://github.com/golemfactory/golem-crowdfunding  
 
* Blockchain Capital Campaign
https://medium.com/zeppelin-blog/blockchain-capital-token-audit-68e882d14f0
https://github.com/BCAPtoken/BCAPToken/tree/5cb5e76338cc47343ba9268663a915337c8b268e/sol

* rlc-token 
https://github.com/iExecBlockchainComputing/rlc-token 

* Cosmos
https://github.com/cosmos/fundraiser-lib/tree/693cf3f32e9fd679216372876dda86fa57a3277e https://medium.com/zeppelin-blog/cosmos-fundraiser-audit-7543a57335a4

* Matchpool
https://github.com/Matchpool/contracts https://medium.com/zeppelin-blog/matchpool-gup-token-audit-852a70330f2

---




