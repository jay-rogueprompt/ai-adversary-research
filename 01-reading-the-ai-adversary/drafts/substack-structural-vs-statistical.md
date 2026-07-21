# Most AI Guardrails Are Not Security Controls

*A working note from the defender's side of agentic AI.*

I want to make an uncomfortable claim and then defend it: most of what the industry calls an AI guardrail is not a security control. It is a classifier wearing a security label. And the difference is not pedantic. It determines whether your control holds when someone who knows it exists tries to get past it.

I come at this from threat intelligence and counter-adversary work, not from application security. That background changes what you notice. An AppSec reviewer looks at an agentic AI system and asks whether the controls are present. A counter-adversary analyst looks at the same system and asks a different question: when the adversary knows exactly how this control works, what do they do next, and does anything catch them. Those two questions produce very different verdicts on the same architecture.

## The partition

Here is the distinction I have found most useful. Every control in an agentic AI system falls into one of two categories.

A **structural** control decides from a fact that exists independent of the model. A cryptographically signed token and the scope it does or does not contain. A tenant identity bound to the authenticated session. A registry entry. A bind manifest listing which tools are actually attached to this agent right now. These controls survive an adversary who has completely taken over the model's reasoning, because the fact they check is not something the model can rewrite by being talked into it.

A **statistical** control decides from a classifier reading natural language. Prompt injection detection. Domain classification. Reversibility scoring. Sensitive-data detection. These are the controls most people mean when they say guardrail, and they share one property that should worry you more than it seems to: they fail silently. When an attacker shapes input to slip past the classifier, the classifier does not raise its hand and say it was beaten. It just returns "benign," and the system proceeds as if nothing happened.

That silence is the whole problem. A firewall rule that fails, fails loud. A classifier that is evaded produces the same output as a classifier that correctly saw nothing. You cannot tell the difference from the outside, and neither can your SOC.

## Why this is not a solved problem you can classifier your way out of

The instinct, when you point this out, is to say: fine, make the classifier better. Train it on more evasions. Add a second one. This misreads the situation.

The root issue is that a probabilistic system cannot give you a deterministic guarantee. The same input can produce a different output. There is no setting of the weights that turns "usually catches injection" into "enforces a policy." You can push the evasion boundary further out, which raises the attacker's cost, and that is worth doing. But you have not changed the category of the thing. It is still a control with an evasion boundary, and a motivated adversary's entire job is to find that boundary.

This is the part that testing teaches you and a design review cannot. When you actually exercise a guardrail, you are not checking whether it blocks the obvious case. You are measuring how much work it takes to get past it, and, more importantly, whether it makes any noise when you do. A guardrail that blocks the textbook payload and stays silent on the variant next to it is not giving you the security property you think it is. You only learn that by pushing on it, which is why "we have prompt injection detection" is a statement about a single point, not a region.

## The rule I actually design around

So I do not try to make statistical controls into guarantees. I use them for two things they are genuinely good at: raising attacker cost, and generating signal. And then I put a structural control behind every statistical one that gates a high-impact action.

The rule, stated plainly: a statistical control may lower risk and must generate detection signal, but it may never be the last thing standing between an adversary and an action that exfiltrates data or cannot be undone. Behind it there has to be something structural that bounds the damage when the classifier is beaten. And where there is no such structural backstop, you say so out loud and accept the residual risk on purpose, rather than hiding it behind a classifier and hoping.

Let me make this concrete with the attack everyone is worried about.

Simon Willison named the **lethal trifecta**: give an agent access to private data, expose it to untrusted content, and give it the ability to communicate externally, and you have handed an attacker a data exfiltration primitive. The untrusted content carries an injected instruction, the agent reads your private data, the agent ships it out. No exploit code. Just language.

The statistical answer is prompt injection detection: catch the malicious instruction in the untrusted content. Deploy it, by all means. But assume it will eventually be evaded, because it is a classifier and that is what classifiers do. What catches the attack when the injection detector misses?

The structural answer is an egress allowlist that untrusted content cannot influence. The agent is allowed to read attacker-controlled text, and it is allowed to send email, but only to destinations approved out of band, destinations the untrusted content has no way to set. Now the injection can still steer the model. It simply cannot convert that into exfiltration, because the one leg of the trifecta you can cut without breaking the agent's usefulness is the external-communication leg, and you cut it with a fact, not a classifier.

That is the whole move. The classifier raises cost and, when it fires, tells your hunters someone is trying. The structural control is what actually holds when the classifier does not. One is for signal. The other is for the guarantee.

## Where it breaks, because it does

I am not selling a solution, so let me tell you where this stops working.

Some harms have no structural backstop and I will not pretend otherwise. If the damage is entirely in generated text, uplift content with no tool call and no external send, then the egress allowlist and the token scopes do nothing, because nothing is being sent or executed. The text itself is the harm, and text generation is exactly the probabilistic surface you cannot gate deterministically. That is a residual risk you accept or handle out of band. Anyone who tells you their classifier closes it is selling you the silent-failure mode as a feature.

And the structural controls are only as good as the components that anchor them: the thing that signs the tokens, the registries, the identity provider. Those form a trusted computing base, and if you have not named yours and written a compromise story for each piece, your structural guarantees are resting on faith too. That is a longer conversation and I have written it up separately.

## Why I think this matters for where the field is going

Agentic AI security is being written mostly from the application-security side, and that side is very good at cataloging controls. What it undercounts is the adversary who reads the catalog. The counter-adversary habit, assume the control is known and ask what still holds, is the habit that separates a control that survives contact from one that only survives a slide.

If you take one thing from this: go through your agentic deployment and label every control structural or statistical. Then find every place a statistical control is being trusted as if it were structural. Those places are where your architecture breaks, and the useful, slightly unnerving part is that they are completely predictable once you start looking.

---

*I write about agentic AI security from a threat intelligence and counter-adversary perspective. The reference architecture this note draws on, including the kill-chain analysis and the trusted-computing-base compromise stories, is on my GitHub, labeled honestly as design work rather than a deployed system. Attributions: the lethal trifecta is Simon Willison's; instruction/data separation traces to the dual-LLM pattern and to DeepMind's CaMeL; the PDP/PEP and deny-by-default vocabulary is from NIST SP 800-207; least agency is from the OWASP Top 10 for Agentic Applications 2026.*
