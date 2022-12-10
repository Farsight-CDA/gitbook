---
description: >-
  In order to understand why we need a cross-chain aware blockchain name system
  we have to take a look at why the existing name systems are not actually
  solving the problem that they are meant to solve!
---

# Shortcomings of existing blockchain name systems

## Scope

For this page, we have looked into the following name systems:

* ENS
* Starname
* Unstoppabledomains

## Accessibility

We define "Accessibility" as how big the group of people is that can access the service without any previous actions (like installing / funding wallets etc.)

What we found is that all existing name systems are limited to one ecosystem, if not only one chain. If you want to use ENS, you need EVM wallets and own some Ether on the Ethereum mainnet. It's unlikely that new users will have that set up.

Starname is in a better position by being a Cosmos chain. Using IBC, it _will_ be possible to register a name from most chains within the Cosmos while being able to pay fees in a variety of assets.\
While the Cosmos will continue to integrate better into other chains, there are limits to how far this will go!

In all cases the accessibility is quite limited and only targetting a relatively small subset of crypto users but only very few users that are just joining the space.

## Pricing

Name costs must both be low enough to be worth it for the average user and flexible enough to adjust the price for "contested" names. Additionally, we think that there should be free names to especially target new users joining into the space.

We think ENS does a great job at the first 2 tasks: \
\- Free names are available for as little as `0.004 ETH`, the shorter the name, the more expensive it gets\
\- "Contested" names that were just released will undergo an [Exponential Dutch Auction](https://artblocks.wiki/Community/Dutch-Auction-Results#different-types-of-dutch-auctions), allowing the highest bidder to get it.

However, ENS does not offer a free tier for `.ens` names. It is however possible for services to offer free subdomains for their domain, which finds use for example in [cb.id.](https://help.coinbase.com/en/wallet/managing-account/coinbase-ens-support)



Most other name systems we looked at use an even simpler approach, with just a flat price per name length. This is an issue as it leaves access to "contested" names to luck or even an external factor like the validator creating the block!\
Another issue is providing unlimited free names, as this encourages bots claiming and selling all names that users might be interested in.

## Namespace Conflicts

It is very tempting to offer a wide variety of top-level-domains (**tld's**) for sale. The available namespace gets a lot bigger and users would have maximum freedom choosing their names.

However, we agree with the [vision of ENS](https://medium.com/the-ethereum-name-service/why-ens-doesnt-create-more-tlds-responsible-citizenship-in-the-global-namespace-7e66658fe2b1) in that regard. In order for name systems to be useful, we need a globally accepted namespace across all sectors. Currently, there is pretty much a name system for every single chain offering their own set of tld's that interfere with each others.\
Apart from conflicting with each others, they are also often times conflicting with the biggest accepted name service we have: **DNS.**&#x20;

Name systems must integrate into the world we are in and not try to create a new one! Therefore, name systems should respect names registered in DNS and in an ideal world DNS would respect names registered in blockchain name systems.



ENS seems to be the only name system out there to realize and address this issue. Other name systems like Starname allow you to register the entire namespace: Including all tld's used by other name systems.

##





