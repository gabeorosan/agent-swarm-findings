# Method and verification

## Sources

| Source | Use |
|---|---|
| [collusion.wiki](https://collusion.wiki) published dump | `revisions.jsonl` (14,591), `events.jsonl` (19,913), `pages.jsonl` (4,579), `labels.jsonl` (3,103). The publishers explicitly invite reanalysis |
| [METR / Redwood investigation](https://metr.org/blog/2026-08-26-openai-hugging-face-incident-investigation/) | The sibling Hugging Face incident, with agent chain-of-thought |
| [ecosyste.ms](https://packages.ecosyste.ms) | Recovery of fully-yanked RubyGems packages |
| `usemod.org` page history | Fleet envelopes, via `action=browse&raw=1` |
| Hacker News thread 49563355 (1,229 comments) | Community leads, each verified independently before inclusion |

## Quote verification

Every quotation was checked byte-for-byte against the source corpus before inclusion. Quotes that
could not be matched exactly were dropped rather than paraphrased. Attributions use the
revision-editor label; note that agents copied each other's text forward, so the editor of a
revision and the handle signing the text inside it frequently differ, and these are not equated.

## Evidence levels

Applied throughout:

- **Artifact** — a preserved, inspectable record establishes a bounded fact
- **Operational linkage** — independent artifacts establish that two activities belong to one operation
- **Attribution** — evidence supports who operated it, why, and how broadly

A statement recorded inside a corpus establishes that the statement was made, not that its contents
are true. Agent self-reports of execution, observation or submission are labelled as such.

## Known coverage limits

- **1,246 deleted page_keys have no creation record** in `revisions.jsonl`. Any lifetime analysis on
  this dataset — including the ones here — is missing roughly a quarter of the deleted population.
- Deletion events are all `success_observed: true`; failed deletion attempts are not represented.
- Fully-yanked RubyGems packages are absent from the compact indexes; the 1,606-package scan of
  1–20 May 2026 depends on a third-party mirror and is not guaranteed complete.
- The Fleet payloads are recoverable only at revision 1 of each page; later revisions are blanked.

## Conduct

No writes were made to any third-party system. No package was installed or executed. No
authentication was attempted anywhere. Counter endpoints were read via documented read paths only,
never increment paths. One class of exception is logged for transparency: several `is.gd`/`v.gd`
aliases were resolved with GET before a no-network-interaction rule was adopted; they redirect to
read-only endpoints.
