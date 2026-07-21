# The Structural Core

**Status: [DESIGN] stub, next to be developed.**

The load-bearing controls: the ones that survive a fully compromised agent because they decide on facts the agent cannot rewrite. This file will specify each. The set:

- Session-bound identity and tenant (never from agent output).
- Attenuated, signed, task-scoped tokens; child tokens cryptographically derived from and strictly weaker than parent (PDP/PEP, NIST SP 800-207).
- The bind manifest and the capability booleans (has_code_execution, has_external_send, has_production_access), which make the lethal trifecta a structural pre-run condition.
- Hard-rule vetoes evaluated over structural inputs only. No classifier participates in a veto.
- The mission capsule as a signed, non-rewritable scope object, verified at every step by an enforcement surface separate from the model.
- The external-send egress allowlist that untrusted content cannot influence.

Design discipline: if any item here is actually a classifier in disguise, the core is hollow. Each will be audited against that test.
