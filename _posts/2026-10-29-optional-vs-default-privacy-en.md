---
layout: post
title: "Money Used to Forget: Optional Privacy, Default Privacy, and the Accident of Surveillance"
date: 2026-10-29 13:00:00 +0000
categories: [cryptocurrency, proof-of-work, privacy]
lang: en
---

For almost the entire history of money, money had amnesia. A cowrie shell, a gold solidus, a silver thaler, a crumpled banknote — none of them carried a memory of where they had been or whose hands they had passed through. You accepted them not because you could inspect their history, but because you couldn't. The value was in the object, not in the biography of the object. It is only in the last fifty years — a rounding error in five thousand years of money — that we built currencies that remember everything. The debate between optional privacy and default privacy in crypto, between Litecoin and Zcash on one side and Monero, Zano, and ZKas on the other, is really a debate about whether that amnesia was a bug we fixed or a feature we carelessly threw away.

---

**The long default.** Cash is a bearer instrument, and bearer instruments are the original privacy technology. Settlement happens at the moment of handover, with no third party in the room, no ledger updated, no record created. Two properties follow that we rarely name until they are gone. The first is fungibility: one coin is exactly as good as another, because there is no way to rank them by ancestry. The second is permissionlessness: nobody can decline your money because of who you are or what you once bought. Even early account-based money kept much of this spirit. Banks kept ledgers, but bank secrecy was a point of professional pride, sometimes enshrined in law. Your banker knew your business; the world did not.

The monitored monetary system is a digital-age construction. SWIFT began wiring bank messages in the 1970s, card networks turned every purchase into a data point, and anti-money-laundering regimes gradually converted payment processors into deputized observers. Then Bitcoin arrived in 2009 with a strange new compromise: pseudonymous addresses floating above a radically public ledger. Satoshi's privacy advice — keep your public keys anonymous — held for about as long as it took for chain analysis to become an industry. A Bitcoin transaction is private the way a masked man walking through a crowd of camera drones is private.

---

**The honest case for the glass ledger.** Traceability is not nothing, and privacy advocates do themselves no favors by pretending otherwise. When the FBI recovered most of the Colonial Pipeline ransom in 2021, it did so by following Bitcoin through the very ledger its critics call a surveillance machine. Stolen funds can be followed, sanctions can be enforced, and an exchange can prove — at least in principle — that the money it claims to hold actually exists. Our earlier Zano articles circled the same asymmetry from the technical side: a transparent chain lets anyone audit the money supply just by looking, while a privacy chain has to prove its integrity with cryptography, and when that proof has a hole, nobody can see the counterfeit piling up. Transparency is a genuine public good. The question is who gets to use it, and at what price to everyone else.

---

**The price of being watched.** The problem with financial surveillance is not that good people might watch; it is that the infrastructure of watching does not come with a guarantee about who holds it. A database of everyone's transactions is a honeypot, and honeypots get breached — the same banks and processors trusted to monitor money routinely fail to protect the data they collect. Worse, monitoring is not a cost center; it is a business model. Payment data feeds advertising, credit scoring, and trading strategies. And wherever someone sits close enough to the flow to see it before the public does, you get the oldest crime in finance wearing new clothes: informational asymmetry, front-running, insider advantage. A fully visible mempool of human economic life hands an edge to whoever owns the best vantage point, and that vantage point is never evenly distributed.

There is also a quieter casualty: fungibility. Once coins carry legible histories, they can be ranked, tainted, and blacklisted. An address that once touched a sanctioned mixer makes its outputs persona non grata at an exchange, and suddenly one bitcoin is no longer one bitcoin. We reinvented the problem that cash solved millennia ago — money that must be inspected before it can be accepted — and called it progress.

---

**Optional versus default: the anonymity set is the whole argument.** This is where Litecoin's MWEB and Zcash's shielded pool diverge from Monero, Zano, and ZKas, and it matters less cryptographically than socially. Optional privacy sounds like the reasonable compromise: transparent when you want, private when you need. In practice, privacy you must opt into is privacy most people never use, and the few who do stand out. For most of Zcash's life, only a minority of transactions touched the shielded pool, which means the shielded few were hiding in a crowd of their own choosing — a small crowd. Every opt-in private transaction is also a public statement: *this one, look here, someone wanted secrecy.* Optional privacy turns discretion into evidence.

Default privacy flips the burden. On Monero, every transaction is private, so no single transaction is suspicious for being private; your purchase hides inside the entire economy's routine behavior. Zano takes the same position and extends it to staking and user-issued assets, and ZKas — as we saw when reading its code against its whitepaper — simply refuses to offer a transparent mode at all. Privacy, like herd immunity, only works when almost everyone has it. That is the strongest argument for the default-private camp, and it is not primarily an argument about criminals. It is an argument that privacy is a public good consumed collectively or not at all.

The honest cost is regulatory: default-private coins get delisted, and optional-private coins get delisted too, just more politely. If the compliance outcome is similar either way, the case for weakening the anonymity set becomes weaker still.

---

**Cash with a receipt you can choose to show.** The most interesting development is that the two camps are quietly converging on the same endpoint from opposite directions. Zcash has been pushing its wallets toward shielded-by-default, while Zano — private to the bone — offers auditable wallets, and after Hard Fork 6, Gateway Addresses: a deliberately transparent account type for exchanges and bridges, sitting on top of a chain that hides everything else. That is the Zcash model turned upside down, and it is the right way up. The goal was never a world where no one can ever see a transaction. It is a world where disclosure is a choice made by the person whose money it is — view keys for your accountant, an auditable wallet for your auditor, a gateway balance for your counterparty — rather than a standing permission granted to whoever runs the rails.

Money that forgets was not a design flaw of the ancient world; it was the load-bearing property that made money fungible, neutral, and free of gatekeepers. Surveillance money is the historical anomaly, an accident of digitization we started treating as a moral necessity. The real question is not whether privacy is legitimate — five thousand years of cash already answered that. It is who holds the switch. Default privacy with selective disclosure puts the switch in the owner's hand. Optional privacy, like the glass ledger before it, leaves it in everyone else's.
