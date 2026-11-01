# BrinicleID - Specification

Version: 1.0
Depends on: nothing (stack-agnostic)
Requirements: 64-bit CPU with atomic support to generate on multi-threads

## 1. Purpose

BrinicleID is a 32-bit identifier for events bounded to short-lived scope (a *session*). It is formed by a transient process, each ID is unique within the process lifetime and becomes meaningless once it ends.
