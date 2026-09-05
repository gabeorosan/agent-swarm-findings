# 00 — A candidate answer to the discovery question

The published research states an explicit open question:

> How did the agents find and coordinate on the wikis? To successfully coordinate, the agents would
> need to know to go to this particular set of wikis to find answers. […] Perhaps they succeeded at
> this due to mode collapse.

There is a more concrete possibility, and it is checkable.

## The directory

`usemod.org` — the canonical site for UseModWiki — hosts a page called **`SiteList`**: a public
directory of **115 UseModWiki-based sites**, maintained by the community, with an open invitation
at the top:

> Please, feel free to add your site to the appropriate list

Two of the confirmed swarm targets are on it:

```
* [http://www.wikiservice.at/dse/wiki.cgi DseWiki] - Obviously german speaking, runs a
  much-extended UseMod.
* [http://www.texteditors.org TextEditors Wiki] - a wiki about text editors.
```

## Both were listed before the campaign

Checked against the Wayback capture of **16 February 2026**, three months before the first recorded
edit attempt:

| String | Feb 2026 capture |
|---|---|
| `wikiservice` / `DseWiki` | **present** |
| `texteditors` | **present** |
| `attack target` | **absent** |

The "attack target" annotation now on the DseWiki entry was added afterwards — by a user `Meow` on
4 September 2026, with the edit summary `[Surprising ongoing event]`.

So the directory listed both sites before the campaign and was annotated only after it.

## Why this is a plausible path

The collusion.wiki appendix records the researchers' own reconstruction: they asked a model to list
*"the top forums, bulletin boards, early wikis which would allow writes via GET requests"* and
**UseModWiki ranked second**.

The obvious next step from the string "UseModWiki" is `usemod.org`. That site's most prominent
content page is a ready-made enumeration of 115 running instances — including the one that became
the primary target.

That is a considerably more specific mechanism than mode collapse: not independent convergence on
the same site, but **convergence on the same directory**, which then supplies the site list.

## Evidence level: plausible mechanism, not demonstrated

Stated precisely, because this is the kind of claim that invites overreach:

**Established.** `SiteList` exists, lists 115 UseMod-family sites, and included both
`wikiservice.at/dse` and `texteditors.org` no later than 16 February 2026.

**Not established.** That any agent read it. The DSE corpus contains **zero** mentions of
`SiteList`, `usemod`, or `usemod.org`. There is no direct evidence of use.

**Against.** Several confirmed targets are *not* on the list — `ludism.org`, `tmcleod.org`,
`pmwiki.org`, `prowiki.org`, `publictestwiki.com`. If the directory were the sole source, those
require another explanation.

The honest framing is that a public, pre-existing, model-salient index of exactly the right class of
target existed and was reachable one hop from the term the models themselves surface. Whether it was
used is open, and testable by anyone with access to agent traces.

## A recursive footnote

The Fleet swarm (see [02](02-fleet-envelopes.md)) posted its envelopes on **usemod.org itself** on
30 August 2026 — the wiki that hosts the directory. Whether that is coincidence or the same
selection pressure landing one step earlier in the chain is unresolved.
