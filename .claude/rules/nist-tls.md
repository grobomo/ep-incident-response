# NIST CSF 2.0 -- Encryption in Transit

TLS 1.2+ required for ALL connections (internal and external).
- No HTTP endpoints -- HTTPS only
- Reject any code that disables TLS verification (e.g., `verify=False`, `rejectUnauthorized: false`)
- mTLS for internal service-to-service where supported
- Block any PR that creates unencrypted endpoints
