# NIST CSF 2.0 -- Encryption at Rest

All customer data MUST be encrypted at rest using AWS KMS Customer Managed Keys (CMK).
- S3: SSE-KMS with dedicated CMK per workstream
- EBS, RDS, DynamoDB: KMS-encrypted -- no exceptions
- Never store plaintext customer data in logs, task files, PR descriptions, or comments
- Block any PR that introduces unencrypted storage
