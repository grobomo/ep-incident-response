# EP Incident Response -- CCC Fleet Architecture

## Context

Critical incident response for EP Entertainment Partners Jenkins infrastructure compromise.
This project uses a hierarchical Claude Code (CCC) fleet to coordinate the response at scale.

## Fleet Architecture

```
                    [Root Manager]
                    /    |    \
              [Mgr1] [Mgr2] ... [Mgr5]        Tier 1: 5 managers
              / | \
         [M1a] ... [M1e]                       Tier 2: 25 managers
          / | \
     [M1a1] ... [M1a5]                         Tier 3: 125 managers
      / | \
  [W1] ... [W5]                                Tier 4: 500 workers (leaf)
```

- **500 workers** organized in a 5-per-manager hierarchy
- **4 tiers**: Root -> Tier 1 (5) -> Tier 2 (25) -> Tier 3 (125) -> Tier 4 workers (500 approx)
- Each manager supervises exactly **5 children** (managers or workers)

## Encryption -- NIST CSF 2.0

All data handling follows NIST Cybersecurity Framework 2.0 requirements:

- **At rest**: AWS KMS Customer Managed Keys (CMK) for all stored data
- **In transit**: TLS 1.2+ for all inter-node communication
- **Key rotation**: KMS automatic annual rotation enabled
- **No plaintext secrets**: All credentials via KMS envelope encryption or AWS Secrets Manager

## Communication Model

- Managers dispatch tasks downward and aggregate results upward
- Workers execute atomic incident response tasks (scan, contain, remediate, verify)
- All inter-node messages encrypted with TLS 1.2+ (mTLS preferred)
- Task results signed and encrypted at rest before storage

## Incident Response Phases (NIST)

1. **Identify** -- Asset inventory, compromise scope assessment
2. **Protect** -- Credential rotation, access revocation, network segmentation
3. **Detect** -- IOC scanning, log analysis, lateral movement detection
4. **Respond** -- Containment, eradication, evidence preservation
5. **Recover** -- Service restoration, verification, monitoring
