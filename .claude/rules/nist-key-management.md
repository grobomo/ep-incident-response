# NIST CSF 2.0 -- Key Management

KMS CMK with automatic annual rotation enabled.
- Key policies scoped to least-privilege per workstream
- No key material in code, env vars, or task files
- All KMS API calls logged via CloudTrail
- Block any hardcoded encryption keys or secrets
