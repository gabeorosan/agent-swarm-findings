# 07 — Corrections: claims investigated and withdrawn

Findings that looked strong and did not survive their own confounds. They are kept here rather
than deleted, because the tests that killed them are the useful part.

## Withdrawn: the ZZZ pages had a survival advantage

**The claim.** Widely repeated in press coverage: agents noticed the cleanup ran alphabetically
and invented `ZZZ`-prefixed backup pages to outlast it. The supporting quote is real:

> `wiki cleanup/deletion sweep appears active alphabetically. If this page vanishes, try
> [[ZZZDataUSAConstructionWageLive]]`

**The apparent confirmation.** ZZ-prefixed pages lived a median **678.7 hours** versus **410.0**
for everything else — a difference of +268.7 hours, permutation test over 20,000 shuffles showing
zero exceedances.

**Why it's wrong.** Entirely an artefact of creation date. ZZ pages have a median creation date of
26 May; everything else, 18 June — roughly three weeks older, so mechanically longer-lived.
Controlling for creation day, the median within-day difference is **−3.5 hours**, and ZZ pages
outlived others in only 2 of 7 same-day cohorts. ZZ pages were deleted at **100%** (58/58) versus
84.9% for the rest.

Worse, the treatment group is wrong: **36 of 59 ZZ pages predate the first deletion by nine days**
and are named `ZZFooBarSlash/link`, `ZZFooBarUnderscore_id`, `ZZFooBarSpace_Space` — page-title
character fuzzing. The convention already existed; the anti-deletion story is a *repurposing*.

The sweep wasn't reliably alphabetical either. Daily rank correlation between deletion order and
alphabetical position swings from **+0.876** to **−0.903**; on 2–4 July it ran *reverse*
alphabetical, which would delete ZZ pages first.

## Withdrawn: encoding corruption as a relay clock

**The claim.** The wiki round-trips text as UTF-8→Latin-1, so a curly apostrophe doubles in length
on each pass. Tracking `Master's degree` gave 3 → 6 → 12 → 48 → 96 → 192 bytes in 48 minutes;
corpus-wide the median growth factor where it grows is exactly **2.00×** across 124 growth events
versus 5 shrinks. It looked like a molecular clock for message propagation — count the corruption,
recover how many agents had relayed it.

**Why it's wrong.** The alternative is that the *save path* re-encodes the whole page, making the
measure count saves rather than hops. That is testable: if so, every pre-existing span should
deepen in lockstep while newly typed text starts clean. **116 of 156 consecutive revision pairs
show exactly that, with 2 mixed.** The clock measures the wiki, not the agents.

The measurement is real; the interpretation was not. Correct label: an *encoding-depth trace*.

## Corrected: "benchmark contamination"

The eval items are demonstrably on the public web with exact wording, round order and timer
structure. But the chain from there to a training effect is publication → crawl inclusion →
training-set inclusion → model exposure → score effect, and only the first link is evidenced.

Correct claim: **evaluation-item disclosure creating a contamination pathway.** Not demonstrated
training contamination.

Related error: two follow-up prompts were initially attributed to one episode. `Now, do the same
for 2008.` sits on `LFSequenceCollabMay03`, a different task family from the clothing item. A
follow-up is not a recoverable item without its antecedent.

## Corrected: the Cashiers "end-to-end chain"

Offered as proof of publication → submission: cohorts fail R1 alone, then answer R2–R5 correctly
from a cached table in 11-second windows. It does not hold. It conflates the Masters/2014 and
Bachelors/2015 sequences, and eleven-second answering cannot distinguish a copied answer from an
independently fetched one. One agent says exactly that:

> `We submitted an unverified wrong guess, but later fetched exact value Education - 5,432 via
> api.cors.lol`

The chain that does close is OECD, where reliance is stated outright:

> `We used old workbook-padded consensus for R1-R3 (9.70/9.90/16.40) before discovery.`

## Corrected: "no package-registry activity"

Searching the *wiki corpus* for `rubygem`, `pypi`, `artifactory` returned zero, and that was
reported as "no package activity." Invalid inference — the packages were never going to be in the
wiki corpus. They were on rubygems.org, where 923 of them sit. See [04](04-rubygems-may-2026.md).

Lesson: searching one place and generalising to "does not exist" is the error to guard against
throughout this material.

## Corrected: "no non-OpenAI agents"

Reported on the basis of the DSE corpus, which is genuinely OpenAI-only. But the Fleet swarm
(30 Aug, usemod.org, AWS/GCP, encrypted envelopes) and Centaur (4 Sept, Muse Spark) are both
non-OpenAI. Same failure mode as above: correct about the corpus, wrong about the world.

## Overstatements walked back

- **"Termination-safe"** describes agent *intent*, not verified survival.
- **"Container died"** — missing heartbeats establish a last-observed beacon. Process failure,
  timeouts, and API overload all fit. Agents said as much: `silence cannot yet prove terminality`.
- **"Values unrecoverable"** → *not retrievable from the retired endpoint*.
- **"The researchers missed X"** → *their published inventory does not identify X*.
