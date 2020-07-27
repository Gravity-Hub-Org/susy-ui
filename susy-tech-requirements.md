  
# SuSy: Technical requirements

### Abstract

This document describes technical requirements for SuSy and recommendations on how to implement concrete interfaces. When implementing new modules for SuSy, the *core principles of interfaces* and *abstractions* must not be violated. 

---
### Table Of Contents

1. Gravity Node participation.
2. SuSy Extractor’s uniqueness and specifics.
3. Future extension of the App.

This document only describes the most vital components of the system. 


---
#### 1. Gravity Node in relation to SuSy

Strictly speaking, the SuSy application conforms to all of the requirements specified by Gravity Protocol. This includes the requirement of having at least two specific Nebulae (smart contracts in a targetchain) and two specific extractors for each Nebula.

Comparing to *the ordinary Gravity Protocol Node*, it is worth mentioning that *SuSy* differs from it ***only by having dedicated nebulas and extractors***. SuSy conforms to the constraints of the legder, and this dependency is crucial for the system to work.

A Gravity Node operates *under the hood* of SuSy, being mainly responsible for reaching the consensus about cross-chain transactions.

#### 2. Distinguishing features of the SuSy Extractor

The main goal of the SuSy Extractor is to manage the state on both chains.

With regard to the Extractor's behavior, SuSy aims to establish specific jobs for it, such as:
1. *Management of the payment states on both chains (target and source).*
2. Confirmation/rejection of results
3. Tracking the payments queue (which payment to execute at a specific point in time).


![SuSy extractor](https://i.imgur.com/GuQD90A.png)

The implementation of the SuSy extractor follows these principles:
A) Provide a second layer of logic on the highest accessible data transport controller (HTTP). 
B) Incapsulate interactions with pulse tx, or lock funds on chain "A" and unlock on chain "B".
C) Expose routes to necessary overview information such as "data feed tag" and "description"
D) Provide a sole route for accessing the transfer state, handle it according to parameters (chain, network id, sender address).
E) Pulse transaction should be encapsulated (*the user should know nothing about the internal ledger*)

SuSy Extractor operates mainly through ***fetching*** and ***delivering*** current info about payments on specific chains. Because of the potential difference in APIs, the getters of chain info should be maintained using ***different adapters*** for each specific blockchain. Adapters inside the extractor achieve compatibility by combining ***multiple*** chains. 

To summarize, SuSy ***only has a single extractor***, whereas ***multiple chains compatibility*** requires ***multiple instances of the same extractor***. This is achieved by ***switching adapters*** inside the extractor ***at runtime***. *(the example is in the specification)*. 
