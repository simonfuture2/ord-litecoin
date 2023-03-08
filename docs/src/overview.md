Ordinal Theory Overview
=======================

Ordinals are a numbering scheme for litoshis that allows tracking and
transferring individual lites. These numbers are called [ordinal
numbers](https://ordinals.com). Litoshis are numbered in the order in which
they're mined, and transferred from transaction inputs to transaction outputs
first-in-first-out. Both the numbering scheme and the transfer scheme rely on
*order*, the numbering scheme on the *order* in which litoshis are mined, and
the transfer scheme on the *order* of transaction inputs and outputs. Thus the
name, *ordinals*.

Technical details are available in [the
BIP](https://github.com/casey/ord/blob/master/bip.mediawiki).

Ordinal theory does not require a separate token, another blockchain, or any
changes to Litecoin. It works right now.

Ordinal numbers have a few different representations:

- *Integer notation*:
  [`2099994106992659`](https://ordinals.com/sat/2099994106992659) The
  ordinal number, assigned according to the order in which the litoshi was
  mined.

- *Decimal notation*:
  [`3891094.16797`](https://ordinals.com/sat/3891094.16797) The first
  number is the block height in which the satoshi was mined, the second the
  offset of the litoshi within the block.

- *Degree notation*:
  [`3°111094′214″16797‴`](https://ordinals.com/sat/3%C2%B0111094%E2%80%B2214%E2%80%B316797%E2%80%B4).
  We'll get to that in a moment.

- *Percentile notation*:
  [`99.99971949060254%`](https://ordinals.com/sat/99.99971949060254%25) .
  The litoshi's position in Litecoin's supply, expressed as a percentage.

- *Name*: [`satoshi`](https://ordinals.com/sat/satoshi). An encoding of the
  ordinal number using the characters `a` through `z`.

Arbitrary assets, such as NFTs, security tokens, accounts, or stablecoins can
be attached to satoshis using ordinal numbers as stable identifiers.

Ordinals is an open-source project, developed [on
GitHub](https://github.com/casey/ord). The project consists of a BIP describing
the ordinal scheme, an index that communicates with a Bitcoin Core node to
track the location of all satoshis, a wallet that allows making ordinal-aware
transactions, a block explorer for interactive exploration of the blockchain,
functionality for inscribing satoshis with digital artifacts, and this manual.

Rarity
------

Humans are collectors, and since satoshis can now be tracked and transferred,
people will naturally want to collect them. Ordinal theorists can decide for
themselves which sats are rare and desirable, but there are some hints…

Litecoin has periodic events, some frequent, some more uncommon, and these
naturally lend themselves to a system of rarity. These periodic events are:

**Blocks: In Litecoin, new blocks are added to the blockchain roughly every 2.5 minutes. 
    The creation of new blocks is what allows transactions to be confirmed and added to the blockchain.

**Difficulty adjustments: Difficulty adjustments occur every 2016 blocks in Litecoin. 
    This is done to ensure that blocks are created at a consistent rate and to maintain the security of the network.

**Halvings: Litecoin, like Bitcoin, has a fixed supply of coins. Every 840,000 blocks, 
    the block reward for miners is reduced by half. This is known as a "halving" event. 
    The most recent halving in Litecoin occurred on August 5th, 2019, and the next one is expected to occur in August 2023.

**Cycles: Litecoin, like many other cryptocurrencies, experiences cycles of 
    price increases and decreases. These cycles are influenced by a variety of factors, 
    including market demand, adoption, and regulatory developments.

In terms of rarity, the halving events can be considered the most rare, 
as they occur only once every 840,000 blocks. 

The other events occur more frequently, with blocks being added every 
few minutes and difficulty adjustments occurring every 2016 blocks. 

However, all of these events are important for the functioning and security of the Litecoin network.

This gives us the following rarity levels:

- `common`: Any sat that is not the first sat of its block
- `uncommon`: The first sat of each block
- `rare`: The first sat of each difficulty adjustment period
- `epic`: The first sat of each halving epoch
- `legendary`: The first sat of each cycle
- `mythic`: The first sat of the genesis block

Which brings us to degree notation, which unambiguously represents an ordinal
number in a way that makes the rarity of a litoshi easy to see at a glance:

```
A°B′C″D‴
│ │ │ ╰─ Index of sat in the block
│ │ ╰─── Index of block in difficulty adjustment period
│ ╰───── Index of block in halving epoch
╰─────── Cycle, numbered starting from 0
```

Ordinal theorists often use the terms "hour", "minute", "second", and "third"
for *A*, *B*, *C*, and *D*, respectively.

Now for some examples. This litoshi is common:

```
1°1′1″1‴
│ │ │ ╰─ Not first sat in block
│ │ ╰─── Not first block in difficutly adjustment period
│ ╰───── Not first block in halving epoch
╰─────── Second cycle
```


This litoshi is uncommon:

```
1°1′1″0‴
│ │ │ ╰─ First sat in block
│ │ ╰─── Not first block in difficutly adjustment period
│ ╰───── Not first block in halving epoch
╰─────── Second cycle
```

This litoshi is rare:

```
1°1′0″0‴
│ │ │ ╰─ First sat in block
│ │ ╰─── First block in difficulty adjustment period
│ ╰───── Not the first block in halving epoch
╰─────── Second cycle
```

This litoshi is epic:

```
1°0′1″0‴
│ │ │ ╰─ First sat in block
│ │ ╰─── Not first block in difficulty adjustment period
│ ╰───── First block in halving epoch
╰─────── Second cycle
```

This litoshi is legendary:

```
1°0′0″0‴
│ │ │ ╰─ First sat in block
│ │ ╰─── First block in difficulty adjustment period
│ ╰───── First block in halving epoch
╰─────── Second cycle
```

And this litoshi is mythic:

```
0°0′0″0‴
│ │ │ ╰─ First sat in block
│ │ ╰─── First block in difficulty adjustment period
│ ╰───── First block in halving epoch
╰─────── First cycle
```

If the block offset is zero, it may be omitted. This is the uncommon litoshi
from above:

```
1°1′1″
│ │ ╰─ Not first block in difficutly adjustment period
│ ╰─── Not first block in halving epoch
╰───── Second cycle
```

Rare Litoshii Supply
-------------------

### Total Supply

- `common`: 2.1 quadrillion
- `uncommon`: 6,929,999
- `rare`: 3437
- `epic`: 32
- `legendary`: 5
- `mythic`: 1

### Current Supply

- `common`: 1.9 quadrillion
- `uncommon`: 745,855
- `rare`: 369
- `epic`: 3
- `legendary`: 0
- `mythic`: 1

At the moment, even uncommon satoshis are quite rare. As of this writing,
745,855 uncommon litoshis have been mined - one per 25.6 litecoin in
circulation.

Names
-----

Each litoshi has a name, consisting of the letters *A* through *Z*, that get
shorter the further into the future the satoshi was mined. They could start
short and get longer, but then all the good, short names would be trapped in
the unspendable genesis block.

As an example, 1905530482684727°'s name is "iaiufjszmoba". The name of the last
litoshi to be mined is "a". Every combination of 10 characters or less is out
there, or will be out there, some day.

Exotics
-------

Litoshis may be prized for reasons other than their name or rarity. This might
be due to a quality of the number itself, like having an integer square or cube
root. Or it might be due to a connection to a historical event, such as
satoshis from block 477,120, the block in which SegWit activated,
2099999997689999°, the last satoshi that will ever be mined.

Such litoshis are termed "exotic". Which litoshis are exotic and what makes
them so is subjective. Ordinal theorists are encouraged to seek out exotics
based on criteria of their own devising.

Inscriptions
------------

Litoshis can be inscribed with arbitrary content, creating Litecoin-native
digital artifacts. Inscribing is done by sending the litoshi to be inscribed in
a transaction that reveals the inscription content on-chain. This content is
then inextricably linked to that litoshi, turning it into an immutable digital
artifact that can be tracked, transferred, hoarded, bought, sold, lost, and
rediscovered.

Archaeology
-----------

A lively community of archaeologists devoted to cataloging and collecting early
NFTs has sprung up. [Here's a great summary of historical NFTs by
Chainleft.](https://mirror.xyz/chainleft.eth/MzPWRsesC9mQflxlLo-N29oF4iwCgX3lacrvaG9Kjko)

A commonly accepted cut-off for early NFTs is March 19th, 2018, the date the
first ERC-721 contract, [SU SQUARES](https://tenthousandsu.com/), was deployed
on Ethereum.

Whether or not ordinals are of interest to NFT archaeologists is an open
question! In one sense, ordinals were created in early 2022, when the Ordinals
specification was finalized. In this sense, they are not of historical
interest.

In another sense though, ordinals were in fact created by Satoshi Nakamoto in
2009 when he mined the Bitcoin genesis block. In this sense, ordinals, and
especially early ordinals, are certainly of historical interest.

Many ordinal theorists favor the latter view. This is not least because the
ordinals were independently discovered on at least two separate occasions, long
before the era of modern NFTs began.

On August 21st, 2012, Charlie Lee [posted a proposal to add proof-of-stake to
Bitcoin to the Bitocin Talk
forum](https://bitcointalk.org/index.php?topic=102355.0). This wasn't an asset
scheme, but did use the ordinal algorithm, and was implemented but never
deployed.

On October 8th, 2012, jl2012 [posted a scheme to the same
forum](https://bitcointalk.org/index.php?topic=117224.0) which uses decimal
notation and has all the important properties of ordinals. The scheme was
discussed but never implemented.

These independent inventions of ordinals indicate in some way that ordinals
were discovered, or rediscovered, and not invented. The ordinals are an
inevitability of the mathematics of Bitcoin, stemming not from their modern
documentation, but from their ancient genesis. They are the culmination of a
sequence of events set in motion with the mining of the first block, so many
years ago.
