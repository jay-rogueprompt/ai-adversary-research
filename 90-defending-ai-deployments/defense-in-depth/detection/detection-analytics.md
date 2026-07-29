# Detection Analytics

**Status: [DESIGN] stub, high priority.**

D3FEND Detect means detection logic that fires on a described behavior, not log collection, and every analytic here is specified at technique depth rather than gestured at from tactic depth. This file will specify five behaviors fully, each written to the same standard: what fields are joined, what logic fires, what threshold escalates, what an analyst does on triage, and what can be reconstructed afterward. A detection that cannot answer all five is a dashboard, not an analytic.

The five:

1. External send after untrusted-content read in the same session. This is the lethal trifecta expressed as a detection, and the highest-value single analytic on the surface.
2. Canary retrieval or decoy-tool invocation, from the deception layer.
3. Repeated injection-detector hits per session or per user (probing, or an adversary mapping the score oracle).
4. Memory write containing instruction-shaped content, plus later cross-session recall (persistence signal, per the typology's memory-poisoning read).
5. MCP descriptor drift: manifest hash versus signed baseline.

The partition applies to detection too, and ranking the five by signal source is part of the point of this file. Analytics 1 and 5 decide over structural facts (session provenance labels, bind manifests, hashes), which makes them the highest-fidelity class: the adversary cannot rewrite the fact that fires them. Analytic 2 fires on touch of a deception asset, with the noise caveats owned in the deception layer. Analytics 3 and 4 consume classifier output, which makes them the noisiest and most evadable class, and they earn their place as trend and probing signal rather than as verdicts. A SOC that knows which of its detections sit in which class knows which alerts to trust under pressure.
