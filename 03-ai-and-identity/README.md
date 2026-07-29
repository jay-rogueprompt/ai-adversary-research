# AI and Identity

```console
rogue-prompt:~$ cd 03-ai-and-identity
```

**What an agent's credentials are worth to an adversary, and why identity systems cannot see the problem.**

Identity systems answer two questions: who is this, and what may they touch. Neither asks whether an action is consistent with the task that justified granting the access.

Authorization is evaluated per action and per resource. Agentic risk accrues per trajectory. Every individual step in an agentic intrusion can be permitted by local policy while the sequence is the intrusion.

---

## What is here

| File | What it is | Status |
|---|---|---|
| `agentic-identity-model.md` | Capability tiers and autonomy stages, with credential requirements per tier | planned |
| `nhi-and-agent-credentials.md` | Non-human identity as an adversary objective | planned |
| `credential-markets.md` | AI platform and agent credentials in the stolen credential economy | planned |

---

## The claim this section is built on

**`[OPEN]`** High-autonomy agents require ephemeral, just-in-time credentials rather than standing service accounts, because a standing credential attached to an autonomous process is a persistent entitlement with no bounded task to justify it.

This is a design position, not an observation. It follows from the trajectory-versus-action gap above and it needs testing against cases where agent credentials were actually abused.

---

## Sourcing

Public reporting only. `credential-markets.md` in particular draws on published vendor and provider research, not on non-public collection.

> _All opinions are my own and do not reflect my employer._
