# The Trusted Computing Base

**Status: [DESIGN] stub.**

The structural guarantees are only as good as the components that anchor them. This file will give each TCB component a compromise story. The full set:

- Context-assembly / signing layer (holds the signing key). Compromise: forge any risk input or mission capsule. Crown jewel.
- Policy decision point and policy store. Compromise: rewrite vetoes and thresholds.
- Identity provider and its role-update channel. Compromise: forge roles and tenants at the source. (Account-risk and velocity signals are deliberately sourced downstream so IdP compromise degrades rather than passes silently.)
- Registries (model, tool/MCP, safety-profile, scheduled-task). Compromise: a poisoned entry is trusted structurally.
- Token issuance / attenuation service. Compromise: delegation attenuation becomes a lie.
- Bind-manifest mechanism. Compromise: capability booleans no longer reflect reality.
- Audit / log pipeline. Compromise: detection and forensics go dark or get poisoned.
- Upstream classifiers (weaker TCB sense): compromise removes signal and cost, does not forge facts.

Honest reduction: the security of the whole architecture reduces to the integrity of the signing layer, the registries, and the token service. Harden those three first.
