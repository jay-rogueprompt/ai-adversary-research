# Open Questions

This page exists on purpose. If you are evaluating whether I understand this surface, read this before you read anything else. A defender who cannot name what they have not solved has not thought hard enough about the problem.

These are the places where the architecture in this repo does not close the gap. None of them is faked shut elsewhere.

## 1. Pure-text domain harm has no structural backstop

The domain classifier (is this bio, cyber, finance) is statistical. When the harm is entirely in generated text with no tool call, no external send, and no privileged action, there is no structural control behind the classifier. The lethal-trifecta vetoes and the egress allowlist do nothing, because nothing is being sent or executed, the text itself is the harm. This is an accepted residual risk in an enterprise deployment, or it is handled out of band by content policy. I do not claim to close it structurally, because on a probabilistic text generator you cannot.

## 2. Output-encoded exfiltration to an allowlisted destination

The hardest exfiltration channel. An agent encodes sensitive data into a legitimate-looking output and sends it to a destination that is on the egress allowlist (because the destination itself is benign, the payload is the problem). Maps to ATLAS AML.T0086. The egress allowlist, which breaks most exfiltration, does not break this. The artifact is weak (an output hash that does not reveal semantic content). This is a named blind spot in forensic reconstructability, not a solved problem.

## 3. The scheduled-task risk discount is a potential side channel

A registered, pre-approved recurring task gets a lower risk treatment. Two unresolved questions make it unsafe to ship: who sets the scheduled flag and how is that verified structurally, and how does approving a *parameter range* avoid letting an attacker operate maliciously within the approved range under the discount. Until both are answered, the discount is an on-ramp, not a control.

## 4. Tuning-loop integrity

The risk thresholds are meant to be tuned over time from human override patterns. That makes the tuning path a control plane that self-modifies from human behavior, which means it is an attack surface: a patient adversary or an insider generating consistent overrides can drift the thresholds. I have not designed the integrity controls for the modification path. This is also an insider-threat problem, which is my discipline, and I have not yet written it up.

## 5. Weight-level backdoor detection is out of reach and out of scope

For an enterprise that consumes models rather than training them, detecting a trigger-activated backdoor in model weights by behavioral probing is beyond current capability. The honest control is provenance and version pinning, not detection. I do not claim backdoor detection. Any architecture that does is overclaiming.

## 6. Mission-capsule enforcement depends on infrastructure that may not exist

The signed mission capsule is only structural if there is a real enforcement surface, separate from the model, that verifies the signature at every step. In a deployment without that infrastructure, the capsule is aspirational and the control is effectively statistical. Whether a given enterprise actually has this is the difference between the architecture being structural and being a diagram.

## 7. The persistence typology is a hypothesis, not a finding

See `01-adversary/persistence-typology.md`. The mechanism-to-sophistication mapping is reasoned from traditional tradecraft analogy, not yet validated against a body of attributed agentic intrusions. It is useful for triage today. It is not established, and mechanisms can be deliberately spoofed by a sophisticated actor.

## The meta-point

Several of these break the same way: a control I would like to be structural turns out to depend on a classifier, or on infrastructure the enterprise may not have. That is the recurring failure mode of agentic AI security, and it is the whole reason this repo is organized around the structural-versus-statistical partition. The partition does not solve these. It makes them visible, which is the first honest step.
