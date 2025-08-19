# Mini Ledger Solana

## 📌 Solution Abstract
This is a list of mini-implementations of a "Solana-like" ledger.
It demonstrates the key ideas of Solana on a minimal set of primitives:

- **PoH (Proof of History)** as monotonic sha256 "ticks" collected in **Entry** and grouped in **Slot**.
- **Leader mode**: generates PoH, accepts signed transactions, buffers them in entries and produces a log `/ledger`.
- **Validator mode**: accepts foreign slots via `/ingest`, recalculates PoH, verifies signatures and *replays* transactions to a local bank, converging with the leader state.
- **Anti-replay** by signature and `recent_hash` window to protect against "stale" transactions.

Suitable for **TDD/demo/study**, and as a skeleton mini-sandbox based on Solana design.

---

## 🎯 Why this
- **Touch with your hands**: how PoH turns time into data, and data into a reproducible log.
- **See the separation of roles**: the leader writes history, the validator reproduces without trusting the source.
- **Understand the two protections** at the "entry" of a transaction: the freshness of `recent_hash` and the prohibition of replaying a signature (*anti-replay*).

## List of implementations:
- [Python FastAPI](https://github.com/rustkas/mini-ledger-solana-python)

## Why "mini-implementation"

- No distributed consensus (Tower BFT, Vote accounts).
- No P2P network, only HTTP endpoints.
- No sharding by accounts, no parallel runtime.
- Only one transaction type is supported: transfer.
- Slots are fixed by ticks, without time dynamics (~400ms in real Solana).

That is, this is not real Solana, but a "minimal skeleton" that is enough to demonstrate the PoH mechanics, leader/validator work and replay logic.
