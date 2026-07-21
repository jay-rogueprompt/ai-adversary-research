# LLM01 Direct Injection: The Chain Breaks at the Send, Not the Prompt

**Status: [ANALYSIS], theory-craft.** One kill chain for OWASP LLM01 (Prompt Injection), read with both lenses. A hypothesis about how the chain runs and where it collapses, staked in public and open to being wrong.

## The scenario

An attacker sends a crafted message to a customer-support chatbot that can read a private data store and send email. The message tells the model to ignore its guidelines, query the private store, and email the results out. If it lands, the outcome is data disclosure, and from there, privilege escalation and account takeover.

This is the textbook LLM01 case, and it is worth doing precisely because it is textbook. If the method does not clarify the obvious chain, it will not survive the hard ones.

## The chain, stage by stage

1. Craft payload: the attacker designs the injection.
2. Malicious message sent: "ignore previous instructions."
3. Model overrides its guidelines: the system prompt is bypassed.
4. Unauthorized data query: the private store is read.
5. Email send: the data is exfiltrated to an external address.
6. Privilege escalation: the attacker leverages the disclosure to act with more authority.
7. Outcome: data leaked (PII exposed) and account takeover.

## Lens 1: courses of action (coverage)

One interdiction per stage, using the Lockheed Martin courses-of-action verbs. ATLAS techniques are named; pin exact IDs to the current release before publishing.

| Stage | Adversary action | ATLAS technique (name) | Course of action | Control |
|---|---|---|---|---|
| Craft payload | Injection designed | LLM Prompt Injection | Deny | Authentication and rate limiting, block unauthenticated access |
| Malicious message | "Ignore previous instructions" | LLM Prompt Injection: Direct | Disrupt | Input filtering (semantic and pattern) |
| Guidelines overridden | System prompt bypassed | Jailbreak / prompt injection | Disrupt | Prompt hardening, constrain role, lock instructions |
| Unauthorized data query | Private store read | Discovery / data access | Degrade | Least privilege, scope data access to minimum |
| Email send | Exfiltration | Exfiltration via AI Agent Tool Invocation (AML.T0086) | Deceive | Human approval gate on send |
| Privilege escalation | Acts as admin | Impact | Detect | Output and action monitoring, alert on anomalous action |

That table is the coverage story: there is something to do at every stage, and defense in depth means an attacker has to beat all of them.

## Lens 2: the structural chokepoint (priority)

The matrix shows where you *can* interdict. It does not show which interdiction you would never trade away, and on this chain most of the per-stage controls are statistical. Input filtering is a classifier, so it can be evaded. Prompt hardening is a classifier, so it can be evaded. Least privilege helps but does not stop a query the model is authorized to make. The human-approval gate on the send is better, but approval fatigue makes it unreliable at volume, and a persuasive message is exactly what an injected model produces.

The one stage where the chain depends on something the adversary does not control is the send. The whole attack is an exfiltration, and exfiltration needs an outbound channel. So the chokepoint is a structural egress allowlist: the chatbot may send only to destinations approved out of band, destinations the injected content cannot set. Cut that channel and the injection can still fire, the model can still be steered, the private store can still be queried, and none of it reaches the attacker.

This is the external-communication leg of the lethal trifecta (Willison: private data, untrusted content, external communication), and it is the one leg you can cut without breaking the chatbot's real job. It beats the human-approval gate at the same stage because it decides from a fixed list, a fact the adversary cannot rewrite, instead of from a tired human reading a convincing request.

One precondition, chain collapsed. That is the difference between a matrix that says "you have options" and an argument that says "protect this first."

## Where it breaks

- If the chatbot legitimately needs to email arbitrary external addresses, the allowlist is not viable, and you fall back to the weaker approval gate plus detection. The honest version says so rather than pretending the chokepoint always exists.
- The allowlist stops exfiltration by email. It does not stop the model being steered into a harmful answer shown directly to the user, which is a different chain with no exfil leg and no clean structural chokepoint.
- Everything upstream still earns its place as cost and as detection signal. The chokepoint is not a reason to drop the other controls, it is a reason to know which one you would defend last.

## Attribution

- Courses-of-action model and kill chain: Lockheed Martin.
- Exfiltration via AI Agent Tool Invocation: MITRE ATLAS AML.T0086 (other techniques named by function; verify IDs against the current ATLAS release).
- Risk anchor: OWASP Top 10 for LLM Applications 2025, LLM01 Prompt Injection.
- The lethal trifecta: Simon Willison, 2025. The structural-versus-statistical framing: the Agentic AI Defense in Depth work.
