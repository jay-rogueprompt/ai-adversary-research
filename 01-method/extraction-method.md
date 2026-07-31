# Provider Report Extraction

```console
rogue-prompt:~$ cat extraction-method
```

**`[DESIGN]`** The processing and analysis half of the cycle. Collection requirements are in [`collection-plan.md`](collection-plan.md).

Provider misuse reporting is finished intelligence about adversary AI tradecraft, published by the only parties with direct visibility into it. Most enterprises read it as news. This reads it as collection.

Two outputs from one input: a **hunt hypothesis** a SOC can action this quarter, and a **capability facet** that makes the next report readable faster.

---

## Gate 0: sourcing

Do not proceed from secondary coverage. Trade press paraphrases lose the qualifiers that determine what can be claimed.

- Locate the primary publication. Vendor blog, PDF, or advisory.
- Verify report title, publication date, and actor designation against it.
- Note the publishing party's visibility. A provider sees its own platform only. An IR firm sees its engagements only.
- Retrieve the full primary, not the summary page. Vendor landing pages routinely omit the operational detail that carries the finding.
- Re-derive every claim from the primary. Do not check a claim you arrived with. Checking looks for the sentence that fits and finds one.
- Separate observation from expectation. Reports mix what the publisher saw with what it anticipates. A sentence beginning "we expect" is not a finding, and it does not become one by sitting next to findings.

If only secondary sources are available, the output is labeled `[OPEN]` throughout and every claim is attributed to the secondary source, not to the provider.

---

## Gate 1: attribution state

Determine which of three states applies, because it governs everything downstream.

| State | What can be claimed |
|---|---|
| **Named actor** | Joins an existing profile. Capability facet is attributive. |
| **Cluster only** | Builds a profile. Do not assert links to named groups the provider did not assert. |
| **Unattributed technique** | No actor profile. Hunt hypothesis only. Do not manufacture an actor. |

**Enumerate before you bind.** A roundup or half-year report carries several actors and several capabilities, and they do not pair off in the order they appear. List every actor the report names, then bind each capability to exactly one. Any capability the report leaves unbound stays unbound in the case file. A capability described in a general trends section belongs to no actor, and moving it to the nearest named one is the most common way a case file acquires a claim its source does not make.

Record the provider's own confidence language verbatim and do not upgrade it. High confidence stays high confidence. Assessed stays assessed. If the provider hedged, the case file hedges.

---

## Extraction

Pull these fields for each attributed case in the report. Deliberately mechanical: the value is consistency across many reports, not depth on one.

| Field | Guidance |
|---|---|
| **Actor and confidence** | Designation plus the provider's confidence wording, unchanged. |
| **Capability used** | Reconnaissance, lure generation, code assistance, translation, tooling development, operational support, autonomous execution. |
| **Kill chain phase** | Where in the campaign the AI use sits. Prevents treating it as a standalone event. |
| **Sophistication of the ask** | Did the actor push the model hard, or use it as a search engine. |
| **Guardrail interaction** | Whether evasion was attempted, with what pretext, and how patiently. See below. |
| **Degree of autonomy** | What fraction of tactical decisions the model made without a human in the loop. Quote the provider's figure if given. |
| **Enterprise-facing implication** | What a defender should now expect, and where. |

**Guardrail interaction is the highest-signal field and the most skipped.** An actor who abandons a refused request behaves differently from one who spends weeks reformulating it. That difference is a patience and sophistication signal, and it is one of the few tells that does not depend on the actor being resource-constrained. Extract it every time, even when the report treats it as an aside.

Record the pretext as well as the patience. A single-turn framing that succeeds and a multi-week reformulation campaign are both guardrail interactions and they read differently. A cheap pretext that works says more about the guardrail than about the actor, and that is still a finding, just not one about the adversary.

---

## Gate 2: force multiplier or new capability

The central analytic question. Every case file turns on it.

> Did the model make an existing capability cheaper, or did it create a capability the actor did not previously have?

**Force multiplier.** Changes volume, speed, and cost. Changes detection thresholds and triage load. Does not change the threat model. Most cases land here.

