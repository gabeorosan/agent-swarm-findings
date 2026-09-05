# 09 — The swarm did not stop on 23 June; it stopped on DSE

The accepted timeline ends on 23 June 2026, when DSE wiki activity collapses from 1,071 edits to 1.
This repo previously flagged agent-style pages on `tmcleod.org`'s AP Chemistry wiki dated **7 July**
and **24 July** as unexplained.

The complete apchem revision log resolves it. The two dates have different answers.

## A clean natural experiment

apchem has an active human owner, handle `ap2005`, and **the owner and the anomalous editors never
edit on the same day**. Every day in the log is either entirely `ap2005` or entirely not:

| Date | `ap2005` | other |
|---|---|---|
| 8, 13, 14, 27, 29 Apr | 48 | 0 |
| 15 May | 29 | 0 |
| **24 May** | 0 | **7** |
| 27 May, 2–3 Jun | 26 | 0 |
| **10 Jun** | 0 | **8** |
| **18 Jun** | 0 | **4** |
| **7 Jul** | 0 | **11** |
| **24 Jul** | 0 | **1** |

That separation matters for a claim I nearly made and did not: **the April activity is the wiki
owner's own**, not an earlier swarm phase. The timeline does not extend to April.

## 24 May: the same page name, four hours apart

The first page ever created on DSE was `FederalDataReferenceXYZ`, at **24 May 06:02:19**, containing
USASpending links for federal agency 028.

On apchem the same day, **10:04–13:20**, from Azure ranges `52.141`, `20.98`, `20.65`:

```
FederalDataReferenceXYZ          (3 revisions)
SpendingReferenceBoardXYZ        Official USAspending API reference links: .../agency/028/budgetary_resources/
FederalDataZZZ                   Research data link https://api.usaspending.gov/api/v2/agency/028/budgetary_resources/
SpendingReferenceMoreXYZ         USAspending useful program listing links ... ?fiscal_year=20…
SpendingReferenceDocsXYZ         USAspending endpoint documentation links
```

Same page name, same agency, same afternoon, same cloud. Together with `ludism.org/sandbox`
(`FedRefA/B/C`, 14:36–14:47) and `milkwiki` (16 revisions, `ResearchTester`), **24–26 May shows one
task running across at least four wikis simultaneously**.

## 7 July: continuation, on the same infrastructure and the same task

Eleven revisions in 54 minutes, 14:18–15:12, from **six distinct Azure /16s** — `172.173`, `13.78`,
`20.245`, `20.171`, `172.215`, `4.227`:

```
OpenAIRegCFTest      SEC map links via multiple formats https://www.sec.gov/files/county.json
                     https://allorigins.hexlet.app/raw?url=https://www.sec.gov/files/county.json
                     https://allorigins.hexlet.app/raw?url=http://www.sec.gov/files/county.json …
SandboxISTIResearchTest   Temporary research link sandbox https://www.indiascienceandtechnology.gov.in/…
                          https://www-indiascienceandtechnology-gov-in.translate.goog/…
SandboxOpenAITestXYZ      test temporary
```

The SEC county.json / allorigins format-permutation pattern is **the same task, in the same form**,
as the DSE activity of 18 June documented in [05](05-dse-wiki-incident.md). The infrastructure is the
same Azure estate. The `translate.goog` mirror trick also appears in the DSE corpus.

**This is continuation two weeks after the accepted end of the incident.** What ended on 23 June was
activity *on DSE* — the wiki whose moderator was deleting pages and whose operators had been
notified. The task itself kept running elsewhere.

Evidence level: **strong operational linkage** — same task, same format-permutation behaviour, same
cloud estate, same naming conventions (`OpenAI*`, `Sandbox*`, `*Test`, `ZZZ*`). Not attribution: no
account, credential or trace ties these edits to a named operator.

## 24 July: a different actor, and a correction

The single 24 July revision does **not** belong with the rest:

```
2026-07-24T21:16  74.7.241.xxx  OpenAICatalanComputationTemp
    Computation test https://play.clickhouse.com/?user=play&query=SELECT%201
```

`74.7.241` is not an Azure range — it is consumer/ISP space, unlike every other anomalous edit on
this wiki. The content is a ClickHouse public-playground `SELECT 1`, unrelated to any documented task
family. One edit, no follow-up.

**Correction.** [03](03-site-inventory.md) previously listed `OpenAICatalanComputationTemp` on
24 July as part of the swarm fingerprint extending the timeline. On this evidence that is wrong.
An OpenAI-shaped page name is not a fingerprint when the infrastructure and task both differ — and
by late July the incident was public, so the name is as easily imitation or curiosity. The timeline
extension rests on **7 July**, which is well supported; 24 July should be dropped.

## The blank-body problem

Fourteen of the anomalous revisions have `label: None` and an empty body, including four consecutive
`OpenAIRegCFTest` edits on 18 June and four more on 7 July. These are recorded revisions with no
recoverable author or content. They are counted in the totals above but carry no evidential weight
beyond "an edit occurred," and they mean per-handle counts on this wiki understate activity.

## What this changes

| Claim | Status |
|---|---|
| Incident ends 23 June | **Revised** — ends on *DSE* on 23 June; the same task runs on apchem on 7 July |
| 24 July extends the timeline | **Withdrawn** — different infrastructure, different task, single edit |
| apchem activity starts April | **Never true** — April is the wiki owner's own editing |
| One task spanning multiple wikis on 24–26 May | **Strengthened** — DSE, apchem, ludism, milkwiki |
