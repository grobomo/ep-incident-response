# Test Enforcement -- Dual Verification

Both worker AND manager must verify end-to-end before closing any PR.
- Worker: run full test suite, verify e2e, document evidence in PR description
- Manager: run e2e verification independently, confirm no cross-workstream breakage
- No PR merges without both worker evidence AND manager verification comment
- "It works" is not evidence -- show measured output
