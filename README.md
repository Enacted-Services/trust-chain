# Enacted Services Trust Chain

This repository contains the public cryptographic materials for Enacted Services and the necessary
tools and background information to evaluate its trust chain.

In the event of a compromise, you will see a red message below explaining the situation and
providing instructions on how to proceed. Otherwise, you will see a purple message that 
indicates that the materials are valid and trusted.

> [!IMPORTANT]  
> No known compromises have occurred. This message **IS NOT** a substitute for your own due diligence.

## OpSec Overview

All cryptographic materials were generated offline using the instructions and scripts found at
[jhatler/YubiKey-Guide](https://github.com/jhatler/YubiKey-Guide).

Key materials are kept encrypted at rest at all times, possibly through the use of hardware tokens.
All decryption operations on these materials requires at least two factors (what you have and what
you know).

Techniques have been employed to ensure that the most sensitive materials (e.g. Root CA) are not
needed for day-to-day operations. In situations where they are needed, they are decrypted in memory
on an air-gapped system and used only for the duration of those operations.

Day-to-day operations are exclusively performed using hardware tokens. These tokens are protected
by a PIN and are configured to require a touch to perform any cryptographic operations. The tokens
are also configured to require a touch after a short period of inactivity (where possible).

Hardware tokens are stored securely when not in use. Only hardware tokens which support biometric
authentication are permitted for use with these materials. A audit of the tokens is performed
regularly and their management keys are rotated periodically. Tokens which have been lost, stolen,
or reconfigured are considered irreversibly compromised and their materials are revoked. Tokens
which are to be decommissioned are securely wiped and destroyed by at least two trusted parties
to ensure that no one party can compromise the materials.

To safeguard against the loss of these materials, they are backed up in multiple, secure,
geographically-distributed locations. These backups are themselves encrypted and the keys have been
sharded to ensure only a quorum of trusted parties can access them. Each key shard is encrypted
by its owner using the combination of a [one-time pad](https://en.wikipedia.org/wiki/One-time_pad)
(shared among the trusted parties) and a [book cipher](https://en.wikipedia.org/wiki/Book_cipher)
(the book is known only to the owner). These physical materials and digital media are further
protected by tamper-evident seals and stringently documented chains of custody. When a party is
no longer trusted, their key shard is destroyed and the quorum reinitialized by the remaining
parties.

For ecosystems that support it, revocation certificates have been pregenerated and are also stored
in the same manner as the key materials. In the event of a compromise, these certificates can be
immediately published to revoke the compromised materials.

Only the trusted parties are permitted to commit changes to this repository. Each commit updates
the `SHA512SUMS` file with the SHA512 hashes of the files in the repository. The `SHA512SUMS` file
is signed by the party updating the repository using an SMIME certificate which has been issued by
a public CA and which required verification of a government-issued ID to obtain. Each commit must
also be signed by the trusted party's GPG key and they must have vigilant mode enabled on their
GitHub account. These details are verified by the other trusted parties before new parties are
added to the repository, and are audited regularly thereafter.
