<div align="center">

# Reading the AI Adversary

**Counter-adversary research and defense-in-depth for AI systems.**

How an AI system is attacked is a fingerprint for *who* attacked it.

![status](https://img.shields.io/badge/status-research_in_progress-2ea44f?style=flat-square)
![MITRE ATLAS](https://img.shields.io/badge/MITRE-ATLAS-e02f2f?style=flat-square)
![OWASP](https://img.shields.io/badge/OWASP-LLM_%26_Agentic-2f6fe0?style=flat-square)
![NIST](https://img.shields.io/badge/NIST-AI_RMF-8a8f98?style=flat-square)
![D3FEND](https://img.shields.io/badge/MITRE-D3FEND-6f4fe0?style=flat-square)

</div>

---

## The thesis

> **Attribution comes from context, not indicators. And how an adversary abused the AI is new context.**
> An IOC is cheap and disposable. What identifies an actor is the whole chain of what they did and why: they injected the agent, rode its access deeper into the environment, staged the data, moved it out. Every step is a context clue, and together they build the profile. The AI compromise is one thread in that chain. Read it in isolation, as an application-security bug, and you throw the picture away. Read it as part of the campaign, and it becomes attribution.

This is the Pyramid of Pain applied to AI: atomic indicators sit at the bottom, behavior and context at the top, and the way an adversary uses AI is a new source of high-value behavior. It is the through-line of everything here, a hypothesis staked in public and open to being wrong. Attribution was always convergence; AI tradecraft is a new axis of it.

**The defensive companion.** Every control on an AI system is either **structural** (it decides from a fact the adversary cannot rewrite: signed tokens, egress allowlists, bind manifests) or **statistical** (a classifier it can evade, and one that fails silently when it does). Statistical controls buy cost and signal. Structural controls are what hold. Reading the attack in context tells you two things at once: which controls the adversary beat, and which choices they made, which point back to who they are.

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

- The lethal trifecta: Simon Willison, 2025
- Least agency: OWASP Top 10 for Agentic Applications, 2026
- Instruction/data separation (dual-LLM; CaMeL): Willison; Google DeepMind, 2025
- PDP/PEP, deny-by-default: NIST SP 800-207
- Cyber Kill Chain and courses-of-action matrix: Lockheed Martin
- Diamond Model of Intrusion Analysis; Pyramid of Pain
- Adversary and defensive technique vocabularies: MITRE ATLAS, MITRE D3FEND
- Risk taxonomies: OWASP LLM Top 10 2025, Agentic Top 10 2026
- Governance: NIST AI RMF, Generative AI Profile (AI 600-1)

</details>

---

## `// whoami`

<<<<<<< HEAD
A cyber threat intelligence and counter-adversary operations practitioner. I led a team that detected, disrupted, and neutralized adversaries in real time inside a large regulated enterprise. Today I work in AI security at a regulated healthcare organization, and this repo is where I bring that discipline to the future of AI counter-adversary operations.

Contact and more writing: [Substack](https://substack.com/@rogueprompt) · [LinkedIn](https://www.linkedin.com/in/jayd-rogueprompt)
=======
A cyber threat intelligence and counter-adversary operations practitioner: nation-state adversary tracking, threat hunting, incident response, insider threat, CTI program leadership in a large regulated enterprise. This repo is the defender's-eye view of a surface most AI security writing approaches from the application-security side.
>>>>>>> 5c62fcb7c05165e7c1376b55c3532a91860b796d

> _All opinions are my own and do not reflect my employer._
