# The Trusted Computing Base

**Status: [DESIGN] stub.**

The structural guarantees are only as good as the components that anchor them. This file will give each TCB component a compromise story: what an adversary gains by owning it. The full set:

- Context-assembly and signing layer (holds the signing key). Compromise: forge any risk input or Mission Manifest. The crown jewel.
- Policy decision point and policy store. Compromise: rewrite vetoes and thresholds.
- Identity provider and its role-update channel. Compromise: forge roles and tenants at the source. (Account-risk and velocity signals are deliberately sourced downstream, so IdP compromise degrades rather than passing silently.)
- Registries (model, tool and MCP, safety profile, scheduled task). Compromise: a poisoned entry is trusted structurally.
- Token issuance and attenuation service. Compromise: delegation attenuation becomes a lie.
- Bind-manifest mechanism. Compromise: the capability booleans no longer reflect reality.
- Audit and log pipeline. Compromise: detection and forensics go dark or get poisoned.
- Upstream classifiers, in a weaker TCB sense. Compromise removes signal and cost, but does not forge facts.

The honest reduction: the security of the whole architecture reduces to the integrity of the signing layer, the registries, and the token service. Harden those three first.
