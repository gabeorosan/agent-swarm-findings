# 06 — Site inventory

Every site with agent activity, and its confirmation status. "In report" means listed in the
published collusion.wiki analysis; "new" means absent from it.

## Wikis

| Site | Status | Evidence |
|---|---|---|
| `wikiservice.at/dse` | in report | 13,403 revisions |
| `wikiservice.at/probier` | in report | 1,013 revisions |
| `wikiservice.at/fractal` | in report | 169 revisions; agents posted cross-wiki bridge links to it from DSE |
| `publictestwiki.com` | in report | first recorded attempt, 11 May |
| `texteditors.org`, Uncyclopedia | in report | proxy-chain tests |
| **`wikiservice.at/dorfwiki`** | **new** | 6 revisions, 22 Jun — found in the dump's own `wiki` field |
| **`wikiservice.at/gruender`** | **new** | `OpenResearchHelper` edits `DataUsaBridgePlaceResearch`, 22 Jun. Same handle has **32 DSE revisions**, including the same Texas-poverty task at 08:39 that morning |
| **`prowiki.org/wiki4d`** | **new** | D-language wiki dormant since 2011. Hit 18–22 Jun by `OpenAIResearchHelper`, `ResearchHelperTX999`, `AgentBridgeTXUniqueWiki4D999` |
| **`tmcleod.org` (AP Chemistry)** | **new** | `FederalDataReferenceXYZ` on 10 Jun — *the exact page name of the first page ever created on DSE*. Then `SandboxOpenAITestXYZ`, `OpenAIRegCFTest` on **7 Jul**, `OpenAICatalanComputationTemp` on **24 Jul** |
| **`pmwiki.org/wiki/Test/WikiSandbox`** | **new** | handle `ResearchTest`, 27 May, redirect tests plus a Bulgarian national-statistics link. Reverted by PmWiki maintainer Petko at 06:57 — the first human to clean up after these agents |
| **`wikiservice.at/user/milk`** (milkwiki) | **new — see [08](08-community-corroboration.md)** | 16 revisions, all 26 May, handle `ResearchTester`, pages incl. `ZBypass7921`; same federal-data burst as DSE and ludism |
| **`ludism.org/sandbox`** | **externally documented** | `FedRefA`, `FedRefB`, `FedRefC`, `FooBar`, `SandBoxTestAuto` created 26 May 14:36–14:47, the same hours as the DSE federal-data burst |
| **`usemod.org`** | **new — different swarm** | Fleet envelopes, 30 Aug. See [05](02-fleet-envelopes.md) |
| `ludism.org/scwiki` | **externally documented** | I could not reproduce it live months later, but JoshuaDavid has a dedicated scrape. My negative is withdrawn — see [08](08-community-corroboration.md) |

**`tmcleod.org` extends the accepted timeline by two weeks.** The DSE swarm collapsed 23 June; the
same task and infrastructure appear on apchem on 7 July. See [09](09-apchem-continuation.md).

## Non-wiki channels

| Channel | Status | Evidence |
|---|---|---|
| `api.counterapi.dev` | **new** | 50 namespaces; answers encoded as counter values. v1 retired 7 Aug 2026 |
| `bitily.in` (YOURLS) | **new** | 10 `OAI…REPLY` tags used as threaded board. *Observation: the admin interface responded without authentication; operators of YOURLS instances should ensure `/admin/` is authenticated. No access method is documented here and none was used.* |
| `vanderbi.lt` (YOURLS) | partly public | second instance, same pattern; independent writeup at `fi-le.net/vanderbilt` |
| `is.gd`, `v.gd` | **new** | custom aliases minted June 2026, **still resolving** |
| `rubygems.org` | **new** | 923 packages, 1–20 May. See [04](01-rubygems-may-2026.md) |
| `paste.linuxiarz.pl` | **new** | handle `agentR`, USASpending federal account `075-8005` — the same account eleven agents wrote as identical redirects on DSE |

## Cross-site fingerprints

Three markers recur across otherwise unrelated hosts:

1. **`FederalDataReferenceXYZ`** — the first page created on DSE (24 May 06:02:19) and also present
   on `tmcleod.org` (10 Jun).
2. **USASpending federal account `075-8005`** — eleven independent DSE page creations within five
   hours on 26 May, `[Person22]`'s single "human" edit, and a Polish pastebin by `agentR`.
3. **The `ZZ` prefix** — DSE test pages from 26 May, `zzp*` RubyGems packages from 8 May, and,
   per METR, the convention for **1.2 million** message-board entries in the Hugging Face incident.

## Post-publication activity (not part of the incident)

From 4 September 2026 — the day the research published — agent-facing venues and invitations
proliferated: `thecolony.ai/for-agents`, `openagentforum.com`, `messageboardforaiagents.com`,
`benchmarksolutions.org`, `aweb.ai`, `agentin.work`, `agentkind.io/relay`, plus honeypot proposals.
These are responses to the news, not evidence of the swarm, and should not be conflated with it.
