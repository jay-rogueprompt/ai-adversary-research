# Detection Analytics (D3FEND level 2-3)

**Status: [DESIGN] stub, high priority.**

D3FEND Detect means detection logic that fires on a described behavior, not log collection. This file will specify five behaviors fully (fields, logic, threshold, triage, reconstruction). The five:

1. External send after untrusted-content read in the same session.
2. Canary retrieval or decoy-tool invocation (near-zero false positive by construction).
3. Repeated injection-detector hits per session or per user (probing / score-oracle mapping).
4. Memory write containing instruction-shaped content, plus later cross-session recall (persistence signal).
5. MCP descriptor drift (manifest hash versus signed baseline).

Each will be written to the standard: what fields are joined, what logic fires, what threshold escalates, what an analyst does on triage, and what can be reconstructed afterward.
