# Defending AI Deployments

```console
rogue-prompt:~$ cd 90-defending-ai-deployments
```

**Supporting material.** Adversaries attacking AI systems, rather than adversaries using them.

This section reads the AI deployment as the victim: how an actor gets into an agentic system, how they persist inside it, and which controls actually hold. That is a legitimate counter-adversary problem and a different one from the research program in `01` through `04`, which is about adversary use of AI as a capability.

Sorted last on purpose. It is substrate for the main sections, and it is where the defensive implications of the offensive work get worked out.

---

## What is here

| Path | What it is | Status |
|---|---|---|
| [`persistence-typology/`](persistence-typology) | Persistence mechanism read as an actor-intent signal | parts 0 to 2 **live**, 3 and 4 stubs |
| [`kill-chains/`](kill-chains) | One chain per OWASP LLM ID, two lenses each | method and LLM01 **live** |
| [`structural-vs-statistical.md`](structural-vs-statistical.md) | The defensive thesis | **live** |
| [`defense-in-depth/`](defense-in-depth) | Structural core, trusted computing base, detection, frameworks | drafting |

---

## The partition

Every control on an AI system is either **structural** or **statistical**.

**Structural** controls decide from a fact the adversary cannot rewrite: signed tokens, egress allowlists, bind manifests. **Statistical** controls are classifiers, which can be evaded, and which fail silently when they are.

Statistical controls buy cost and signal. Structural controls are what hold.

This partition is a design principle rather than an observation, and it is what makes the section useful to an engineering team deciding what to fund.

---

## Discipline

Labels as defined in the root README. The typology and its series are `[OPEN]` on purpose: the mechanism-to-sophistication mapping is reasoned from traditional tradecraft and has not been validated against a body of attributed agentic intrusions.

Nothing here is a detection, a rule, or an operational artifact. Nothing is drawn from any employer environment.

> _All opinions are my own and do not reflect my employer._
