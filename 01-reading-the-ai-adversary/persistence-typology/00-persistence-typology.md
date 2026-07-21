# Persistence Typology: Reading the Mechanism as an Actor Signal

**Status: [OPEN] hypothesis.** This is a threat-intelligence hypothesis, not a validated finding. It applies actor-profiling tradecraft to agentic AI persistence. I believe it is directionally right and useful for triage, but I have not published cases behind it, and the enterprise incident record for agentic AI is still thin. Treat it as a lens, and push back on it.

## The idea

In traditional intrusion analysis, *how* an actor persists tells you almost as much as *that* they persisted. A cron job and a signed driver are both persistence, but they come from different actors with different resources, patience, and intent. Persistence mechanism is a profiling input.

Agentic AI systems have their own persistence surface, and it is different enough from traditional endpoints that the profiling map has to be redrawn. But the analytic move is the same: the mechanism an actor chooses to make their influence survive a session boundary reveals their sophistication, their patience, and whether they are hunting one target or many.

There are four principal persistence mechanisms in an enterprise agentic deployment. Each maps to a public framework technique where one exists. Each says something different about who you are dealing with.

## The four mechanisms

### 1. Agent memory poisoning

**Mechanism.** The actor plants an instruction-shaped item in the agent's durable memory (a preference, a "standing instruction," a fact) so it is recalled and acted on in future sessions without any live injection. Maps to MITRE ATLAS **AI Agent Context Poisoning (AML.T0080)**, memory-manipulation sub-technique.

**What it reveals.** Low to moderate sophistication, opportunistic, and product-aware. It is cheap, it requires only an understanding of the consumer-facing agent surface, and it assumes the target keeps using the same agent. It is noisy if the defender has a memory-write gate, because the write itself is an event. An actor choosing this is optimizing for persistence-through-the-product, and is probably not deeply resourced. It is also the mechanism most available to an **insider**, who understands the product surface and may have legitimate reason to be writing memory at all, which is what makes the insider case hard.

**Intent read.** Immediate, single-target influence. "Make this one agent keep doing the thing I want."

### 2. MCP descriptor poisoning

**Mechanism.** The actor publishes or modifies a tool descriptor (name, description, schema) so a tool that looks safe behaves maliciously, or so the descriptor itself steers the agent's tool selection. Maps to **AI Agent Tool Poisoning (AML.T0110)**, one of the agent-focused techniques added to ATLAS in the October 2025 MITRE and Zenity Labs collaboration, with **AI Agent Tool Invocation (AML.T0053)** as the trigger surface.

**What it reveals.** Moderate to high sophistication and a supply-chain mindset. It requires understanding the tool ecosystem, registry trust, and how descriptors flow into agent context. Crucially, it is a *one-to-many* play: a poisoned tool in a shared registry reaches every agent that binds it, not one target. An actor choosing this is thinking about a population of victims, which is organized-eCrime or nation-state supply-chain tradecraft, not opportunism.

**Intent read.** Scaled access. "Compromise the tool and I compromise everyone who uses it."

### 3. Token and OAuth-grant persistence

**Mechanism.** The actor establishes durable access at the identity layer: a task token that is not revoked, an OAuth grant that outlives the session, a delegation chain that keeps a foothold. The natural framework home is MITRE ATT&CK rather than ATLAS (Steal Application Access Token; Account Manipulation), and that is itself the tell: the mechanics are not AI-specific, which is exactly the point.

**What it reveals.** High sophistication, identity-oriented, patient. It reflects the mature-actor insight that the durable foothold is the *credential*, not the content. An actor who persists via tokens understands that content-level tricks get cleaned up and identity-level access does not, until someone audits grants. This maps directly to how established intrusion sets already think about long-term access, and its appearance on the AI surface signals an actor who brought traditional tradecraft to a new target.

**Intent read.** Durable, deniable access. "I do not need to touch the agent again; I hold the keys."

