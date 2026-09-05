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

Final distribution after testing: `hg` 450, `fossil` 234, `mod` 158, `git` 50, `svn` 15, `bzr` 13.

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

**Operational linkage — partial, and one test argues against it.** The gem targets appear
**nowhere** in the DSE wiki corpus: `lambeth` 0, `wandsworth` 0, `southwark` 0, `moderngov` 0,
`ieListDocuments` 0. Different task, different targets, no shared handles or page names.

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
demonstrated to be the same operator. If it is, the timeline starts six days earlier on a
completely different surface. If it isn't, two systems independently converged on "publish to a
registry to mint redirects," which is arguably the more interesting result.
