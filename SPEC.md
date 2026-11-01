# BrinicleID - Specification

Version: 1.0
Depends on: nothing (stack-agnostic)
Requirements: 64-bit CPU with atomic support to generate on multi-threads

## 1. Purpose

`BrinicleID` is a 32-bit identifier for events bounded to short-lived scope (a *session*). It is formed by a transient process, each ID is unique within the process lifetime (session) and becomes meaningless once it ends.

## 2. Definitions

- **Session:** A bounded execution scope within a short lifetime with a defined start time.
- **Delta:** The elapsed time since the beginning of a session, measured in units of the tick resolution.
- **Tick Resolution:** The chronometric unit used to measure elapsed time within a session.
- **Sequence:** An ordinal value, unique within the same delta tick to distinguishing IDs generated withing the same delta tick.
