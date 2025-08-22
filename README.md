# 🔐 JWT Auditor

A command-line tool for **comprehensive security auditing of JSON Web Tokens (JWTs)**.
For **ethical use only** — audit systems you are authorized to test.

## ✨ Features

* **Structural & semantic analysis**

  * Decode and pretty-print header and payload.
  * Validate temporal claims (`exp`, `nbf`, `iat`) with optional leeway.
  * Highlight missing essential claims (`iss`, `aud`, `sub`, `jti`).
  * Heuristics for excessive TTL and risky roles/scopes.

* **Cryptographic validation**

  * Supports HS256/384/512, RS256/384/512, PS256/384/512, ES256/384/512, and EdDSA.
  * Load keys from symmetric secret, PEM/DER public key, or remote JWKS.
  * JWK → key conversion with `kid` selection.

* **Vulnerability testing**

  * Attack mutations:

    * `alg=none`
    * RS→HS key confusion
    * `kid` injection (path traversal, SQLi)
    * Malicious `jku`, `x5u`, or embedded `jwk`
  * HS\* dictionary attack (built-in list or custom wordlist).

* **Endpoint exerciser (optional)**

  * Send original and mutated tokens to a target endpoint.
  * Report HTTP status, response size, and possible improper acceptance.

## 🚀 Usage

```bash
# Basic analysis
python3 jwt_auditor.py <token>

# Verify with a symmetric secret
python3 jwt_auditor.py <token> --verify --secret "mysecret"

# Verify with a public key
python3 jwt_auditor.py <token> --verify --pubkey public.pem

# Test with JWKS
python3 jwt_auditor.py <token> --verify --jwks https://example.com/jwks.json

# Generate attack mutations
python3 jwt_auditor.py <token> --mutate --out mutations/

# Exercise endpoint with a token
python3 jwt_auditor.py <token> --target https://api.example.com/protected
```

Do you want me to also make a **short example output section** (showing how the audit report looks in the terminal), so the README feels more practical?
