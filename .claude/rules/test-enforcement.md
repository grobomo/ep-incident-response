# Test Enforcement -- Worker e2e

## WHY

Incident response code runs in a live compromised environment. Untested worker
code can miss IOCs or fail containment.

## Rules

1. Every PR modifying worker logic MUST include e2e tests
2. Worker e2e: receive task, execute, encrypt result, return to manager
3. e2e tests MUST verify KMS encryption (use localstack, not mocks)
4. No PR merges without passing worker e2e verification
