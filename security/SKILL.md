---
name: security
description: Security mistakes Claude introduces. Load when working with auth, crypto, user input, or secrets.
---

# Security — What Claude Gets Wrong

## Input Handling (most common vulnerability source)
- **Parameterized queries ALWAYS** — Claude sometimes concatenates SQL strings "for simplicity"
- Validate on server side — client validation is UX, not security
- Allowlist valid input, don't blocklist bad input

## Secrets
- **Never hardcode secrets** — not even "temporarily". Use env vars or secret managers.
- Claude sometimes generates example code with real-looking API keys — always use `PLACEHOLDER`
- Add `*.env`, `*.pem`, `*.key` to `.gitignore` before first commit

## Auth Mistakes Claude Makes
- Using `==` for token/password comparison → timing attack. Use constant-time comparison.
- Forgetting JWT expiration validation — always check `exp` claim
- Storing plaintext passwords — always bcrypt/argon2

## Crypto
- Never implement custom crypto — use well-known libraries
- `crypto/rand` (Go) / `secrets` (Python) / `crypto.randomBytes` (Node) — NOT math/random
