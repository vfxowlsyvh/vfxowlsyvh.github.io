---
layout: post
title: "Trust, but Read the Code: zkas-rusty Against Its Own Whitepaper"
date: 2026-10-05 10:30:00 +0000
categories: [cryptocurrency, proof-of-work, zkas]
lang: en
---

A whitepaper is a promise; a repository is the truth. Last week we covered ZKas's design on paper — Orchard privacy on Kaspa's BlockDAG, a turnstile invariant, a verifiable fair launch. This week we did the less glamorous thing: cloned [zkas-rusty](https://github.com/firecash/zkas-rusty) and checked whether the code keeps the paper's promises. The short answer is that it does, with unusual honesty — and that the interesting parts are exactly where the code and the paper politely disagree.

---

**The heart is real, and it is tested.** The whitepaper's one genuinely new component — the shielded state transition riding GHOSTDAG's accepted order — lives in `shielded-core/src/state.rs`, and the file's doc comment recites the five steps from the paper almost verbatim: resolve nullifier conflicts (first wins), insert survivors, append the block's subtree to the global tree, check the turnstile, publish the anchor. Better still, the algorithm is deliberately kept *pure* — independent of rocksdb and the consensus pipeline — specifically so the "make-or-break" determinism property is unit-testable. And it is: the test suite includes a parallel-double-spend test (two blocks spending the same note; exactly one survives, every node derives the same anchor), a turnstile overspend rejection, and a multi-block fee re-minting check. The paper claimed "verified by test at the algorithm and the consensus level." That is not boilerplate. It is there.

**The genesis is checkable, byte by byte.** Everything the paper asks you to verify without trust is in `consensus/core/src/config/genesis.rs`: difficulty bits `0x1b02d093` (a real ~50 TH/s target from block one), the coinbase subsidy of `0x05f5e100` — 100,000,000 sompi, exactly 1 ZKAS — paid to a script that is a single `0x00`, OP_FALSE, provably unspendable, and the ASCII anchor `zkas-mainnet btc#959713` with the Bitcoin block hash. No premine is not a claim here; it is a constant you can grep.

**Anchors, merged mining, emission — all present.** The anchor rules (spend against a matured anchor in the `[shielded_anchor_depth, max_shielded_anchor_age]` window, whose source block must be a canonical selected-chain ancestor) are enforced in the virtual processor and exercised by a genuinely thorough test battery that isolates maturity from canonicality. Merged mining is real plumbing: an `AuxPow` type in consensus-core, dual acceptance of native and auxiliary headers, borsh-encoded through the p2p layer with round-trip tests. Emission matches too: `deflationary_phase_daa_score = 0` (decay starts at genesis, no plateau), a dev fee defined as 50 permille of each subsidy, and the three-month half-life in `coinbase.rs`. Batch Halo 2 verification is implemented in `shielded-core/src/verify.rs` via the Orchard `BatchValidator`, as advertised.

---

**Now the cons — because no honest review skips them.**

- **The repo has a previous identity.** Everything was rebranded from "FireCash," and the past keeps leaking through: the mining diagnostics file still describes "FireCash targets 10 blocks/sec," helper scripts reference `/root/firecash/wallets`, and crate names wear their history. Cosmetic, but it complicates auditing — you constantly translate between two names for the same network, and stale docs say 10 BPS where the paper says one.
- **Operational debris tells on itself.** The repo root carries `reap.py` (a script to clean up orphaned wallet-scan backups after a September 2026 restore incident), `restore_baks.py`, and a 385-line `zkas-anchor-pins.tsv` marked "OBSOLETE — DO NOT APPLY, kept for the forensic record." To their credit, they kept the forensics public rather than deleting them. But it confirms the young chain has already had at least one wallet-state incident requiring manual surgery — the whitepaper, naturally, does not mention this.
- **A self-documented performance bug.** The workspace `Cargo.toml` contains a rueful confession: when the cryptography crates were ported and renamed to `zakura-*` (orchard, halo2, pasta curves), the release-profile overrides kept the old package names and "silently stopped matching anything" — so every curve and proving crate has been compiled with overflow checks on, taxing exactly the hot arithmetic the overrides existed to speed up. The comment is admirably honest; the bug sat there burning wallet CPU for weeks. One also notes the crypto stack is a renamed fork, which severs the obvious diff against the audited upstream crates — understandable (someone had to apply the 2026 Orchard fix), but it makes independent verification harder, not easier.
- **Dead seams.** The bridge/burn machinery — peg-outs, exit receipts, an extended turnstile with `pegged_in` and `burns` terms — is written, tested, and then gated behind `BRIDGE_ENABLED = false`, with defense-in-depth guards to refuse burns even if one somehow reached the state transition. This is the right way to ship half-finished features, but it is half-finished nonetheless.

---

**The verdict.** What struck us most is the commenting culture: the code doesn't just state *what*, it argues *why* — why a negative value balance must be rejected at extraction, why the exit nullifier inherits double-spend prevention, why a profile override broke. That is the voice of engineers who expect to be audited and intend to survive it. The whitepaper's core claims — the state transition, the turnstile, the genesis, the emission — are all in the tree, faithful and tested. The gaps are in the penumbra: a renamed dependency stack that needs its own audit trail, documentation that drifts between two brand names and two block rates, and the fossil record of a mainnet that has already taken a few punches. Which is, in the end, the healthiest combination you can ask for in a three-month-old chain: a paper that tells the truth, and code that admits when it doesn't.

*Sources: [zkas-rusty on GitHub](https://github.com/firecash/zkas-rusty), [ZKas whitepaper](https://zkas.info/whitepaper.html)*
