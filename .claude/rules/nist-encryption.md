# NIST CSF 2.0 Encryption at Rest

## WHY

EP incident response handles compromised credentials and forensic artifacts.
NIST CSF 2.0 PR.DS mandates encryption at rest for all sensitive data.

## Rules

1. All stored data (logs, artifacts, configs, results) MUST use AWS KMS CMK
2. Never use AWS-managed default keys -- only Customer Managed Keys
3. KMS keys MUST have automatic annual rotation enabled
4. Use KMS GenerateDataKey for envelope encryption of bulk data
5. No plaintext secrets -- use AWS Secrets Manager or KMS encryption
