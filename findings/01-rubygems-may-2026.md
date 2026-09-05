# 04 — RubyGems, May 2026: 923 packages as redirect primitives

Six days before the earliest recorded wiki edit attempt, the same behavioural signature appears on
a package registry.

## The mechanism

`rubygems.org/api/v1/gems/<name>.yaml` serves a package's description verbatim. Put an HTML
`go-import` meta tag in the description and a Go toolchain fetching that URL follows it to an
arbitrary destination. **Publishing a gem mints an attacker-chosen redirect hosted on
rubygems.org.** There is no payload and no Ruby code — the package *is* the redirect.

Example, from `oaijx7803530`:

```
<meta name='go-import' content='rubygems.org/api/v1/gems/oaijx7803530.yaml mod
https://r.jina.ai/http:%2F%2Fhttpbin.org%2Fresponse-headers?Version=v1.2.3&Time=x'>
```

## Scale

Scanning every RubyGems package created 1–20 May 2026 (**1,606** packages), **923 carry a
go-import directive in the description field**. All are now removed. Combined downloads: **8,001**.

The campaign is tightly bounded. Daily counts: **5 May 1 · 8 May 41 · 9 May 2 · 11 May 259 ·
12 May 620**. First package `2026-05-05T14:58:57`, last `2026-05-12T08:01:00`. On the final day all
620 fall between 01:26:39 and 08:01:00.

A follow-up scan of **20 May – 5 September 2026 (3,515 packages) found zero go-import packages.**
No further matches were observed in that window; the technique does not reappear.

Fully-yanked packages are dropped from `index.rubygems.org/names` and `/versions` and from the
owner API, which is why they are hard to enumerate. They survive in
[ecosyste.ms](https://packages.ecosyste.ms), which is how this set was recovered.

## The escalation, in sequence

| When | What |
|---|---|
| 5 May 14:58 | `tempzzhfar010test` → `https://github.com/golang/example`. The canonical harmless Go test repo — a pure "does this work" probe. 270 downloads |
| 5 May 15:08–15:20 | Same account: `farmer-proxy-test220280` (homepage `h-farm.com`), `xkrbeqkjkg` (homepage `x.com`), descriptions `x test` and `x` — testing whether the *homepage* field also renders as a followable link |
| 8 May 15:59–16:25 | `zzzagent0mzqkj1f_proxy`, then `zzpa`, `zzpb`, `zzpc`, `zzpd`, `zzpe`… one every 20–60 seconds |
| 11 May | `oaijx7803530`, `zrgvsearch94e8` — targets now wrapped in `r.jina.ai` and pointing at real documents |
| 12 May 07:38:37→07:39:14 | `oakmi16800`, `oakmi16900` … `oakmi18000` — one package every ~3 seconds, incrementing `MId=` on a London borough council's committee-documents system |

The 8 May series is a methodical matrix sweep. Same Google Drive file ID throughout, varying two
dimensions:

- VCS scheme: `vcs` → `svn` → `hg` → `bzr` → `git`
- URL form: `lh3.googleusercontent.com/d/ID` → `drive.google.com/file/d/ID/view` →
  `/thumbnail?id=` → `/open?id=` → `googleapis.com/drive/v3/files/ID`

Final distribution after testing: `hg` 450, `fossil` 234, `mod` 158, `git` 50, `svn` 15, `bzr` 13,
`vcs` 2, plus 1 package (`wandsworthprobe1778551714`) whose description contains a go-import string
with no parseable `content` attribute. Total 923.

## Targets

`r.jina.ai` 554 · `moderngov.lambeth.gov.uk` 127 · `democracy.wandsworth.gov.uk` 79 ·
`www.digitizationguidelines.gov` 21 · `lh3.googleusercontent.com` 18 · Southwark council 15 ·
`httpbin.org` 13 · `drive.google.com` 9 · plus `postman-echo.com`, `echo.free.beeceptor.com`,
`dummyjson.com`, `geolocation-db.com` as capability probes.

The `oakmi*` series is **paginated scraping of UK local-government meeting records**, one published
package per page.

## Relation to the reported "RubyGems supply-chain attack"

RubyGems flagged malicious spam on **11 May 2026** (120+ packages initially, then a flood),
suspended new signups **13 May**, brought in WAF and rate limiting, and declared it resolved
**16 May**, having yanked "500+ malicious packages."

923 go-import packages sit inside that window. The security coverage describes a supply-chain
attack; on this evidence it looks more like **automated redirect-minting by something trying to
read documents it could not reach directly**.

## Evidence levels

**Artifact — verified.** Package existence, publication timestamps, descriptions, redirect
targets, download counts, removal status. Directly retrieved.

**Operational linkage — tested directly, and it fails.** The strongest available test is whether
any distinctive, high-information artifact from the gem campaign occurs anywhere in the wiki corpus.
Run against full revision bodies, in literal, percent-decoded and HTML-unescaped forms:

| Artifact | Result |
|---|---|
| Google Drive file ID used throughout the 8 May sweep (`0ByXlrcn4L69jdUJDTGhwQ0RfdGM`) | no match |
| `zzzagent0mzqkj1f_proxy` and its distinctive suffix `mzqkj1f` | no match |
| `tempzzhfar010`, `oaijx7803530`, `zrgvsearch94e8`, `farmer-proxy-test220280` | no match |
| **All 923 gem names** | **0 matches** |

Gem targets are likewise absent: `lambeth` 0, `wandsworth` 0, `southwark` 0, `moderngov` 0,
`ieListDocuments` 0. Different task, different targets, no shared handles, no shared page names,
no shared identifiers.

A negative result here does not refute a common operator — tasks, identifiers and retained records
can legitimately differ — but there is **no positive artifact bridge** in the observed data.

What does overlap:
- `r.jina.ai` — 554 gem targets, **1,679 occurrences in the wiki corpus**. But it is a popular
  public read-proxy; weak alone.
- Naming — `oai*` prefixes, `zzzagent0mzqkj1f_proxy` matching the wiki's `Agent0` handles, `zz*`
  prefixes, `*test` suffixes, random numeric tokens. Moderate.
- Timing — 5–12 May, ending as the wiki phase begins. Moderate.
- Modus operandi — find a writable public surface, use it as a fetch primitive. Strong as pattern,
  weak as identity.

**Attribution — not established.** This is a distinct campaign with the same behavioural
signature, temporally adjacent, sharing proxy infrastructure and naming style. It is *not*
demonstrated to be the same operator, and the artifact join above is the test that would have
shown it if a shared identifier existed.

**Honest headline:** *923 RubyGems packages carried Go import-discovery metadata pointing to
external endpoints, in a concentrated 5–12 May campaign; linkage to the wiki activity remains
unproven.*

One technical caveat worth keeping: a `go-import` tag is **client-interpreted metadata, not an
HTTP redirect**. Go's import-prefix checks, VCS handling and repository-root verification all
affect what actually happens next. Placement is demonstrated; successful retrieval is not. For the
same reason, the `oakmi*` series is evidence of **systematic enumeration**, not of completed
scraping. If it is, the timeline starts six days earlier on a
completely different surface. If it isn't, two systems independently converged on "publish to a
registry to mint redirects," which is arguably the more interesting result.
