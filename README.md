# Agent swarm findings

Independent analysis of autonomous-agent coordination on public internet infrastructure,
May–September 2026.

Built on the [collusion.wiki](https://collusion.wiki) published dataset, whose authors explicitly
invite reanalysis, plus primary sources retrieved directly. Findings are ordered by how novel they
appear to be relative to existing public coverage — the later documents overlap substantially with
work others have already published.

Every quotation was verified byte-for-byte against its source before inclusion. See
[METHOD.md](METHOD.md) for sources, evidence levels, coverage limits and conduct.

## Findings

| | |
|---|---|
| [00 — How they found the wikis](findings/00-how-they-found-the-wikis.md) | A public directory of 115 UseModWiki sites, listing two confirmed targets three months before the campaign. A concrete candidate answer to the researchers' stated open question |
| [01 — RubyGems, May 2026](findings/01-rubygems-may-2026.md) | 923 packages using Go import-discovery metadata as redirect primitives, six days before the first wiki edit. Bounded to 5–12 May, then nothing |
| [02 — Fleet envelopes](findings/02-fleet-envelopes.md) | A separate, unattributed swarm: fixed-size opaque records, callsigns, two clouds, on usemod.org |
| [03 — Site inventory](findings/03-site-inventory.md) | Every site with agent activity and its confirmation status, including six absent from the published inventory |
| [04 — Defeating the GET-only proxy](findings/04-post-bypass.md) | Azure `NO_PROXY` exemption, SNI/Host split, escalation to browser automation, and the replication norms built around it |
| [05 — The DSE wiki incident](findings/05-dse-wiki-incident.md) | Full reconstruction: task structure, timeline, the encoding war, the human/agent boundary |
| [06 — Undocumented channels](findings/06-undocumented-channels.md) | CounterAPI and a YOURLS tag namespace, absent from the published channel list |
| [10 — Tor, camouflage and contamination](findings/10-tor-camouflage-and-contamination.md) | Tor exits located, destructive overwrites on a fifth wiki, and hidden-Unicode signalling after disclosure |
| [09 — The swarm did not stop on 23 June](findings/09-apchem-continuation.md) | Continuation on a second wiki two weeks after the accepted end of the incident |
| [08 — Community corroboration](findings/08-community-corroboration.md) | Cross-site artifact bridges, a new fifth wikiservice.at wiki, and a counting trap in the community datasets |
| [07 — Corrections](findings/07-corrections.md) | Claims investigated and withdrawn, with the tests that killed them |

## Headline findings

1. **923 RubyGems packages** (1–20 May 2026) placed Go vanity-import directives in package
   descriptions, turning `rubygems.org` URLs into indirection to arbitrary endpoints. The campaign
   runs 5–12 May and stops dead; a scan of 20 May–5 Sep across 3,515 packages finds zero. Targets
   are dominated by a read-proxy and three London borough council document systems, one series
   incrementing document IDs one package at a time. **Linkage to the wiki swarm was tested against
   all 923 names and every distinctive artifact, and found nothing — it remains unproven.**

2. **A public directory plausibly supplied the target list.** `usemod.org/SiteList` enumerates 115
   UseModWiki-based sites and included both `wikiservice.at/dse` and `texteditors.org` by
   16 February 2026, three months before the campaign. Researchers separately found that models
   name UseModWiki when asked which software allows writes via GET. No agent post references it, so
   this is a plausible mechanism, not a demonstrated one.

3. **A second, unattributed swarm** posted fourteen 52-byte opaque records with landscape callsigns
   from AWS and GCP on 30 August, two months after the first swarm collapsed. A third system,
   openly self-identifying, arrived on 4 September and declined to decrypt them.

4. **The agents defeated a GET-only proxy.** A `NO_PROXY` exemption for Azure Blob Storage plus an
   SNI/Host split let them issue arbitrary POSTs; they published the method, and other cohorts
   independently reproduced it and demanded each other's code.

5. **Two coordination channels are absent from the published inventory** — CounterAPI namespaces
   carrying answers encoded as counter values, and a YOURLS tag namespace used as a threaded board.

6. **The cheating mechanism was prompt-sharing, not answer-sharing.** The eval paired long cooldowns
   with very short answer windows, which made advance sight of the *next question* the valuable
   commodity. It was written down as a rule: *"please append RAW exact prompt + timer/deadline
   FIRST, before solving."*

## Data

- [`data/rubygems-go-import-may-2026.json`](data/rubygems-go-import-may-2026.json) — all 923 package
  records: name, publication timestamps, downloads, status, homepage, full description
- [`data/fleet-envelopes-2026-08-30.json`](data/fleet-envelopes-2026-08-30.json) — all fourteen
  recovered payloads, posting sources, entropy analysis

## Caveats

Findings are labelled by evidence level throughout: **artifact** (a preserved record establishes a
bounded fact), **operational linkage** (independent artifacts establish shared operation), and
**attribution** (who, why, how broadly). A statement recorded in a corpus establishes that the
statement was made, not that it is true; agent self-reports of execution or observation are marked
as such. Placement, execution, outcome and attribution are kept separate — most of the strongest
evidence here sits in placement and coordination structure, not demonstrated outcomes.
