# Framework Mappings

**Status: [ANALYSIS] stub.**

The principle for this folder: narrow, deep, and defensible beats broad and asserted. Technique-level mappings only. Tactic-only mapping is not alignment, and no alignment is asserted here that is not substantiated. Every ID is verified against atlas.mitre.org before it is cited, because vendor write-ups mislabel ATLAS IDs often enough that secondhand IDs are not citable.

This folder will hold:

- `atlas.md`: mapping to MITRE ATLAS at technique level. The anchor techniques: AI Agent Tool Invocation (AML.T0053), AI Agent Context Poisoning (AML.T0080, memory-manipulation sub-technique), Exfiltration via AI Agent Tool Invocation (AML.T0086), AI Agent Tool Poisoning (AML.T0110), and the AI Model Access tactic (AML.TA0000).
- `d3fend.md`: coverage across Model, Harden, Detect, Isolate, Deceive, Evict, stated as a graph, with the honest note that this architecture historically over-indexed Harden and Isolate and is building out Detect and Deceive.
- `owasp-agentic.md`: OWASP Top 10 for Agentic Applications 2026 (ASI01 through ASI10) as the primary spine, with the OWASP LLM Top 10 2025 for application-level concerns.
- `nist.md`: NIST AI RMF (Govern, Map, Measure, Manage) and AI 600-1, treated as process evidence produced as a byproduct, not as a cross-reference table.
