---
description: >-
  Given our architecture you can see that one chain is in a more powerful
  position than the remaining one. This chain is called the HUB chain.
---

# Selecting a HUB Chain

## Properties of a good HUB chain

### Rapid Transaction Finality

The hub chain will be responsible for many actions within Farsight. Not only will it be the default "storage location" for names, it will also be involved as a root of trust when dealing with data sources on other chains.

This requires the HUB to often pass along transactions to other chains, meaning a spoke sends a message to the HUB, then the HUB passes that along to the chain that the actual action is meant to happen on.

In order for a message to be passed Axelar GMP has to first confirm that the transaction triggering the message is final. This means that it is very unlikely for that transaction to be removed from the blockchain again.&#x20;

A lot of chains are prown to mechanism that can remove transactions called "reorg" ([Read more](https://learnmeabitcoin.com/technical/chain-reorganisation)).\
When messages are sent from chains that are susceptible to reorgs Axelar usually has to wait a couple of blocks to make sure that a reorg after that is very unlikely. This obviously adds a lot of delay to the message delivery and should be avoided for the HUB chain.

For rapid transaction finality we need:

1. No Reorgs
2. Short block times

SEI is about to be the market leader in terms of transaction finality and a reasonable choice here.

### Consistent & Low Gas Fees

* Gas fluctuations cause bad UX (increasing gas, needing to manually refund etc)\
  \-> Especially cause tx submission can be minutes away from execution on target chain
* Hub often part of the GMP call chain\
  \-> Need to pay that gas fee rather often

Nowadays many chains provide this, SEI is just one of them

### IBC Messaging

* Axelar enables GMP across non Cosmwasm chains
* IBC enables it across Cosmos chains\
  \-> Axelar could do it as well but it's more expensive (computationally, therefore we expect there to be higher fees to it)\
  \-> IBC is faster than Axelar

Sei is IBC enabled and it will be possible for us to use IBC messaging from here



## Nice to Haves

### Infrastructure for Marketplaces

We think that there really is no need for every DApp to create it's own order matching & liquidity system by themselves.&#x20;

Farsight will include a marketplace for buying & selling and bidding on names. \
Being able to use existing architecture to build this marketplace reduces the probability of introducing security weaknesses and prevent liquidity and listing fragmentation which is a very common issue on chains like Ethereum / Polygon...&#x20;
