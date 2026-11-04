# scrivmark tutorial example: one finished review round

> **Status:** a worked example, kept as a record. The manuscript and its numbers are invented for the [scrivmark](https://github.com/BWBrook/scrivmark) tutorial.

This is the scrivmark tutorial manuscript, a one-page note on whether wombats prefer sunny burrows, after one complete review round. It shows what a round leaves behind:

- the reviewer's edits as real commits on a review branch;
- the author's decision on each tracked change;
- the comment threads, with their replies;
- the questions the reviewer put to an AI agent while reading, with its answers.

All of it is in git and in one JSON record, [`reviews/2026-11-03-bwb.json`](reviews/2026-11-03-bwb.json).

## Who did what

| Role | Who |
|---|---|
| Author's draft | Fictional "Sam Student", written for the tutorial |
| Reviewer | Barry W. Brook, 3 November 2026, working through the tutorial in the scrivmark viewer with Claude (Opus 5.5) in the chat |
| Answers to the reviewer's asks | Claude Opus 5.5, in that session |
| Author's responses | Simulated: Claude Opus 5.5 played Sam on 4 November 2026 at Barry's request. It chose the decisions, wrote the replies and made the revisions. Its commits are authored as "Sam Student (simulated by Claude Opus 5.5)". |

## The round in numbers

- **Tracked changes:** 19, of which Sam accepted 17. Sam rejected two, each with a comment giving the reason. One was "deep", because burrow depth wasn't measured. The other was "Australia", because "Southern Hemisphere" is what explains why north-facing slopes get the winter sun.
- **Comment threads:** 13 in all: 11 from the reviewer, plus Sam's two explanations of the rejections. All 13 are resolved. One stays orphaned, because the reviewer later deleted the sentence it was about.
- **Asks:** 2, both answered by the agent and archived in the record: "Isn't data plural?" and the table's column alignment.

## Explore it

```bash
uv tool install git+https://github.com/BWBrook/scrivmark
git clone https://github.com/BWBrook/scrivmark-tutorial-example
cd scrivmark-tutorial-example
git log --graph --oneline --all     # the round's history
scrivmark open 2026-11-03-bwb       # switch to the closed round
scrivmark serve                     # then open http://localhost:8765
```

To see the page as Sam first saw it, with the full redline and all 11 of the reviewer's comments still open, rewind your local copy of the review branch to the `as-returned` tag before serving:

```bash
git reset --hard as-returned
```

| Commit | Step |
|---|---|
| `80b6f5b` | Sam's draft, on `main` |
| `f0fcdfd` | The reviewer starts round `2026-11-03-bwb` |
| `d62b0fe` | The reviewer's edits (tag `scrivmark/2026-11-03-bwb/returned`) |
| `93902c7` | Return: the change catalogue is frozen in the record |
| `84945fd` | Sam opens the round (tag `as-returned`) |
| `040f628`, `90f063b` | Sam's decisions, replies and revisions, then close |
| `3db3211` | The round is merged into `main` |

## Licence

Code is released under the [MIT Licence](LICENSE). Text, figures and data created for this project are released under [CC BY-SA 4.0](LICENSE-CONTENT). The note cites two published papers, whose bibliographic details come from Crossref.
