# file: docs/02-bitu-trust-and-settlement.md
# BITU: Trust-Bounded Debt Mobility

**Draft article — protocol model for BIOU settlement**

## From debt edges to a working network

BIOU provides the economic primitive: participants owe one another amounts denominated in bits.

BITU is the protocol that is intended to make those obligations **mobile, machine-processable, and constrained by trust**.

The goal is not to create a global token ledger with one universal balance. The goal is to let independent nodes recognize, transform, and settle debt states through relationships that they themselves have chosen to trust.

## Trust edges and debt edges

BITU uses two closely related concepts.

A **debt edge** describes an obligation between two identities.

A **trust edge** describes how much exposure one identity is willing to extend to another. In practical terms, a participant may say that another public key is trusted up to a certain number of bits. That limit can be changed manually or, where the implementation supports it, updated automatically from network activity.

The trust edge therefore acts as a **cap on how much debt exposure may be propagated through that relationship**.

Trust is not a statement that the other participant is universally reliable. It is a bounded willingness to let that participant participate in one's own debt graph.

## Debt mobility

Consider a chain:

> C owes B → B owes A

A and C may be strangers.

A can still obtain something from C if the protocol can transform the relevant debt states into a new, signed state that reflects the exchange.

For example, if C provides A with 20 bits worth of value, the participating nodes can re-sign their edges so that the outstanding obligations on the path are reduced accordingly.

The result is not necessarily a new permanent A–C debt edge. The value can move through the existing graph by **coordinated debt-edge reduction**.

A direct trust channel between A and C is another possible way for future exchanges to occur.

## Why participating nodes need to be online

BITU intentionally makes the participating identities active parts of settlement.

A pod controls its own private key. To participate in debt-edge mobility, the pod must therefore be available to process and sign the relevant state transitions.

This gives the network a role for always-available participants that is conceptually different from mining.

Instead of performing arbitrary work to win the right to append a global block, participating pods are expected to be available so they can:

- receive and verify signed requests;
- approve or reject debt-edge changes within their authority;
- re-sign new states when an exchange requires transitive settlement;
- relay or process information needed by trusted neighbors.

Availability can itself be rewarded in bits, through increased trust capacity, or through other participation incentives. The exact incentive mechanism remains a design space rather than a finished rule.

## There is no central debt authority

Debt edges are statements made by the participants who control the relevant keys.

Two public keys can create signed messages describing a debt edge or trust edge without asking a central issuer for permission.

What matters is whether another participant is willing to include that statement in its own trusted graph.

This means that BITU does not require a universally authoritative ledger to decide which relationships exist. Different participants can maintain different views of the world according to their own trust boundaries.

## The role of the trust horizon

A node's **trust horizon** determines which identities and debt paths it is willing to rely on.

The horizon may be constrained by graph distance. For example, a participant might accept a debt transformation that travels through a close relationship, but reject an otherwise valid chain that has propagated many hops away.

This is important because transitivity increases reach while also increasing uncertainty.

The system therefore does not try to eliminate trust. It makes trust **explicit, bounded, and local to the participant who bears the exposure**.

That also limits the usefulness of arbitrary fake identities. A public key that nobody is willing to include in a trusted path does not automatically obtain economic reach simply because it exists.

## Debt state as the object that moves

The unit being transferred is not a standalone coin.

What moves through the system is the **economic capacity represented by a set of signed debt states**.

An exchange can therefore cause several edges to change simultaneously. A value of 20 bits can be recognized at one point in the graph while reducing obligations at other points in the same path.

This is why the network can behave as though debt were transitive without requiring every participant to maintain a single global balance sheet.

## Why the system does not rely on mining

A global proof-of-work mechanism would create a shared ordering process by forcing participants to expend computational resources.

BITU takes a different approach. The system expects the identities that control debt relationships to be available to process those relationships directly.

Security and economic restraint therefore come from a combination of:

- cryptographic control of identities;
- signed debt and trust changes;
- bounded trust exposure;
- the participant's ability to stop accepting relationships it no longer trusts;
- the practical value of preserving long-earned trust relationships.

The last point is especially important. Trust is expected to be accumulated gradually and therefore to be something participants do not want to destroy casually.

## What prevents arbitrary value creation?

BITU does not attempt to impose a global maximum supply of bits.

Participants can establish new debt relationships by agreement. The relevant constraint is instead **who is willing to recognize that debt and how much exposure they are willing to accept**.

An edge that exists only between identities outside another participant's trust horizon has no automatic claim on that participant.

Likewise, if a participant considers a relationship fraudulent or excessively risky, it can stop relying on the relationship by removing it from its trusted graph.

This is an intentionally different model from a globally scarce token.

## The unresolved settlement problem

The conceptual model makes one thing clear: a transferable debt system must have authoritative state transitions at the level of the participants controlling each edge.

But the exact protocol for this is not yet specified here.

In particular, the design still needs precise rules for:

- concurrent updates to the same debt edge;
- replay of old signed states;
- conflicting signed states;
- node restarts and recovery;
- stale or temporarily disconnected participants;
- revocation and dispute handling;
- the exact conditions under which a settlement becomes final.

The intended direction is not to hide these problems behind a global mining process, but to solve them through **signed, participant-controlled state changes within bounded trust relationships**.

## The protocol thesis

BITU can therefore be summarized as:

> **A decentralized protocol in which user-controlled identities keep bounded trust relationships and participate directly in the signed state transitions that make interpersonal debt transferable through the network.**

The pod and mesh are the machinery that gives those identities a persistent, reachable form.
