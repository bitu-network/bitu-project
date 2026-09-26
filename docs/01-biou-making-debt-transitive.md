# file: docs/01-biou-making-debt-transitive.md
# BIOU: Making Debt Transitive

**Draft article — conceptual foundation of BITU**

## The starting point

Most systems of money begin by introducing some thing that everyone is expected to accept: a government-issued unit, a scarce token, or another shared representation of value.

BIOU starts somewhere else.

A BIOU is a **Bits-IOU**: a statement of how much one participant owes another, denominated in **bits**. The important question is not merely how to record that debt, but how to make a debt relationship **transferable through a network of other debt relationships**.

In that sense, the central problem BIOU addresses is:

> **How can “A owes B” become useful to A when the person A wants to trade with is not B?**

The answer is to make debt **transitive**.

## Debt as a network

Consider three participants:

- B owes A 100 bits.
- C owes B 100 bits.
- A and C do not currently have a direct debt relationship.

In a conventional bilateral IOU system, A's claim on B is useful primarily against B. C's claim is useful primarily against B. The chain does not automatically become a common medium for exchange.

BIOU introduces a different possibility.

Suppose C provides A with a product or service worth 30 bits. Rather than requiring A and C to establish a permanent direct debt edge, the three parties can **re-sign and reduce their existing edges** so that:

- C owes B 70 instead of 100 bits.
- B owes A 70 instead of 100 bits.

The 30 bits of value have travelled through the network without requiring a new long-lived A–C debt edge.

This is best thought of as **transitive settlement**: a real exchange causes a coordinated state transition across a chain of trusted debt relationships.

A direct debt edge between A and C is another possible outcome. The important point is that the value does not have to remain trapped inside the original bilateral relationship.

## The native unit is the bit

In BIOU, the native unit of value is the **bit**.

The system does not require a universal conversion table saying what a product or service “really” costs in bits. Participants can decide that themselves. A broken pipe, a useful file transfer, a product, or a service can be assigned a bit value by the people participating in the exchange.

The intended connection to data is immediate: transfers that the protocol can observe and verify can automatically update debt bookkeeping. Human agreements can update the same bookkeeping for goods and services outside the data layer.

This makes bits a common accounting unit without requiring the system to pretend that every real-world thing has an objectively fixed price.

## Why this is different from a token

A token normally represents value by pointing to something outside the individual relationship: an issuer, a protocol, a reserve, a scarcity schedule, or another system-wide rule.

A BIOU instead represents a **relationship between participants**.

The value is anchored in the set of people and nodes willing to recognize, honor, and settle those relationships. A bit is therefore not intended to be a globally interchangeable object in the same sense as a conventional token. Its practical value depends on which debt relationships a participant is willing to accept.

This is the sense in which BIOU is intended to replace an arbitrary token or external authority with a **user-anchored vehicle of value**.

## Trust is what makes transitivity usable

Debt can only travel through relationships that participants are willing to rely on.

A participant therefore does not need to accept every debt edge in the world. It can define a **trust horizon**: the set of identities and debt paths it is willing to expose itself to.

The trust horizon can be limited by distance, by the amount of exposure, or by both. A debt relationship one trusted step away may be acceptable while a chain ten steps away may not be.

The purpose of this boundary is not to create a universal ranking of identities. It is to keep the consequences of accepting a debt path close to the relationships a participant actually trusts.

Trust is therefore part of the liquidity mechanism. A debt edge becomes more useful when it can participate in more acceptable paths, but extending those paths also increases the accepting participant's exposure.

## Credit can be created locally

Any two public-key identities can produce signed statements describing a debt edge or trust edge. There is no central issuer that must authorize the relationship.

Whether a third participant will include that edge in its own debt graph is a separate question. It depends on whether the relevant identities and paths fall inside that participant's trust horizon.

This allows local economic relationships to emerge without requiring a global registry of approved debt.

## The important distinction: transitivity is not global fungibility

BIOU does not need every bit in the world to be interchangeable with every other bit.

Instead, the system aims for **transferability inside a network of mutually accepted debt relationships**.

This makes the network closer to a graph of obligations than to a central pool of coins.

The important operation is therefore not “move token X from wallet A to wallet B.” It is:

> **Change several signed debt states so that an actual exchange can be recognized across an existing trust graph.**

## What is deliberately not solved here

The conceptual model does not by itself specify the complete protocol needed to implement it.

A production system still has to define, among other things:

- the exact representation and signing of a debt edge;
- how concurrent edge changes are ordered and reconciled;
- how conflicting or stale signed states are handled;
- how a node discovers an acceptable path through the trust graph;
- how limits on debt and trust are computed;
- what makes a particular settlement final.

Those are protocol questions rather than reasons to abandon the core idea.

## The core idea

BIOU can therefore be summarized in one sentence:

> **BIOU turns interpersonal debt into a transferable network primitive by allowing real exchanges to settle value across chains of mutually trusted debt relationships.**

BITU is the protocol and machine around that primitive.
