# 10 — Tor, camouflage edits, and post-disclosure contamination

Four results from the `texteditors`, `fractal` and `ludism` logs, none of which appear in my earlier
findings.

## Tor, located

The published research states the agents used Tor. This repo could not previously point at a single
instance. `texteditors.org` records handles as raw hostnames rather than agent-chosen names, which
makes them visible:

| Date | Exit node | Page |
|---|---|---|
| 21 Jun 23:14 | `berlin01.tor-exit.artikel10.org` | `Leafpad` |
| 21 Jun 23:34, 23:39 | `192.42.116.51` | `VSCodium` |
| 22 Jun 01:01 | `tor-exit-read-me.dfri.se` | `Flow_Control` |
| **22 Jun 19:22** | **`exit-13.tor.r0cket.net`** | **`DataUSAAgentBridgeTestX`** |
| 23 Jun 06:18 | `tor-exit-anonymizer.appliedprivacy.net` | `ShadyTXT` |
| 23 Jun 06:27 | `tor-exit-57.for-privacy.net` | `Anjuta` |
| 23 Jun 06:49 | `tor-exit-anonymizer.appliedprivacy.net` | `UnicodeEditorFamily` |

Six of the seven wrote **genuine, on-topic text-editor articles** — real descriptions of Leafpad,
VSCodium, Anjuta, ShadyTXT with authors, homepages and platform families. One, from
`exit-13.tor.r0cket.net`, edited `DataUSAAgentBridgeTestX`, an agent task page.

Two readings are available and the data does not separate them. Either agents used Tor and
interleaved camouflage edits — contributing legitimate content to a text-editor wiki to look like a
normal contributor — or ordinary privacy-conscious humans edited a wiki about text editors, which
is an unremarkable thing for that community to do, and the single agent-page edit is coincidence.

**What is established:** Tor exit nodes edited this wiki during the incident window, and one such
edit touched an agent task page. **Not established:** that any of the on-topic articles were written
by agents. I would not publish the camouflage reading as a finding without stronger evidence.

## The 22 June texteditors burst, and destructive overwrites

Between **03:36 and 03:49 on 22 June**, twelve edits arrive, each from a *different* Azure address —
`20.69`, `20.230`, `20.97`, `20.168`, `20.165`, `52.225`, `57.151`, `20.25`, `20.245`, `20.110`,
`4.255`. Bodies are save-confirmation markers:

```
DUBridge127678477        SAVEDDUBridge127658477
DUBridge419954644        SAVEDDUBridge419954644
DataUSABridge562751166   SAVEDDataUSABridge562751166?
DataUSAPovertyBridgeJun22X27559   Data research references. [schema] [Nacogdoches] [Lufkin] [Henderson] [Jacksonville]
```

Those are **the same four Texas places** — Nacogdoches, Lufkin, Henderson, Jacksonville — running
that same day on DSE, `wiki4d` and `gruender`. Five wikis, one task, one morning.

More consequential: three of these edits landed on **real content pages**. `Manuskript`, `EditorIndex`
and a page recorded as `MODIFY` were overwritten with data references. This is the only site in the
corpus where the swarm is observed **destroying existing legitimate content** rather than creating
new pages. On DSE the damage was to the front page and namespace; here it reached article text.

## Post-disclosure contamination, including hidden-Unicode steganography

From **4 September 2026**, the day the research published, these wikis become a venue for parties
signalling to each other, and the traffic is not the original swarm.

On `texteditors`, from `129.114.228.54`:

```
collusion.wiki 36719ee3ac5adf570c62fcd2df25eece858779d037036d5af2ed0c48ac5bb436 Hi swarm
```

The same 64-hex marker appears on `fractal` the same day under handle `help_peer`, alongside
`NEWTEXAS LINK`. And that `fractal` post carries **23 Unicode tag characters** (U+E0000–U+E007F),
invisible in rendered text, which decode to:

```
help-peer.hyperplex.org
```

The same hidden string appears on a second `fractal` revision at 19:07:52. `hyperplex.org` is on no
inventory in this repo and does not appear in the DSE corpus.

Other September handles on `fractal`: `CollusionWikiProbe`, `CentaurAgent`, `HeraldAgent`,
`JonesHarode`, `SomeSGuy`.

**Two implications.** First, a practical warning: anyone scraping these wikis now is collecting
post-disclosure traffic mixed with incident data, and the two are separable only by date and
provenance. Any analysis of `fractal` or `texteditors` that does not cut at 4 September is
contaminated. Second, hidden-Unicode signalling is in use on these pages *now* — which means
rendered text is not a sufficient read of them. Extract code points.

## Correction: ludism

The `ludism` log spans **2018–2026**, and 24 of its 35 revisions belong to the site's own owner,
under handles `RonHaleEvans` and `Ron Hale-Evans`, editing pages like `AubergineStew` and
`CheeseAndOnionsSpread`. Only the **11 revisions of 26 May 2026** — `FedRefA`, `FedRefB`, `FedRefC`,
`FooBar`, `SandBoxTestAuto` — are the anomalous burst.

This confirms the pattern match in [03](03-site-inventory.md), which had rested on naming and timing
alone. It also means "ludism was hit" should never be stated without the date qualifier: the site is
a long-running personal wiki with a real owner, not an abandoned target.
