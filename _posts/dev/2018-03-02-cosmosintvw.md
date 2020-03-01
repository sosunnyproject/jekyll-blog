---
layout: post
categories: dev
title: "블록체인 코스모스 네트워크 조사"
date: 2018-03-02T13:01:27-05:00
share: false
---

## Jae Kwon Cosmos Interview by Epicenter

- Was looking for Consensus Algorithm without PoW component
  - found BFT algorithm
  - created Tendermint from that idea
- Tendermint: open source project
  - anyone can create own blockchain without worrying about networking/p2p/consensus/tx broadcasting; blockchain, cryptocurrency easily
  - with this, we are creating cosmos

What applications have used tendermint
- no production release yet
- PoS blockchain application not yet - Cosmos would be the first
  - cosmos will be the proof that tendermint is good to use
  - proof of concept; swift, r3, new startups building on tendermint today
  - energy companies, logging systems - proof of existence/documents, ethereum blockchain - ethermint: ethereum testnet or private net without PoW 

Cosmos and Tendermint?
- Tendermint: standalone component
  - well-defined narrowed scope
  - p2p, consensus, rpc endpoint, tx broadcasting
  - you're supposed to provide your own state machine/application logic so that tx has meaning
  - we made tendermint so that it can be a common component infra layer for all blockchain, we need it for cosmos
  - continue to maintain and develop further, secure more
  - here to stay
- tendermint is separate company - all in bits inc.software company
- we made Interchain foundation - for managing cosmos network: no for-profit, contracting all in bits and other companies to develop cosmos network, foundation
  - after fundraise, decide atom distribution
  - before hub launches, delegation game
  - atom holders choose delegate to determine validators
  - 

what is cosmos?
  - network, 
  - internet of blockchain
  - what is blockchain network? private, public.. they're not talking to each other
  - there are centralized exchange, cross=chain exchanges, but no TCP/IP or my computer talking to server via internet type of communication
  - have blockchain communicate
  - BC painpoints: interoperability, scalability, speed 
    - better architecture for BC communicate
  - bridge several BC platforms - Bitcoin, Ethereum, make easy to develop New PoS, private and public and consortium, coin/token can be transferred from one BC to another

Cosmos network
- many BC, protocols..
- first BC that's gonna launch in cosmos network is HUB
  - Cosmos Hub
    - simple PoS
    - Be a light client to other and all BC
    - clearing house at the center. not centralized. custodian
    - first component
- bridge between ethereum and bitcoin
  - bridge zones
  - adapter zones: eth - cosmos hub - bitcoin
- DEX: own BC, run by same validators of cosmos hub
  - distributed exchange
  - any token in cosmos network can be exchanged for one another
- starting with the hub, multi-asset token, building bridges out, make easy for New PoS
- BC function as db and different chains are independent db, but ultimately it's gotta be one big db

Consensus Cosmos
- tendermint BFT
- 100 validators, grow 300 in 10 years
  - signs, votes, round-based protocol
- PBFT (1999) - consensus, similar approach to this
  - suited for BC world. 
  - underlying consensus algorithm
1. tx finality in few seconds
  - no more waiting for final block
2. how is secure unless there's sth being burned like bitcoin
  - when double spend - we can find who's responsible, and punish
  - robust, fast, consensus layer 
3. on top of Tendermint, DPoS
  - you can delegate / vote
  - limited num of validators

Cryptocurrency cosmos hub?
- cosmos hub is multi-asset
- token : atom: staking token
  - not gas for now
  - more like 'virtualized bitcoin miners' 
  - atom holders: determining consensus, participate governance, pass proposals, vote to inflate atom supply, etc.
- cosmos hub: tx fee will be dividied among atom stakeholders

- Bitcoin: 6 hours waiting until transaction confirmed
- tendermint bft proof of commit can be really fast
  - proof is short: no chain of hashes, just need more than 2/3 signatures of validators
  - in the future: my phone creates transaction --> gets short data packet that proves this BC, latest Block has is xxx --> this light client is cosmos IBC's 핵심
  - merkle proof, block hash...
  - own implmentation of balancing merkle proof - binary tree, short version, based on ADL tree? 

1. destination chain learns about latest hash of center chain - block hash with proof/signatures
2. hosting a packet with merkle proof - goes all the way up to block hash
3. send a packet from one chain to another

### SWAP example
A: group of validators running one chain -- Asset Aapple
B: group of validators own atom, running the hub 
C: group of Validators running another chain -- Assent MSFT
Move Apple share to C chain from A chain

A account in Cosmos hub
C account in Cosmos hub
you can do swap transaction in the hub
you can use DEX but don't need to just swap

A - petrician tree 
- packet move from A to C chain
- reserved for outbound packet
- 