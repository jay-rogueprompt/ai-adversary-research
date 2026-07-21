# Reading the AI Adversary

The lead body of work. A counter-adversary and threat-intelligence view of attacks against AI systems: who is acting, how they persist, how they run the chain, and what their choices reveal about who they are.

This is the adversary's chair. The defense-in-depth section is the same phenomena seen from the defender's chair. Red informs blue.

## The point of view

Adversary behavior drives the structure, not a list of vulnerabilities. The organizing question is the one from traditional intrusion analysis: assume the adversary knows the control exists, and ask what they do next. The mechanics on the AI surface are new. The tradecraft is not, and the analyst habits that read persistence, pivoting, and attribution in traditional intrusions read them here too.

Signature frame: **attribution is convergence, and AI TTPs are a new axis of it.** A single AI technique attributes nobody. Folded into the Diamond Model alongside infrastructure, tooling, and history, it becomes another vertex of a picture that does.

## What's here

- **`persistence-typology/`** the series. Persistence mechanism read as an actor-intent-and-sophistication signal. Anchor plus one deep dive per mechanism (memory, MCP descriptor, token/OAuth, index/embedding). `00-persistence-typology.md` is the lens; the numbered files go deep. Labeled [OPEN] hypothesis, on purpose.
- **`kill-chains/`** one chain per OWASP LLM Top 10 ID, each read with two lenses: a Lockheed Martin courses-of-action matrix (coverage) and a single structural chokepoint (priority). `README.md` is the method; `llm01-direct-injection.md` is the first worked chain and the model for the rest.
- **`actor-profiling.md`** threat-actor-to-AI-tooling profiling, public actors only. Stub.

## Discipline

- Public, already-attributed cases and general method only. Never my own environment.
- Label everything. The persistence typology and the attribution frame are hypotheses, not findings.
- Map ATLAS by technique and pin exact IDs to the current release before publishing.
- Name prior art: lethal trifecta (Willison), Diamond Model, Lockheed Martin kill chain, ATLAS.

## Series status

| Piece | Status |
|---|---|
| `persistence-typology/00-persistence-typology.md` | published (OPEN hypothesis) |
| `persistence-typology/01-memory-poisoning.md` | published (OPEN hypothesis) |
| `persistence-typology/02-mcp-descriptor-poisoning.md` | stub |
| `persistence-typology/03-token-oauth-persistence.md` | stub |
| `persistence-typology/04-index-embedding-poisoning.md` | stub |
| `kill-chains/README.md` (method) | published |
| `kill-chains/llm01-direct-injection.md` | published |
| `kill-chains/llm02..llm10` | to come, same structure |
| `actor-profiling.md` | stub |
