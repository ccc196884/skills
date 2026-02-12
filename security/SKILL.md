---
name: security
description: Security-aware coding patterns. Loaded when working with auth, input handling, crypto, or sensitive data.
---

# Security

## Input Validation
- Validate ALL external input (user input, API responses, file contents)
- Allowlist over blocklist — define what IS valid, not what isn't
- Validate on the server side, never trust client validation alone
- Use parameterized queries — NEVER concatenate SQL strings

## Authentication & Authorization
- Never store plaintext passwords — use bcrypt/argon2
- Use constant-time comparison for secrets (`hmac.Equal`, `crypto.timingSafeEqual`)
- Validate JWT signatures AND expiration AND issuer
- Check authorization on every request, not just at login

## Secrets Management
- Never hardcode secrets, API keys, or credentials in source code
- Use environment variables or secret managers (1Password, Vault, etc.)
- Add secret patterns to `.gitignore` (`.env`, `*.pem`, `*.key`)
- Rotate secrets on any suspected exposure

## Common Vulnerabilities
- **XSS**: Escape all user content in HTML output
- **CSRF**: Use anti-CSRF tokens for state-changing requests
- **Path traversal**: Canonicalize paths, reject `..` sequences
- **SSRF**: Allowlist outbound URLs, block internal IPs
- **Deserialization**: Never deserialize untrusted data with unsafe deserializers

## Cryptography
- Use well-known libraries — never implement your own crypto
- AES-256-GCM for symmetric encryption
- Ed25519 or P-256 for signatures
- Use cryptographically secure random: `crypto/rand`, `secrets`, not `math/rand`

## Logging & Error Messages
- Never log secrets, tokens, or passwords
- Don't expose stack traces or internal errors to end users
- Log security events (failed auth, permission denied, unusual patterns)