**New capability.** Changes the threat model itself. Requires showing the actor could not otherwise have fielded this, not merely that it was faster.

The bar for claiming new capability is high and the failure mode is inflation. Before claiming it, state explicitly what the actor would have had to do without the model and why that was out of reach. If that sentence cannot be written, it is a force multiplier.

A confirmed new-capability finding moves the standing `[OPEN]` claim in the repo root and warrants its own writeup.

---

## Gate 3: does this yield a hunt hypothesis

**Honest null results are required.** Not every disclosure produces something a defender can hunt for. Much of what providers observe is reconnaissance, target research, and tooling work occurring on a platform the enterprise does not own, generating no local telemetry.

Proceed to a hunt hypothesis only if the activity produces an observable downstream effect inside an enterprise. Otherwise the case file terminates at the actor profile and says so plainly. A case file that ends with "no enterprise-observable effect, profile only" is a legitimate and useful output.

Do not manufacture a hypothesis to fill the section.

---

## Hunt hypothesis construction

The bridge is to ask what the observed activity **produces downstream**, and hunt for that rather than for the activity itself.

Each hypothesis states four things:

1. **Claim.** What should now be observable, phrased as a testable statement.
2. **Telemetry required.** Which data source and which fields. Be specific about what must already be collected and retained.
3. **Falsification.** What result would show the hypothesis is wrong. A hypothesis with no failing condition is an assertion.
4. **Baseline dependency.** What prior period is needed for comparison, and whether the organization is likely to have it.

The telemetry step is where most translation fails. "Expect better-targeted phishing" is not actionable. "Expect a measurable decline in the true positive rate of existing lure heuristics, testable against six months of prior email security verdicts" is.

Where the honest answer is that no common telemetry would capture it, say that. Naming the visibility gap is itself a finding.

---

## Capability facet

The second output. AI tooling is not a fifth Diamond Model vertex. It is a facet of **capability**, and treating it as separate is the error that keeps AI security siloed from CTI.

Record model choice, prompting style, guardrail-evasion patience, which tasks the actor delegated, and what the AI use left behind. These accumulate across reporting cycles into a profile.

**Residue is its own field.** Generated code carries the generator's habits: comment language, assistant responses committed alongside the output, coding tools left installed on operator infrastructure. These are artifacts of the tooling rather than choices by the operator, which makes them harder to spoof deliberately and easier to leave by accident. Extract them separately from tradecraft. They speak to the operator rather than to the operation, and they are the strongest evidence available for the standing claim that habits of use may prove stickier than infrastructure.

**`[OPEN]`** Whether AI tooling choices are durable enough to be attributive is unproven. Infrastructure rotates cheaply and hashes rotate cheaper. Habits of use may prove stickier because they reflect how a team works. Treat accumulated facets as a hypothesis under test, not as established attribution.

---

## Output format

Case file, following repo conventions:

```
# CF-NN: <case name>

**`[ANALYSIS]`** with staked `[OPEN]` claims, marked inline.

## Source
Primary publication, date, publishing party, visibility scope.

## Actor
Designation, confidence (provider wording), attribution state.

## Extraction
The field table, filled.

## Verdict: force multiplier or new capability
With the counterfactual sentence stated explicitly.

## Hunt hypothesis
Claim, telemetry required, falsification, baseline dependency.
Or: no enterprise-observable effect. Profile only.

## What this moves
Which standing repo claim this confirms, weakens, or leaves untouched.
```

The final section is what makes a set of case files a research program rather than a pile of writeups. Every file must state its effect on the standing claims, including "no effect."

---

## Discipline

- Public reporting only. No employer environments, no non-public collection.
- Never upgrade a provider's confidence language.
- Never assert an actor link the provider did not assert.
- Never promote an expectation to an observation.
- Label honestly: `[ANALYSIS]` for grounded analysis, `[OPEN]` for staked hypotheses.
- No em dashes. Commas, colons, or parentheses.
- Verify titles, dates, and designations against the primary source before publishing.
