  
# SuSy: Technical requirement

### Abstract

This document represents technical details for SuSy and recommendations on how to implement concrete interfaces. *Core principles of interfaces* and *abstractions* must not be violated. 

---
### Table Of Contents

This document consists of several parts. We’ll only dive into vital parts of the system. 
1. Gravity Node participation.
2. SuSy Extractor’s uniqueness and specifics.
3. Future extension of the App.

---
#### 1. Gravity Node Participation

Strictly speaking, the SuSy application conforms to all of the requirements specified by Gravity Protocol. This includes the existence of specific Nebulas (at least 2) and 2 specific extractors for each.

Comparing to *ordinary Gravity Protocol Node* It worth mentioning that *SuSy app* differs from it ***only by having specific nebulas and extractors***. SuSy conforms to ledger constraints and its dependency is ***vital***.

Gravity Node exists and operates *under the hood* of SuSy. The first one is mainly responsible for reaching the consensus.

#### 2. SuSy Extractor’s uniqueness and specifics.

As regards Extractor's behavior, SuSy aims to set specific duties for it, such as:
1. *Management of payment state on both chains(target and source).*
2.  Results confirmation/declining
3. Observation of payments queue (which payment to operate at the exact timeframe).

The main goal the SuSy extractor should achieve - is to manage the state on both chains.

![SuSy extractor](https://i.imgur.com/GuQD90A.png)

By design we have to follow these statements:
A) Provide the second layer of logic on top accessible data transport controller (HTTP). 
B) Incapsulate pulse tx resolving. Strictly speaking, lock funds on chain "A" and unlock on chain "B".
C) Expose routes to compulsory overview data such as "data feed tag" and "description"
D) Provide route(only one) for accessing transfer state, handle according to params (chain, network id, sender address).
E) Pulse transaction should be encapsulated (*the user knows nothing about internal ledger*)

Extractor operates mainly on ***fetching*** and ***delivering*** current info about the payments on specific chains. The chain info getters should be maintained using ***different adapters*** for specific blockchain because API differs. Adapters inside the extractor combine ***multiple*** chains compatibility. 

Here the conclusion is that SuSy ***has only one extractor***. ***Multiple chains compatibility *** suggests ***multiple instances of the same extractor***. Such goal is achieved by ***switching adapters*** inside extractor ***at runtime***. *(the example is in the spec)*. 
