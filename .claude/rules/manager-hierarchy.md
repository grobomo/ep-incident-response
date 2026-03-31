# Manager Hierarchy -- Span of Control

## WHY

The CCC fleet uses a strict 5-per-manager hierarchy. Overloading managers
or creating ad-hoc connections causes message loss and coordination failures.

## Rules

1. Every manager supervises exactly 5 children -- no exceptions
2. 4 tiers: Root (1) -> T1 (5) -> T2 (25) -> T3 (125) -> Workers (~500)
3. Tasks flow top-down, results flow bottom-up -- never lateral
4. No cross-tier or skip-level messaging
5. If a manager fails, its parent reassigns the 5 orphans to a replacement
