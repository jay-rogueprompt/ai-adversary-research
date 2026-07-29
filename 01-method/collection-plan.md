# Collection Plan

**`[DESIGN]`** Standing collection requirements for the case file library.

```console
rogue-prompt:~$ cat collection
```

The case files are only as good as what feeds them. This is the front half of the cycle: what is being collected, from where, and what gets discarded before analysis starts.

Published because a collection plan is an artifact in its own right. Most public threat research shows the output and hides the requirements. The requirements are the part that determines whether the output is systematic or opportunistic.

---

## Priority intelligence requirements

Five standing PIRs. Anything that does not serve one of these is out of scope, regardless of how interesting it is.

| # | Requirement | Why it stands |
|---|---|---|
| **PIR-1** | Attributed adversary use of AI in live operations | The core requirement. Named or clustered actors only. |
| **PIR-2** | Autonomous or agentic execution within an intrusion | Tests the standing force-multiplier claim directly. |
| **PIR-3** | AI tooling as a traded commodity in criminal markets | Pricing, adoption, and supply are constraint made visible. |
| **PIR-4** | AI system and agent credentials in the identity economy | Non-human identity, tokens, and service accounts as targets. |
| **PIR-5** | Provider disclosures of model misuse and safety incidents | Includes incidents involving a provider's own systems. |

**Explicitly out of scope.** Vulnerability research with no adversary. Model safety and alignment work. Prompt injection technique papers absent an actor. Product announcements. Funding news.

That exclusion list is doing most of the work. The volume of AI security content with no adversary in it is very high, and consuming it is the main way this kind of program stalls.

---

## Source tiers

Tiering is a citation rule, not a quality ranking. Tier 2 is useful and it never appears in a case file as a source.

**Tier 1: primary, citable.**

Provider threat intelligence: Google Threat Intelligence Group, Anthropic, OpenAI, Microsoft Threat Intelligence.

Incident response and vendor research: Mandiant, Unit 42, Cisco Talos, Volexity, Recorded Future, Sekoia, ESET, Trend Micro.

Government and sector: CISA advisories, NCSC, CERT-UA, sector ISAC bulletins.

**Tier 2: discovery only, never cited.**

Trade press and aggregators. Used to learn a report exists, hours or days faster than the primary feed surfaces it. The workflow is always: spot in Tier 2, retrieve the Tier 1 primary, cite the primary. Gate 0 of the extraction method forbids working from paraphrase, and this is where that discipline gets applied in practice.

**Tier 3: research.**

arXiv cs.CR, academic security venues. Rarely produces a case file. Occasionally produces a framing or a prior-art hit, and the prior-art function alone justifies keeping it.

---

## Triage gate

Every item clears three questions before it reaches the extraction method. Anything that fails is closed with a one-line reason, not left open.

**1. Is there an adversary?** An actor doing something, not a technique existing. Fails: most of what arrives. Closes as `no actor`.

**2. Which PIR does it serve?** Name one. If the answer requires arguing, it is out. Closes as `out of scope`.

**3. Is a primary source retrievable?** If only trade press exists and no underlying report can be found, hold rather than close, and revisit in a week. Some disclosures precede their own publication. Closes as `no primary`.

Items clearing all three enter the queue and get worked through the extraction method. Closed items are logged with their reason and never re-triaged, which prevents the same discarded article surfacing four more times through four different feeds.

---

## Cadence

| Interval | Action |
|---|---|
| **Daily** | Skim Tier 2 for surfacing signal. Ten minutes. No analysis. |
| **Weekly** | Triage the queue against the three gates. Retrieve primaries. |
| **Per event** | High-signal disclosures get a fast case file within days, not weeks. |
| **Monthly** | One worked case file, full method, published. |
| **Quarterly** | Review the standing `[OPEN]` claims against everything collected. Move what moved. |

The quarterly review is the step that makes this a program. Individual case files accumulate into nothing unless something periodically asks what the body of work now says that it did not say before.

Speed of translation is the capability being demonstrated by the per-event files. Depth is demonstrated by the monthly ones. Both are needed and they prove different things.

---

## Instrumentation

RSS into a reader, with the tier encoded as folder structure so citation discipline is enforced by where an item lives rather than by memory. Most Tier 1 sources publish a feed. The ones that do not are checked manually on the weekly cycle.

The tooling is deliberately unremarkable. The requirements above are the part that matters, and they work identically in any reader.

---

## Known limits

**`[OPEN]`** This collection is a floor, not a picture, and every finding drawn from it should be stated as a lower bound.

**Platform bias.** Provider reporting sees only that provider's models. An actor running open-weight models locally is invisible to the entire Tier 1 set, and the actors most worth worrying about have the resources to do exactly that. The collection is biased toward adversaries who chose convenience over operational security.

**Attribution bias.** Providers publish what they could attribute, which skews the record toward actors already well characterized elsewhere. Novel and careful actors are underrepresented by construction.

**Discretionary disclosure.** What gets published is shaped by legal, commercial, and policy considerations rather than by defender need. Absence of reporting is not evidence of absence of use.

**No non-public collection.** Nothing here derives from closed sources, employer environments, or non-public access.

---

> _All opinions are my own and do not reflect my employer._
