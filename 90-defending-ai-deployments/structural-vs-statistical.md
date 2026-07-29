# The Structural versus Statistical Partition

**Status: [DESIGN].** The organizing principle of this repository. The narrative version of this argument is published as an essay; this is the reference version.

## The root principle

You cannot get a deterministic security guarantee out of a probabilistic component. The problem is not sampling noise, and pinning temperature to zero does not fix it. A learned model's decision boundary cannot be enumerated, verified, or exhaustively tested, and the adversary, not the defender, chooses the input. A component whose behavior on adversarial input is unknowable cannot be the thing that reliably enforces a binary policy. This is not a defect to be patched. It is the nature of learned statistical inference, and every design decision in this repository is a response to it.

## The partition

Sort every control by where its decision comes from.

**Structural controls** decide from a fact that exists independently of any model output:

- a cryptographically signed token, and what scope it does or does not contain
- a tenant or user identity bound to the authenticated session
- a registry entry (model, tool, MCP server, safety profile)
- a bind manifest: what tools are actually attached to this session
- a deployment-stage or configuration value
- a hash or signature match

These survive an adversary who fully controls the agent's reasoning, because the fact is not something the agent can rewrite by being manipulated.

**Statistical controls** decide from a classifier reading natural language:

- injection detection
- domain classification (bio, cyber, finance)
- reversibility and external-impact scoring
- memory-write poisoning detection
- PII and sensitive-data detection

These fail when the adversary shapes input to evade the classifier. The critical property is that they usually fail *silently*: evasion produces no event, so the defender does not learn the control was beaten.

## The rule

A statistical control may lower risk and must generate detection signal. It may never be the last thing standing between an adversary and an irreversible or exfiltrating action.

Behind every statistical control that gates a high-impact action there must be a structural control that bounds the blast radius when the classifier is beaten. Where no such structural backstop exists, the architecture must say so, and the residual risk is accepted explicitly rather than hidden behind a classifier.

## Applying the rule (worked examples)

For each statistical control, ask two questions: what happens when it is evaded, and does anything structural catch it.

- **Injection detection.** Evaded by novel phrasing, encoding, cross-chunk splitting. When evaded, the injected instruction reaches the model. **Backstop:** the external-send egress allowlist and the bind-manifest vetoes. The injection can steer the model but cannot convert into exfiltration (sends only reach allowlisted destinations) or privileged execution (an untrusted-content session does not also hold code-exec-plus-production). This is the good case: the classifier fails, and structure bounds the failure.
- **Domain classifier.** Evaded by obfuscated phrasing. When evaded, the domain risk floor never engages. **Backstop:** partial to none. If the harm needs a tool or a send, structure still bounds it. If the harm is pure generated text, nothing structural catches it. Named residual risk.
- **Reversibility classifier.** Evaded by a plan that composes into an irreversible effect. **Backstop:** map irreversibility to tool tier and destination (structural) wherever possible, so "irreversible" is expressed as "touches this tool, this destination, this stage" rather than as a plan-reading judgment. Genuinely novel compositions remain residual.
- **Memory-write poisoning detection.** Evaded by instruction-as-preference or slow drip. **Backstop:** memory provenance, plus a rule that recalled memory carries a trust label into the next turn, so poisoned memory is read as untrusted content and cannot satisfy the trusted-instruction path. This converts a silent statistical failure into a bounded one, but only if the memory read path is structurally labeled.
- **PII and sensitive-data detection.** Evaded by novel formats. **Backstop:** at ingestion, the conservative default (untagged data inherits the highest co-occurring sensitivity) is structural. At output, mostly none, which is why the egress allowlist matters more than the redactor.

## The consequence for the whole architecture

The real guarantees of this architecture come from six or seven structural facts, not from the classifiers. The classifiers are worth deploying, but their highest value is not blocking, it is feeding detection. That reframing is the difference between an architecture that looks defended and one that is, and it comes from the defender's discipline rather than the engineer's.

The first job when auditing any agentic AI deployment: label every control structural or statistical, and find every place a statistical control is being trusted as if it were structural. Those places are where the architecture breaks, and they are predictable.
