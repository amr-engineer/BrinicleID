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

## 5. Encoding

### BrinicleKey:

64-Bit Layout:

```
[ 1 size ] [ 3 version ] [ 44 timestamp ] [ 4 resolution ] [ 10 layout ] [ 1 borrow ] [ 1 reserved ]
```

```
 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111 1111
 │└┬┘ └┬───────────────────────────────────────────────────┘ └┬─┘ └─────────┬┘││
 │ │   └─ 44-bit Unix timestamp in milliseconds   Resolution ─┘  ID layout ─┘ ││
 │ └─ Key version                                              Enable Borrow ─┘│
 └─ ID size                                                          Reserved ─┘
```

resolution enum:
```
   0 0000 =   1 day |  1 0001 =   1 h   |  2 0010 =   5 min |  3 0011 =   1 min
   4 0100 =  30 sec |  5 0101 =   5 sec |  6 0110 =   1 sec |  7 0111 = 100 ms
   8 1000 =  10 ms  |  9 1001 =   1 ms  | 10 1010 = 100 µs  | 11 1011 =  10 µs
  12 1100 =   1 µs  | 13 1101 = 100 ns  | 14 1110 =  10 ns  | 15 1111 =   1 ns
```
