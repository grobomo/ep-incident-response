# EP Incident Response -- CCC Fleet Operations

## Context
EP Entertainment Partners critical incident response. Jenkins infrastructure compromise.
Legato MSP coordinating. Trend Micro MDR provider.

## CCC Fleet Architecture

Hierarchical fleet of 500 workers organized in 4 tiers with strict 5-children-per-manager limits.

```
T1 Director (1)
  |-- T2 Managers (5)
       |-- T3 Managers (25)
            |-- Workers (500, distributed across T3 managers)
```

### Tier Roles

| Tier | Role | Count | Responsibility |
|------|------|-------|---------------|
| T1 | Director | 1 | Overall coordination, NIST compliance, customer comms |
| T2 | Division Managers | 5 | Workstream ownership (contain, eradicate, recover, monitor, report) |
| T3 | Team Managers | 25 | Direct worker supervision, PR review, quality gates |
| Workers | Execution | 500 | Individual tasks, code changes, analysis, remediation |

### Hierarchy Rules
- **Max 5 children per manager** -- no exceptions
- T3 managers each supervise up to 20 workers
- T2 managers each supervise 5 T3 managers
- T1 director supervises 5 T2 managers
- Every worker reports to exactly one T3 manager
- Every PR requires manager sign-off before merge

## NIST CSF 2.0 Encryption Requirements

All customer data handling follows NIST Cybersecurity Framework 2.0.

### At Rest
- All customer data encrypted with AWS KMS Customer Managed Keys (CMK)
- S3 buckets: SSE-KMS with dedicated CMK per workstream
- EBS volumes: KMS-encrypted
- RDS/DynamoDB: KMS-encrypted
- No plaintext customer data in logs, task files, or PR descriptions

### In Transit
- TLS 1.2+ required for all connections
- No HTTP -- HTTPS only
- Internal service-to-service: mTLS where supported
- VPN for any direct customer network access

### Key Management
- CMK rotation: automatic annual rotation enabled
- Key policies: least-privilege per workstream
- No key material exported or hardcoded
- CloudTrail logging for all KMS API calls

## Workstreams

| ID | Name | T2 Owner | Focus |
|----|------|----------|-------|
| WS1 | Containment | T2-1 | Isolate compromised Jenkins, network segmentation |
| WS2 | Eradication | T2-2 | Remove threat actor artifacts, patch vulnerabilities |
| WS3 | Recovery | T2-3 | Rebuild Jenkins, restore services, validate integrity |
| WS4 | Monitoring | T2-4 | Deploy detection rules, continuous threat hunting |
| WS5 | Reporting | T2-5 | Timeline, evidence preservation, customer deliverables |

## Code Standards

- Every change on a feature branch, never commit to main
- One focused task per PR
- Both worker AND manager must verify e2e before closing PR
- All secrets via AWS Secrets Manager or KMS -- never in code
- Task files in `.claude-tasks/` directory
