# Test Enforcement -- Manager e2e

## WHY

Manager orchestration failures cascade to all children. Both dispatch and
aggregation must be verified before deployment.

## Rules

1. Every PR modifying manager logic MUST include e2e tests
2. Manager e2e: dispatch to children, aggregate results, relay upward
3. e2e tests MUST assert TLS in transit and KMS encryption at rest
4. PRs touching both worker and manager MUST pass both e2e suites
5. No test shortcuts -- do not disable requirements for "emergency" fixes
