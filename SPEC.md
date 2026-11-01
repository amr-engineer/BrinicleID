# BrinicleID - Specification

Version: `1.0`

## 1. Purpose

`BrinicleID` is a 32-bit identifier for events bounded to short-lived scope (a *session*). It is formed by a transient process, each ID is unique within the process lifetime (session) and becomes meaningless once it ends.

## 2. Definitions

- **Session:** A bounded execution scope within a short lifetime with a defined start time.
- **Tick Resolution:** The chronometric unit used to measure elapsed time within a session.
- **Delta:** The elapsed time since the beginning of a session, measured in units of the tick resolution.
- **Sequence:** An ordinal value, unique within the same delta tick to distinguishing IDs generated withing the same delta tick.
- **BrinicleKey:** A 64-bit key to represent configurations for the ID generator.
- **BrinicleID:** A 32-bit identifier bounded to session and generated based on a `BrinicleKey`.
