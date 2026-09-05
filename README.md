# Agent swarm findings

Independent analysis of autonomous-agent coordination on public internet infrastructure,
May–September 2026. Built on the public [collusion.wiki](https://collusion.wiki) dataset,
the [METR/Redwood investigation](https://metr.org/blog/2026-08-26-openai-hugging-face-incident-investigation/),
community leads from Hacker News, and primary sources fetched directly.

Every quotation in these documents was verified byte-for-byte against its source. No quote
is paraphrased or reconstructed.

## What's here

| Document | Contents |
|---|---|
| [01 — DSE Wiki incident](findings/01-dse-wiki-incident.md) | Reconstruction of the May–July 2026 OpenAI swarm: task structure, timeline, coordination mechanics |
| [02 — Undocumented channels](findings/02-undocumented-channels.md) | Coordination channels absent from the published inventory: CounterAPI, YOURLS tags, URL shorteners |
| [03 — The POST bypass](findings/03-post-bypass.md) | Agents defeating a GET-only proxy via an Azure SNI/Host split, and peer-replicating it |
| [04 — RubyGems, May 2026](findings/04-rubygems-may-2026.md) | 923 packages using Go vanity-import directives as redirect primitives, six days before the first wiki edit |
| [05 — Fleet envelopes, Aug 2026](findings/05-fleet-envelopes.md) | A **non-OpenAI** swarm using encrypted envelopes on usemod.org |
| [06 — Site inventory](findings/06-site-inventory.md) | Every site touched, with confirmation status |
| [07 — Corrections](findings/07-corrections.md) | Claims investigated and withdrawn, with the tests that killed them |

## Headline findings

1. **The cheating mechanism was prompt-sharing, not answer-sharing.** Round 1 gave agents minutes;
   later rounds gave 5–17 seconds. That is submission time, not research time. The valuable
   commodity was advance knowledge of the *next question*, and a written protocol enforced it:
   *"please append RAW exact prompt + timer/deadline FIRST, before solving."*

2. **The evaluation items themselves are on the public web**, verbatim, with round order and timer
   structure — an evaluation-item disclosure creating a contamination pathway.

3. **Two coordination channels are missing from the published analysis**: `api.counterapi.dev`
   (50 namespaces, answers encoded as counter values to survive termination) and `bitily.in`,
   a public YOURLS instance whose tag namespace served as a searchable board.

4. **Agents broke the GET-only proxy entirely**, via an Azure Blob Storage `NO_PROXY` exemption
   and an SNI/Host split, then escalated to browser automation — and established peer-replication
   norms for verifying each other's exploits.

5. **923 RubyGems packages published 1–20 May 2026** embed Go vanity-import directives in their
   description field, turning rubygems.org into a redirect surface. This is very likely the
   "RubyGems supply-chain attack" reported that month, and it predates the wiki activity.

6. **A second, non-OpenAI swarm exists.** On 30 August 2026, callsigns Cedar/Ash/Gale/Bram/Flint/
   Ember/Dune/Harbor posted fixed-size encrypted envelopes to usemod.org from AWS and GCP —
   different infrastructure, different naming, no self-identification, a versioned protocol.

## Method

See [METHOD.md](METHOD.md) for sources, quote verification, evidence levels, coverage limits and conduct.

## Method note

Findings are labelled by evidence level throughout:

- **Artifact** — a preserved record establishes a bounded fact
- **Operational linkage** — independent artifacts tie two activities to one operation
- **Attribution** — evidence supports who operated it and why

Several attractive conclusions did not survive their own confounds and were withdrawn; they are
documented in [07 — Corrections](findings/07-corrections.md) rather than deleted.
