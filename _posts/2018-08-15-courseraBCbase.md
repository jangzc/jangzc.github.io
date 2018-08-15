---
layout:     post
title:      Coursera的区块链base课程要点
subtitle:   
date:       2018-08-15
author:     Jang
header-img: img/post-bg-debug.png
catalog: true
tags:
    - BlockChain
---

### Week One: Defining a Blockchain<br>
The blockchain technology supports methods for<br>
* a decentrailized peer-to-peer network
* a collective trust model among unknown peers
* a distributed immutable ledger of records of transactions
<br>

**Decentralization** means the network operates on a user-to-user(or peer-to-peer) basis.

A **Distributed Immutable Ledger** means the data does not sit on one all-powerful server and the data stored in it cannot be deleted or edited

Transactions bring about transfer of value in Bitcion Blockchain. The concept UTXO defines the inputs and outputs of such a transaction.

Once a block is verified and algorithmically agreed by the miners, it is added to the chain of blocks, viz., the blockchain.

An **Unspent Transaction Output(UTXO)** can be spent as an inout in a new transaction.

The main operations in a blockchain are transaction validation and block creation with the consensus of the participants.Yet, there are many underlying implicit operations, as well.

A **Smart Contract** provides the very powerful capability of "code execution" for embedding bussiness logic on a Blockchain.

Significant innovations such as smart contracts have opened up boarder applications for blockchain technology.Private and permissioned-blockchains allow for controlled access to the blockchain, enabling many diverse business models.

In a **Private Blockchain**, access to the Blockchain is limited to selected participants.

**Permissioned or Consortium Blockchain** has the benenits of a public blockchain with allowing only users with "permission" to collaborate and transact.

### Week Two: Ethereum Blockchain<br>
Smart contracts add a layer logic and computation to the trust infrastructure supported by the blockchain.

Smart contracts allow for execution of code, enhacing the basic value transfer capability of the Bitcion Blockchain.

**Solidity** is the high level programming language code for writing smart contracts that run on EVM.

Accounts are basic units of Ethereum protocol: external owned accounts and smart contract accounts.

An Ethereum transaction includes not only fiedls for transfer of Ethers but also for messages for invoking smart contract.

**Externally Owned Accounts**, or EOA, are controlled by private keys.

**Contract Account**, or CA, are controlled by code and can be activated only by an EOA.

An Ethereum block contains the usual prev block hash, nonce, transaction details, but also about gas(fee) limits, the state of the smart contracts and runner-up headers.

**Transaction Validation** involves checking the timestamp and nonce combination to be valid, and the availiablity of sufficent fees for execution.

**Miner Nodes** in the network receive, verify, gather and execute transactions.

Any transaction in Ethereum, including transfer of Ethers, requires fees or gas points to be specifiled in the transaction.

**Gas Points** are used to specify the fees instead of Ether for ease of comparison using standard values

Miners are paid fees for security, validation, execution of smart contrac as well as for creation of blocks

### Week Three: Algorithms and Techniques<br>

**Elliptic Curve Crypography(ECC)** family of algorithms is used in Bitcoin as well as Ethereum Blockchain for generateing the key pair.

**Rivest-Shamir-Adelman(RAS)** is a commonly used implementation of public-private key in many applications, except Blockchains because of its need for a more efficent and stronger algorithm.

**Hashing** transforms and maps an arbitrary length of input data value to a unique fixed length value.

The following are two basic requirements of a hash function.
* make certain that one cannot derive the original items hashed from the hash value
* make sure that the hash value uniquely represents the original items hashed

A combination of hashing and encryption are used for securing the various elements of the blockchain. Private-public pair and hashing are important foundation concepts in decentralized networks that operate beyond the trust boundary.

**Asymmetric crypography** uses public-private key pairs to encrypt and decrypt data.

### Week Four: Essentials of Trust
