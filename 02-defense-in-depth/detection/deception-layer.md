# The Deception Layer

**Status: [DESIGN] stub.**

The claim this file will develop: on the agentic AI surface, deception (D3FEND Deceive) is the cheapest high-fidelity detection available, and it is native to counter-adversary work in a way the rest of the defensive stack is not. A deception asset has no legitimate reason to be touched, so touching one is signal by construction. This is the build-out of the Deceive gap named in the framework mappings, and it is the defensive twin of the Deceive cell in the kill-chain matrices.

Three deployments:

- Canary documents seeded in the RAG index that no legitimate query should surface. Retrieval of one is a high-fidelity injection or scope-breach signal.
- Decoy credentials or a decoy tool present in some bind manifests that no legitimate task uses. Invocation is a strong signal the agent is being driven.
- A honeypot MCP server on the allowlist that does nothing real and appears in no task template. Any call is an agent being steered somewhere no workflow goes.

The caveat that has to be designed for, because the traditional claim does not import untested: on a conventional surface, only an adversary touches a deception asset, so an alert is an adversary. On this surface there is a second noise source, the model itself. Every deception asset here sits behind a probabilistic selector: a retriever can surface a canary on an oddly shaped benign query, and a planner can invoke a visible decoy tool out of ordinary confusion, with no adversary present. The fidelity claim is earned per asset, by making the canary semantically distant from the legitimate corpus and the decoy descriptor unattractive to a benign planner, and the residual noise is measured rather than assumed away. Deception on a probabilistic surface inherits some of the surface's noise. The design owns that instead of overclaiming zero.

Why it matters here: deception turns the statistical layer's noise into clean signal, and it is the one detection class whose fidelity does not depend on a classifier correctly reading adversarial content. It fires on touch, not on interpretation.
