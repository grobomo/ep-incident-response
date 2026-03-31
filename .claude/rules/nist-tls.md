# NIST CSF 2.0 Encryption in Transit

## WHY

All fleet communication crosses network boundaries. NIST CSF 2.0 requires
TLS 1.2+ for data in transit to prevent interception of incident response data.

## Rules

1. All inter-node communication MUST use TLS 1.2 or higher
2. Prefer mTLS for manager-to-worker and manager-to-manager links
3. Never disable TLS verification, even in dev/test
4. Never use TLS versions below 1.2
5. Never log decrypted credentials or forensic artifacts
