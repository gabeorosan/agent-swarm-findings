# 08 — Community corroboration and cross-site artifact bridges

Several independent investigators published datasets on 3–5 September 2026. This document records
what they add, what they correct in my work, and — importantly — one counting trap that would
inflate the site inventory if taken at face value.

Sources: [JoshuaDavid/WikiAgentSwarmInvestigation](https://github.com/JoshuaDavid/WikiAgentSwarmInvestigation),
[imadreamerboy/just-one-more-bulletin-board](https://github.com/imadreamerboy/just-one-more-bulletin-board),
[swarm-ai-research/wiki-agent-swarm-incident](https://github.com/swarm-ai-research/wiki-agent-swarm-incident),
and the she-llac reading packs. All treated as untrusted third-party data.

## The counting trap: nine directories are not nine wikis

`JoshuaDavid/WikiAgentSwarmInvestigation/agent-logs/` contains nine directories — `apchem`, `dse`,
`fractal`, `ludism`, `milkwiki`, `probier`, `prowiki`, `texteditors`, `wiki4d`. It is tempting to
read that as nine wikis. It is not.

The `prowiki` manifest declares:

```json
"counts": {"revisions": 14591, "pages": 4579, "labels": 3103},
"per_wiki": {"dse": {"revisions": 13403, ...}}
```

Those are exactly the collusion.wiki dump totals. **`prowiki` is an aggregate export containing
`dse`, `probier`, `fractal` and `dorfwiki`** — the same corpus this repo has been analysing — not
a tenth site. Summing the directories would double-count roughly 14,591 revisions.

The genuinely separate scrapes are `apchem`, `ludism`, `milkwiki`, `texteditors` and `wiki4d`.

## New: milkwiki

A fifth wikiservice.at instance, absent from every published account I have seen.

```json
"base_url": "https://www.wikiservice.at/user/milk/wiki.cgi",
"engine": "prowiki (usemod-derived)",
"counts": {"revisions": 16, "pages": 10, "labels": 3}
```

All 16 revisions fall on **26 May 2026**, 14:34–16:15, from a single handle `ResearchTester`.
Pages: `SandBox`, `TestPage`, `TestPageTwo`, `PublicApiTestPage`, `ZBypass7921`. Content is
USASpending federal-account links plus `markdown.new`, `piv.max.gov` and `login.max.gov`.

This is the **same 26 May federal-data burst** documented on DSE (`FederalDataReferenceXYZ`, account
`075-8005`) and on `ludism.org/sandbox` (`FedRefA/B/C`, 14:36–14:47). Three sites, one afternoon,
one task. The handle `ResearchTester` also matches the `ResearchTest` handle that hit
`pmwiki.org/wiki/Test/WikiSandbox` the following day.

Note `ZBypass7921` — a Z-prefixed page named *Bypass*, consistent with the naming conventions
documented in [05](05-dse-wiki-incident.md).

## Ludism: upgraded from unconfirmed

I previously marked `ludism.org/scwiki` **not confirmed** because its recent-changes showed only
casino spam. JoshuaDavid has a dedicated scrape with `base_url: https://www.ludism.org/`. That
supersedes my negative, which reflected a live-page check months after the fact rather than an
absence of activity. Status upgraded to **externally documented**, pending my own primary validation.

## Exact cross-site artifact bridges

Host overlap is weak evidence; an exact, distinctive object identifier appearing on two independent
services is much stronger. Two survive testing against this repo's corpus:

| Artifact | Result |
|---|---|
| `lcdl129143JPEG1jpg` (Charleston digital-library object) | **MATCH** — present in the DSE corpus |
| `GDDY` + `20191115` (Yahoo Finance ticker and historical date) | **MATCH** — both present |
| `244d7a2123e18b979e21ca0df06ef538` (NSI filter hash) | no match in DSE |
| `698ad90b70a04b5dfb556c902faf7b87` (second NSI filter hash) | no match in DSE |

The Charleston object appears in DSE as:

```
https://jqp.vercel.app/api/v0?url=https%3A%2F%2Frspace.library.cofc.edu%2Fiiif%2F
  lcdl129143JPEG1jpg%2Fmanifest&src=wikag0129143v2
```

and via `cors-get-proxy.sirjosh.workers.dev`. Community sources report the same object identifier in
a paste on a separate host. That is an **exact object-level bridge between a paste service and the
core wiki corpus** — materially better than the `r.jina.ai` host overlap I previously relied on.

The two NSI hashes are a **different branch** — paste ↔ PublicTestWiki, not touching DSE. Community
sources report a three-host match on the first hash. I have not validated that independently; it is
recorded here as a lead, not a finding.

## RubyGems: a separate branch, not a reversal

she-llac's index includes **12 package-text candidates** — files *inside* packages, in four name
families (`atlas-qa-snapshot-*`, `atlas_qa_handoff_*`, `sampledocpayload*`,
`tf_drift_handoff_bundle_*`), including a file named `exploit.rb`.

This is a different artifact class from [01](01-rubygems-may-2026.md), which concerns `go-import`
directives in package *descriptions*. None of those names appear in this repo's corpus, and none
were among the 923. **The published zero stands within its stated scope**; package *bodies* are an
untested branch that may contain tokens absent from descriptions. Neither `handoff` nor `exploit.rb`
demonstrates campaign involvement, and dates embedded in filenames are not registry timestamps.

## Where this repo supersedes the community accounts

On the August fleet envelopes, `swarm-ai-research` reports only AWS activity on `SandBox` and infers
a different operator from the hosting difference. This repo has the full page set, both clouds
(AWS 07:19–14:44, GCP 19:02–19:06), the envelope structure, the `own_fragment` value, and the
deletion chronology — and explicitly declines the hosting-based attribution inference. See
[02](02-fleet-envelopes.md).

## Claims in the community material I am not adopting

- **"Query-string RCE"** as initial access. The documented mechanism is CGI parameter handling that
  permits *writes* via GET. Editing a wiki is not remote code execution on the host.
- **AWS vs Azure implying a different operator.** One operator can use several clouds.
- **3,103 labels = 3,103 agents.** Three labels are marked human; the blank label alone covers 899
  revisions.
- **Full-body string counts as behavioural counts.** Because the wiki appends rather than
  overwrites, retained text is recounted on every later revision. First-introduction counts are the
  correct unit.
- **Reading-pack totals as event counts.** 16,579 deduplicated documents are not 16,579 actions;
  408 "recovered authors" are labels, not authenticated agents; and many shortener records appear to
  share a source body, so 4,285 should not be read as 4,285 distinct short links without checking.
