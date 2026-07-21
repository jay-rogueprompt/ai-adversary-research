<div align="center">

# Reading the AI Adversary

**Counter-adversary research and defense-in-depth for AI systems.**

Who attacks AI, how they persist, and what the way they do it reveals about *who they are.*

![status](https://img.shields.io/badge/status-research_in_progress-2ea44f?style=flat-square)
![MITRE ATLAS](https://img.shields.io/badge/MITRE-ATLAS-e02f2f?style=flat-square)
![OWASP](https://img.shields.io/badge/OWASP-LLM_%26_Agentic-2f6fe0?style=flat-square)
![NIST](https://img.shields.io/badge/NIST-AI_RMF-8a8f98?style=flat-square)
![D3FEND](https://img.shields.io/badge/MITRE-D3FEND-6f4fe0?style=flat-square)

</div>

---

## The two ideas this hangs on

> **Attribution is convergence, and AI TTPs are a new axis of it.**
> A single indicator attributes nobody. Folded into the Diamond Model alongside infrastructure, tooling, and history, an adversary's AI tradecraft becomes another vertex of a picture that does.

> **Structural beats statistical.**
> Every control on an AI system either decides from a fact the adversary cannot rewrite (structural: signed tokens, egress allowlists, bind manifests) or from a classifier it can evade (statistical: it fails, usually silently). Statistical controls buy cost and signal. Structural controls are what hold.

The first idea leads. The second is how the defense follows from the offense.

---

## Navigate

The adversary section is the lead. The defense section exists to show what the offense implies, not the other way around. **Start with `01`.**

| Path | What it is | Status |
|---|---|---|
| [`01 · persistence-typology/`](01-reading-the-ai-adversary/persistence-typology) | Persistence mechanism read as an actor-intent signal (a series) | anchor + memory poisoning **live**, 3 stubs |
| [`01 · kill-chains/`](01-reading-the-ai-adversary/kill-chains) | One chain per OWASP LLM ID, two lenses each | method + LLM01 **live** |
| [`01 · actor-profiling.md`](01-reading-the-ai-adversary/actor-profiling.md) | Threat-actor-to-AI-tooling profiling, public actors | stub |
| [`02 · structural-vs-statistical.md`](02-defense-in-depth/structural-vs-statistical.md) | The thesis | **live** |
| [`02 · defense-in-depth/`](02-defense-in-depth) | Structural core, trusted computing base, detection, frameworks | stubs |
| [`open-questions.md`](open-questions.md) | What is unsolved, and where I know it breaks | **live** |

---

## How to read the labels

Everything here is labeled, honestly.

- **`[ANALYSIS]`** adversary-behavior analysis grounded in public frameworks.
- **`[DESIGN]`** worked-through architecture. Mine, defensible, not a deployed system.
- **`[OPEN]`** a hypothesis, staked in public ahead of the case files, open to being wrong.

Nothing here is a deployed system, a weaponized artifact, or drawn from any employer environment. **Public cases and general method only.**

---

<details>
<summary><b>Prior art, named</b></summary>

<br>

- The lethal trifecta — Simon Willison, 2025
- Least agency — OWASP Top 10 for Agentic Applications, 2026
- Instruction/data separation (dual-LLM; CaMeL) — Willison; Google DeepMind, 2025
- PDP/PEP, deny-by-default — NIST SP 800-207
- Cyber Kill Chain and courses-of-action matrix — Lockheed Martin
- Diamond Model of Intrusion Analysis; Pyramid of Pain
- Adversary and defensive technique vocabularies — MITRE ATLAS, MITRE D3FEND
- Risk taxonomies — OWASP LLM Top 10 2025, Agentic Top 10 2026
- Governance — NIST AI RMF, Generative AI Profile (AI 600-1)

</details>

---

<div align="center">

A cyber threat intelligence and counter-adversary practitioner, pointed at the surface everyone else is arriving at from application security.

<sub>All opinions are my own and do not reflect my employer.</sub>

</div>
