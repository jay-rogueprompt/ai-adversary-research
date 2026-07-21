# Rogue Prompt

Reading the adversaries who target AI, and building the defenses that hold when they do.

I spent years attributing attacks against enterprises and disrupting threat actor infrastructure. This is that discipline applied to AI: counter-adversary tradecraft, pointed at how large language model and agent systems are actually attacked, and at what the way they are attacked reveals about who is behind it.

## Two theses hold this together

- **Attribution is convergence, and AI TTPs are a new axis of it.** Attribution was never about a single indicator. It is infrastructure, tradecraft, tooling, and history stacked until the picture is undeniable. AI hands adversaries new tradecraft, and that tradecraft becomes another axis feeding the same method.
- **Structural beats statistical.** Every control on an AI system either decides from a fact the adversary cannot rewrite (structural: signed tokens, egress allowlists, bind manifests) or from a classifier reading language (statistical: it can be evaded, usually silently). Statistical controls raise cost and generate signal. Structural controls are what actually hold.

The first thesis leads. The second is how the defense follows from the offense.

## Status labels

Everything here is labeled, honestly.

- **[ANALYSIS]** adversary-behavior analysis grounded in public frameworks (MITRE ATLAS, OWASP, Lockheed Martin, NIST).
- **[DESIGN]** worked-through architecture. Intellectually mine, defensible, not a deployed system.
- **[OPEN] / theory-craft** a hypothesis, staked in public ahead of the case files, open to being wrong.

Nothing here is a deployed system, a weaponized artifact, or drawn from any employer environment. Public cases and general method only.

## How to navigate

```
01-reading-the-ai-adversary/   THE LEAD. The counter-adversary view of AI attacks.
   persistence-typology/       Persistence mechanism as an actor-intent signal (a series).
      00-persistence-typology.md   the anchor / lens
      01-memory-poisoning.md       deep dive 1
      02..04                       the other three mechanisms
   kill-chains/                One chain per OWASP LLM ID, two lenses each.
      README.md                    the method (courses of action + structural chokepoint)
      llm01-direct-injection.md    the first worked chain
   actor-profiling.md          threat-actor-to-AI-tooling profiling (public actors)

02-defense-in-depth/           SUPPORT. The defender's architecture.
   structural-vs-statistical.md    the thesis
   structural-core.md, trusted-computing-base.md, detection/, frameworks.md

open-questions.md              What is unsolved. Read this to judge whether I know where the hard parts are.
```

Start with `01-reading-the-ai-adversary/`. The defense section exists to show what the offense implies, not the other way around.

## Attribution (prior art, named)

- The lethal trifecta: Simon Willison, 2025.
- Least agency: OWASP Top 10 for Agentic Applications, 2026.
- Instruction/data separation (dual-LLM; CaMeL): Simon Willison; Google DeepMind, 2025.
- PDP/PEP, deny-by-default: NIST SP 800-207.
- Cyber Kill Chain and courses-of-action matrix: Lockheed Martin.
- Diamond Model of Intrusion Analysis; Pyramid of Pain.
- Adversary and defensive technique vocabularies: MITRE ATLAS, MITRE D3FEND.
- Risk taxonomies: OWASP Top 10 for LLM Applications 2025 and Agentic Applications 2026.
- Governance: NIST AI RMF and the Generative AI Profile (AI 600-1).

## Who

A cyber threat intelligence and counter-adversary practitioner: Navy, then CTI, then years hunting nation-state APTs, ransomware crews, and organized threat actors. Led CTI teams, contributed to the Verizon DBIR and two CISA #StopRansomware advisories. This is the discipline I came from, pointed at the surface everyone else is arriving at from application security.

Published as Rogue Prompt. All opinions are my own and do not reflect my employer.
