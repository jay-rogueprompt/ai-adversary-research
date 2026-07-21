# Open Questions

This page exists on purpose, and it is the right place to start. In agentic AI security, the open problems are as diagnostic as the solved ones: an architecture that cannot name its own unsolved gaps has not been stress-tested against them. Naming them is not a caveat to the work. It is part of the work.

These are the places where the architecture in this repo does not close the gap. None of them is quietly closed somewhere else in the repo.

## 1. Pure-text domain harm has no structural backstop

The domain classifier (is this bio, cyber, finance) is statistical. When the harm lives entirely in generated text, with no tool call, no external send, and no privileged action, there is no structural control standing behind it. The lethal-trifecta vetoes and the egress allowlist do nothing here, because nothing is being sent or executed: the text itself is the harm. In an enterprise deployment this is either an accepted residual risk or it is handled out of band by content policy. I do not claim to close it structurally, because on a probabilistic text generator you cannot.

## 2. Output-encoded exfiltration to an allowlisted destination

The hardest exfiltration channel. An agent encodes sensitive data into legitimate-looking output and sends it to a destination on the egress allowlist: the destination is benign, the payload is the problem. Maps to ATLAS AML.T0086. The egress allowlist, which breaks most exfiltration, does not break this. The forensic artifact is weak (an output hash proves something left without revealing what it meant). This is a named blind spot in forensic reconstructability, not a solved problem.

## 3. The scheduled-task risk discount is a potential side channel

A registered, pre-approved recurring task receives a lower risk treatment. Two unresolved questions make it unsafe to ship. First, who sets the scheduled flag, and how is that verified structurally rather than taken on trust. Second, how does approving a parameter range avoid handing an attacker the discount while they operate maliciously inside the approved range. Until both are answered, the discount is an on-ramp, not a control.

## 4. Tuning-loop integrity

The risk thresholds are meant to be tuned over time from human override patterns. That makes the tuning path a control plane that modifies itself from human behavior, which makes it an attack surface: a patient adversary, or an insider generating consistent overrides, can drift the thresholds. I have not designed the integrity controls for that modification path. This is also an insider-threat problem, which is my discipline, and I have not yet written it up.

## 5. Weight-level backdoor detection is out of reach and out of scope

For an enterprise that consumes models rather than training them, detecting a trigger-activated backdoor in model weights through behavioral probing is beyond current capability. The honest control is provenance and version pinning, not detection. I do not claim backdoor detection here, and I treat detection claims elsewhere as ahead of the research until proven otherwise.

## 6. Mission Manifest enforcement depends on infrastructure that may not exist

The signed Mission Manifest is only structural if there is a real enforcement surface, separate from the model, that verifies the signature at every step. In a deployment without that infrastructure, the manifest is aspirational and the control is effectively statistical. Whether a given enterprise actually has that surface is the difference between this architecture being structural and being a diagram.

## 7. The persistence typology is a hypothesis, not a finding

See `01-reading-the-ai-adversary/persistence-typology/`. The mechanism-to-sophistication mapping is reasoned by analogy from traditional tradecraft, not yet validated against a body of attributed agentic intrusions. It is useful for triage today. It is not established, and a sophisticated actor can deliberately spoof the mechanisms.

## The meta-point

Several of these break the same way: a control I would like to be structural turns out to depend on a classifier, or on infrastructure the enterprise may not have. That is the recurring failure mode of agentic AI security, and it is the whole reason this repo is organized around the structural-versus-statistical partition. The partition does not solve these problems. It makes them visible, which is the first honest step.