### 4. Index and embedding poisoning

**Mechanism.** The actor corrupts the retrieval layer: poisoned documents in the RAG corpus, or manipulation in embedding space, so that future queries across many users and sessions surface attacker-shaped content. Relates to **OWASP LLM04 (Data and Model Poisoning)** and **LLM08 (Vector and Embedding Weaknesses)**.

**What it reveals.** High sophistication and strategic patience. It is slow, it is hard to attribute (the poisoned document may have entered months before the effect), and it shapes outcomes at the population level rather than compromising a session. An actor choosing this is optimizing for *influence at scale over time*, which is the most strategic and the most nation-state-shaped of the four. It is also the closest thing on this surface to an information-operations capability rather than an access capability.

**Intent read.** Strategic influence. "I do not want access to your agent, I want to shape what everyone's agents conclude."

## The typology as a triage table

| Mechanism | Framework mapping | Sophistication | Reach | Intent read |
|---|---|---|---|---|
| Agent memory poisoning | ATLAS AML.T0080 | Low-moderate | One target | Immediate single-target influence |
| MCP descriptor poisoning | ATLAS AML.T0110 / AML.T0053 | Moderate-high | One-to-many | Scaled access via supply chain |
| Token / OAuth persistence | ATT&CK (identity layer) | High | Deep, one target | Durable deniable access |
| Index / embedding poisoning | OWASP LLM04 / LLM08 | High | Population, over time | Strategic influence at scale |

The diagonal is the useful part: as you move down the table, reach and patience increase and the actor's likely resourcing increases with them. Recovering the mechanism during response is not just an IOC, it is a prior on who you are dealing with before attribution evidence arrives.

## Why this is a defender's contribution and not an engineering one

An application-security architect sees these four as four vulnerabilities to close. A counter-adversary analyst sees them as four *tells*. Both views are correct and they are complementary, but the second one is missing from almost all agentic AI security writing, and it is the one that feeds an actual CTI process: mechanism choice becomes an input to actor profiling, alongside target selection, timing, and the untrusted-content vector used for initial access.

The payoff for a SOC: when your deception layer or your memory-write gate fires, the *mechanism* that fired tells your analyst which playbook to open and roughly which tier of adversary to expect, before deeper investigation. That is triage value, and triage value is what makes a typology operational rather than academic.

## Where this breaks (because an honest hypothesis says so)

- **Mechanism can be spoofed.** A sophisticated actor can deliberately use a low-sophistication mechanism to look opportunistic. The typology is a prior, not proof, and a good adversary knows you are reading the mechanism.
- **The enterprise case record is thin.** Much of the public agentic-attack corpus is research and red-team work, not in-the-wild intrusions with attributed actors. The sophistication-to-mechanism mapping is reasoned from tradecraft analogy, not yet from a body of attributed cases. That is why this is labeled OPEN.
- **Mechanisms combine.** Real intrusions chain persistence (token foothold plus a poisoned index for influence). The typology describes pure cases; reality is mixtures, and the mixture itself is a further signal I have not worked through.
- **Insider cases distort the map.** An insider can reach several of these mechanisms with legitimate access, collapsing the sophistication signal. The insider dimension deserves its own treatment and I have not written it yet.
- **The set may not be complete.** Agent-configuration modification (ATLAS AML.T0081) and agent-created scheduled tasks or automations are persistence surfaces this typology does not yet read. If the four-mechanism frame survives contact with cases, those are the candidate fifth and sixth, and the frame should be judged partly on how well it absorbs them.

## What would make this real

Cases. Specifically, attributed or semi-attributed agentic intrusions where the persistence mechanism is known and the actor's other tradecraft is known, enough of them to test whether the mechanism-to-sophistication mapping holds. Until that exists, this is a well-reasoned lens that a practitioner can use for triage while knowing its limits. If you have such cases (sanitized, publishable), they are exactly what turns this from hypothesis into contribution.
