---
description: Potentially viable architectures for a cross-chain aware name system.
---

# General Architecture

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

#### Simplified Query Algorithm

1. Lookup the name on the hub chain\
   **a)** Entry is found\
   Entry is your result -> Exit\
   **b)** No entry is found\
   Name does not exist -> Exit

### Distributed Tree Architecture

This architecture mimics DNS to some degree. Data is not stored centrally but only the root node `.` as well as the tld's are on the Hub chain.\
The ownership of subdomains can be transferred to other GMP connected chains leaving the Hub chain with nothing but a reference to the other chain.

| Pros                                                                      | Cons                                                                                                      |
| ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| The average user only has to use GMP once for registering and never after | Complicated name hierarchies can result in certain actions requiring an arbitrary high amount of GMP hops |
| After moving your name you can manage it from any chain without using GMP | Name queries can require reading data from a series of blockchains                                        |

#### Simplified Query Algorithm

1. Lookup the name on the hub chain\
   **a)** Entry is found\
   Entry is your result -> Exit\
   **b)** No entry is found\
   Go up one level and check again till you find an entry, then go to 2.
2. If the name entry is a reference go to 3. otherwise the name does not exist
3. Go back to step 1 but look on the referenced chain instead of the hub. \
   Start with the full name again. Do not go further up than the name that you stopped when going up last time.

