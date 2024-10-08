# 4.3 Attacks against Standardized Key Registration Protocols

Let $BadPop = (BadP, BadV)$ be the standardized key registration protocol for BMS and let the algorithms be as follows:

1. Algorithm $BadP$, on input $(pk, sk)$ sends $pk || \bm{BSign^H} (sk,〈pk〉)$
2. Algorithm $BadV$, upon receiving $(pk, π)$, runs $\bm{BVf^H} (pk,〈 pk 〉, π)$
   - replies with $pk$ if the result is $1$ and $⊥$ otherwise.

Here $H$ is the same hash function as used in $BMSign$ and $BMVf$.

We deﬁne a simple msuf-kr adversary A that successfully mounts a rogue-key attack against BMS with respect to the BadPo p registration protocol.

1. Adversary A gets the honest party’s public key $pk^∗ = g^{{sk}^*}$
2. chooses $s ← Z_p$
3. **public key** $pk = \frac {g^s} {pk^∗} = g^{s−sk^*}$
4. The forgery on any message $M$ and multiset ${pk^∗, pk}$ is simply $H(M)^s$
   1. clearly veriﬁes under the two public keys given.
5. Now to register its key, the adversary makes the query 
   1. $OMSign({pk^∗},〈 pk 〉)$, receiving $σ = H(〈pk〉)^{sk^*}$
   2. sets $π ← \frac {H(〈 pk〉)^s} {σ}$
   3. registers with $pk || π$

It is easy to see that this veriﬁes, and thus A can always output a multisignature forgery: its msuf-kr advantage is one.
