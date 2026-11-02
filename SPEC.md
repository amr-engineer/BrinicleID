# BrinicleID - Specification

Version: `1.0`

## 1. Purpose

`BrinicleID` is a 32-bit identifier for events bounded to short-lived scope (a *session*). It is formed by a transient process, each ID is unique within the process lifetime (session) and becomes meaningless once it ends.

## 2. Definitions

- **Session:** A bounded execution scope within a short lifetime with a defined start time.
- **Tick Resolution:** The chronometric unit used to measure elapsed time within a session.
- **Delta:** The elapsed time since the beginning of a session, measured in units of the tick resolution.
- **Sequence:** An ordinal value, unique within the same delta tick to distinguishing IDs generated withing the same delta tick.
- **BrinicleID:** A unique 32-bit identifier bounded to session.
- **BrinicleKey:** A 64-bit value that carries the parameters needed to generate and decode any `BrinicleID`.

## 3. Guarantees

BrinicleID is designed to provide the following properties:

- **Compact Representation:** Each identifier occupies exactly 32 bits, minimizing storage and transmission overhead.
- **Chronological Ordering:** The identifier's higher-order bits are temporal information, enabling chronological sorting within a session.
- **Monotonicity:** Identifiers generated within a session follow a non-decreasing chronological order.
- **Session-Level Uniqueness:** Every identifier generated within the same session is unique, including identifiers produced concurrently across multiple threads.
- **Deterministic Parsability:** The 64-bit `BrinicleKey` stores generator metadata, allowing `BrinicleID`s to be easily and deterministically decoded.

## 4. Non-Guarantees

`BrinicleID` intentionally does not provide the following:

- **Global Uniqueness:** Uniqueness is restricted to a single session. Identifiers generated in different sessions may overlap.
- **Cross-Session Ordering:** Identifiers from different sessions have no defined chronological relationship and must not be compared for ordering.
- **Cross-Session Stability:** An identifier has no independent meaning outside its originating session. Its interpretation depends on the associated session context.
- **Adversarial Collision Resistance:**  Identifiers are deterministic and predictable by design.

> Note: Read [README.md](README.md) for info about alternatives.
