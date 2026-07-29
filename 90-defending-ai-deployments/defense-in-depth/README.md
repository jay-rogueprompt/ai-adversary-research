# Defense in Depth

The support body of work: the defender's architecture that follows from the adversary analysis in the lead section. Read the adversary side first. This is what the offense implies.

## The thesis

`structural-vs-statistical.md` is the anchor. Every control on an AI system is either structural (decides from a fact the adversary cannot rewrite) or statistical (decides from a classifier and can be evaded, usually silently). A statistical control may lower risk and must generate signal, but it may never be the last thing between an adversary and an irreversible or exfiltrating action. Behind every statistical control that gates a high-impact action there must be a structural control that bounds the blast radius when the classifier is beaten.

This is also the idea that turns the kill-chains work into an argument: the "structural chokepoint" in each chain is exactly a structural control sitting where the adversary depends on something they do not own.

## What's here

- **`structural-vs-statistical.md`** the thesis. Published.
- **`structural-core.md`** the load-bearing structural controls (identity, tokens, bind manifest, egress allowlist, Mission Manifest). Stub.
- **`trusted-computing-base.md`** the full TCB with a compromise story per component. Stub.
- **`detection/`** the detection layer: `detection-analytics.md` (the five behaviors worth firing on) and `deception-layer.md` (the assets that make an alert mean something). Stubs.
- **`frameworks.md`** honest, technique-level framework mappings. Stub.

## Discipline

Same as the lead section. Label everything (`[DESIGN]` here, mostly). No employer material.

The detection standard: each analytic is specified to the depth an analyst can act on and reconstruct from, which means naming the fields joined, the logic, the escalation threshold, the triage path, and what survives for forensics. It stops short of vendor-specific rule syntax, because the contribution here is which behaviors are worth firing on and what an artifact can ever tell you about the actor, not a portable SIEM ruleset. Detection engineering translates this; it does not replace it.
