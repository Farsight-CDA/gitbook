---
description: Potentially viable architectures for a cross-chain aware name system.
---

# Architecture Choices

All somewhat known name systems to date have been restricted to a single chain only which limited their architecture options.

Using general message passing we gain access to a few more design decisions we otherwise would not have.

The big underlying option is to not store all data on a single chain but move data to other chains in some cases for efficiency, security or gas cost reasons.

We will go over both options in detail for you to understand the reasoning behind our choice:

### Hub And Spokes Architecture

![](https://vishnunanduri.files.wordpress.com/2017/02/hub-spoke-generic.gif)

This architecture uses a single blockchain to store **all** state data. Changes to that data can be requested from the connected spokes using GMP.

| Pros                                                                                                | Cons                                                                     |
| --------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Looking up data is straightforward, all queries completed on one blockchain                         | Writing data from a spoke **always** requires GMP adding cost and delays |
| <p>Everything can be done in a single roundtrip between Hub &#x26; Spoke chain<br>=> 2 messages</p> | Most actions will require the full roundtrip                             |
| Battle tested and used in many projects                                                             | Not an innovation                                                        |
|                                                                                                     | Hard time integrating with other name systems on other blockchains       |

#### Simplified Query Algorithm

1. Lookup the name on the hub chain\
   **a)** Entry is found\
   Entry is your result -> Exit\
   **b)** No entry is found\
   Name does not exist -> Exit

### "Pull Out" Architecture

Instead of the names being stored on just a single hub they can be pulled out onto other chains individually. Meaning that you can store records / ownership of names on other chains.

This will not include sub-names though, those will individually need to be transferred out.

| Pros                                               | Cons                                                                                    |
| -------------------------------------------------- | --------------------------------------------------------------------------------------- |
| Mostly straightforward implementation              | Extendability on other chains (e.g. integrating other name systems) always requires GMP |
| Trading & Record management does not involve GMP   | Managing sub-names will require 1-2 GMP messages                                        |
| Reading records takes at most 2 blockchain lookups |                                                                                         |

#### Simplified Query Algorithm

1. Lookup the name on the hub chain\
   **a)** **Entry is found**\
   Entry is your result -> Exit\
   **b) Link is found**\
   ****Do 2.\
   **c)** **No entry is found**\
   Name does not exist -> Exit
2. Lookup name on the chain the link points to. This will always point to a valid entry which is your result.

### Distributed Tree Architecture

This architecture mimics DNS to some degree. Data is not stored centrally but only the root node `.` as well as the tld's are on the Hub chain.\
The ownership of subdomains can be transferred to other GMP connected chains leaving the Hub chain with nothing but a reference to the other chain.

| Pros                                                                      | Cons                                                                                                      |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| The average user only has to use GMP once for registering and never after | Complicated name hierarchies can result in certain actions requiring an arbitrary high amount of GMP hops |
| After moving your name you can manage it from any chain without using GMP | Name queries can require reading data from a series of blockchains                                        |

#### Simplified Query Algorithm

Go down the tree level by level. This means you gotta split your name at the `.` first. \
**(Continue here)** Every step you reappend one section to the queried name (right to left) till you are looking up the entire name again.

Looking up a name goes as follows:

1. Check registry on the current chain (Initially the Hub)
2. **A: Entry (no link) is found:**\
   ****If the current query is not yet the full name you are looking for than the name does not exist.\
   Otherwise you just found the entry that you were looking for **-> Exit**\
   **B: Link is found:**\
   ****Set current chain to where link points **-> Continue**\
   **C: No entry is found:**\
   ****Name does not exist **-> Exit**\


\=> Essentially just follow the links until you either reach the name you are looking for or a dead end\
\






