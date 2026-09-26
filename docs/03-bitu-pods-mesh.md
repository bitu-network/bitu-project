# file: docs/03-bitu-pods-mesh.md
# BITU Pods and Mesh: The Machine That Makes BIOU Tangible

**Draft article — the first practical use case and implementation layer**

## Why build a machine around BIOU?

A transferable-debt protocol is an abstract idea.

BITU deliberately pairs that idea with a physical and immediately understandable machine: a **pod** that carries its own cryptographic identity and can participate in a peer-to-peer network wherever it is connected.

The purpose of the pod and mesh is not to replace the BIOU concept. They are the mechanism that turns the concept into something people can actually run, observe, and use.

The intended progression is:

> **portable identity → reachable peer → trusted debt relationship → transferable BIOU**

## A pod is an identity that can move

A pod is a mounted volume used as the persistent home of a BITU identity.

The pod generates an Ed25519 keypair. Its public key is the identity other nodes use to refer to it, while its private key remains protected on the device.

The important property is portability.

The identity is not tied to:

- an IP address;
- a MAC address;
- a particular computer;
- a particular Wi-Fi network.

The pod can move to another compatible machine and continue to represent the same public-key identity.

The practical expectation is that most people will use one pod as one identity. Multiple pods can still exist, including for privacy reasons, without requiring the system to expose a higher-level cluster identity.

## The router is plumbing, not identity

A machine may host multiple pods.

BITU therefore uses a machine-level router rather than requiring every pod to own a completely separate networking stack.

The router itself has no independent identity. It acts as plumbing between the network and the identities of the pods it hosts.

When a request is addressed to a particular public key, the appropriate local pod can prove control of that identity by signing with its private key.

This separation allows one computer to host several independent BITU identities without turning the computer itself into the identity.

## Discovery by proof, not by address

IP addresses and MAC addresses are useful for reaching a machine, but they are poor persistent identities.

BITU therefore treats addresses as temporary **reachability hints**.

A node can broadcast a challenge containing a random nonce. A node that controls the requested private key signs the nonce and responds. The challenger verifies the signature against the claimed public key before accepting the address as a reachable endpoint for that identity.

The same principle can authenticate delivered messages: the sender signs the message, and the recipient verifies the signature against the sender's public key.

The rule is simple:

> **Addresses tell you where a key may currently be reachable. The key tells you who you are talking to.**

## Store-and-forward

A peer does not need to be online at the exact moment another participant wants to send it a message.

The router can keep a small outbound queue for an unreachable peer and send the message after that peer is discovered and cryptographically verified again.

This is basic store-and-forward behavior, but it matters for BITU because the economic protocol depends on participant identities remaining recognizable even when their network attachment changes.

## Moving beyond one LAN

The current implementation model begins with ordinary LAN/WLAN connectivity. The broader vision is to use existing networks as transport while keeping identity and trust centered on public keys.

One proposed extension is WLAN hopping: a machine that can access multiple nearby networks can periodically move between them and refresh the set of identities it can currently reach.

Another is internet bridging: a node that has both mesh reachability and conventional internet access could relay information between otherwise disconnected WLAN clusters.

These are transport techniques, not the economic idea itself. They exist to make the key-centric network usable across the infrastructure people already have.

## Storage is a secondary feature, not the core invention

The physical nature of the pod makes storage an obvious BITU feature.

Data can move between participants, and nodes can choose to provide durable storage for other participants. A storage provider can periodically answer randomly selected challenges derived from stored data, with successful answers producing BIOU credit.

This creates a direct connection between useful storage activity and the debt network.

But storage should not be confused with the central idea of BITU.

The deeper primitive is transferable debt. Storage is an early, concrete use case that demonstrates why a user-controlled, persistent network identity can be valuable.

## Why the pod matters economically

The pod is not merely a convenient place to store a private key.

It makes the economic participant portable.

A person can move the pod from one computer or network to another without changing the identity that other participants recognize. That gives debt relationships continuity across changes in physical connectivity.

The network can therefore treat the public key as the persistent participant while treating machines, addresses, and WLANs as changing transport conditions around it.

## Why a physical machine helps explain the protocol

BIOU is easier to understand when there is a visible machine doing something with it.

A person can plug in a pod, discover another identity, transfer data, watch a signed relationship change, and see the same identity remain meaningful after the pod moves to another machine.

That is intentionally part of the design strategy: instead of asking users to become interested in an abstract monetary protocol first, give them a useful machine and let the underlying BIOU mechanism reveal itself through use.

## Implementation-specific choices

The current implementation includes choices that are practical rather than fundamental to BIOU itself, including:

- Windows-based pod storage;
- DPAPI protection for the private key;
- a machine-level router;
- in-memory routing tables rebuilt after restart;
- LAN discovery through challenge/response;
- per-peer outbound queues;
- loopback-based testing of multiple local pods.

These choices may change without changing the underlying BIOU concept.

Likewise, several mesh extensions remain open design work, including reliable WLAN hopping schedules, internet NAT traversal, and the persistence strategy for routing hints.

## The role of the machine layer

The machine layer can be summarized as follows:

> **The pod gives the participant a portable identity. The mesh makes that identity reachable. BIOU gives the reachable identity an economic relationship with other identities.**

That is why the pod and mesh belong in the BITU project, but they should not be mistaken for the conceptual center of the system.
