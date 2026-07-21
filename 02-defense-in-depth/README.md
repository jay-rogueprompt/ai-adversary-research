# Defense in Depth

The support body of work: the defender's architecture that follows from the adversary analysis in the lead section. Read the adversary side first. This is what the offense implies.

## The thesis

`structural-vs-statistical.md` is the anchor. Every control on an AI system is either structural (decides from a fact the adversary cannot rewrite) or statistical (decides from a classifier and can be evaded, usually silently). A statistical control may lower risk and must generate signal, but it may never be the last thing between an adversary and an irreversible or exfiltrating action. Behind every statistical control that gates a high-impact action there must be a structural control that bounds the blast radius when the classifier is beaten.

This is also the idea that turns the kill-chains work into an argument: the "structural chokepoint" in each chain is exactly a structural control sitting where the adversary depends on something they do not own.

## What's here

- **`structural-vs-statistical.md`** the thesis. Published.
- **`structural-core.md`** the load-bearing structural controls (identity, tokens, bind manifest, egress allowlist, mission capsule). Stub.
- **`trusted-computing-base.md`** the full TCB with a compromise story per component. Stub.
- **`detection/`** detection at the interpretive level (what an artifact reveals, what is invisible), not SIEM rule specs. Stubs.
- **`frameworks.md`** honest, technique-level framework mappings. Stub.

## Discipline

Same as the lead section. Label everything ([DESIGN] here, mostly). Detection stays interpretive and CTI-flavored, not detection-engineering rule specs. No employer material.
