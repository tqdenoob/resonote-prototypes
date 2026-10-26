# collab.md: Working on the ResoNote prototype repo

Team G1T2, IS211 Interaction Design and Prototyping, AY2026-27 Term 1.

This file sets out how the seven of us write code together on the Iteration 2 high-fidelity prototype. Read it once before your first commit. If something here stops making sense, raise it in the group chat and change this file in a PR, so the rule and the practice stay the same thing.

---

## 1. The one rule that matters most

**Every PR that changes what the prototype does or looks like must also update `CLAUDE.md` in the repo root.**

No exceptions for "small" changes. A renamed button counts, because button labels are what our Changes doc, our experiment script and our screenshots refer to.

The update has three parts, and all three are required:

1. **What the prototype is now.** The current list of views, what each one does, and what is simulated.
2. **Why it is like that.** The decision behind the change: which heuristic problem it fixes, which empathy finding supports it, which alternative we tried and dropped.
3. **Which deliverable it touches.** The Iter2 file(s) and section(s) that now need to match, for example "Iter2.03 Changes, Change 2" or "Iter2.04 Prototype, View 7 screenshot".

### Why we do this

- **Our deliverables live in Drive, the prototype lives here.** Ryan and Ziyu own most of the Drive files. The person writing Iter2.04 Prototype or Iter2.05 Experiment Design is often not the person who changed the code. `CLAUDE.md` is how they find out what changed without reading diffs.
- **The rubric grades consistency.** Prototype is 40 of 100 marks. Prof Ben's Iteration 1 feedback flagged mismatches between descriptions and ratings (HE #11 and #14). If our Requirements scenario says one thing and the prototype does another, we lose marks for a problem that is purely clerical.
- **Claude and other AI tools start every session cold.** Anyone on the team who opens Claude Code, Cursor or Copilot in this repo gets `CLAUDE.md` loaded automatically. If it is stale, the assistant builds on a prototype that no longer exists and confidently tells you things that are wrong.
- **The Journal needs this history anyway.** Iter2.07 asks for weekly progress, changes, and alternative designs with screenshots. If `CLAUDE.md` and the changelog are kept up to date, the Journal is mostly copy, trim and add screenshots.
- **The LLM declaration needs evidence.** We must say which parts were AI-drafted and what we added. Logging it as we go is far easier than reconstructing it in Week 12.

### What the repo `CLAUDE.md` should contain

This is separate from anyone's personal `CLAUDE.md`. Keep it team-facing: no grades, no private notes about teammates. Use this structure and keep the headings stable so people can find things:

```markdown
# CLAUDE.md: ResoNote Iteration 2 prototype

## Project in one paragraph
<Current problem and solution statement, copied from Iter2.01 Overview. Update when Overview changes.>

## Easy scenario being prototyped
<Short version of the Iter2.02 Requirements easy scenario, with its specific details (song, bars, tempo).
 Note which hard-scenario features we borrowed and which exceptional cases we added.>

## Current prototype state (last updated: YYYY-MM-DD by <name>)
| # | View | Route / file | What it does | Simulated? | Owner |
|---|------|--------------|--------------|------------|-------|
| 1 | Music Library | /library | ... | Pre-loaded songs | ... |

## Navigation map
<Every branch and decision labelled, e.g. "Passage Complete -> Next problem / Repeat drill / End session".
 This is the source for the Iter2.04 navigation diagram.>

## Simulation and Wizard-of-Oz
<What is faked and how: scripted AI feedback, fixed recording result, input meter animation,
 what happens when a user leaves the safe path (the warning text).>

## Heuristic evaluation changes implemented
| HE # | Severity | Change in prototype | View(s) | Iter2.03 section |

## A/B experiment variants
<Independent variable, how variant A and B are selected (e.g. ?v=A / ?v=B), what differs,
 the two dependent variables and how the prototype logs them. Freeze status.>

## Decision log
| Date | Decision | Why | Alternatives tried | Affects deliverable |

## AI assistance log
| Date | Who | Tool | What was AI-drafted | What we changed or added |

## Open issues
```

---

## 2. Repo layout

Suggested structure. Adjust once we pick the stack, then update this section.

```
/                     Repo root
  CLAUDE.md           Living project state (see section 1)
  collab.md           This file
  CHANGELOG.md        One line per merged PR, newest first
  /src                Prototype source
    /views            One folder or file per view, numbered to match Iter2.04 (01-library, 02-import, ...)
    /data             Pre-loaded songs, scripted AI feedback, fake recording results
    /variants         A/B variant differences, kept isolated
  /docs
    /screenshots      One PNG per view per variant, named 06-feedback.png, 06-feedback-B.png
    /diagrams         Navigation diagram source and exports
```

Number views to match the Iter2.04 Prototype doc. When someone writes "View 7" in the doc, in a PR or in chat, everyone should know which file that is.

---

## 3. Branches and pull requests

- **`main` is always demoable.** Anyone should be able to open the deployed link at any moment and run the easy scenario end to end. Never push directly to `main`.
- **One branch per piece of work**, named by type and view:
  - `view/06-feedback-screen`
  - `fix/he2-play-pause-toggle`
  - `ab/variant-b-drag-handles`
  - `docs/claude-md-week10`
- **Small PRs.** One view, one fix, or one variant per PR. A PR that touches five views is hard to review and hard to describe in `CLAUDE.md`.
- **At least one reviewer** who did not write the code. The reviewer checks:
  - The easy scenario still runs from start to end on a phone-sized screen.
  - `CLAUDE.md` was updated with all three parts (state, why, deliverable).
  - `CHANGELOG.md` has a line.
  - Screenshots in `/docs/screenshots` are replaced if a view's appearance changed.
- **Squash and merge**, so `main` has one commit per change and the history reads like a changelog.
- **Don't push to someone else's branch** without asking them first. Comment on the PR instead.
- **Delete the branch after merging.**

### PR description template

```markdown
## What changed
<One or two sentences, in terms a user would notice.>

## Why
<HE problem number, empathy finding, scenario step, or experiment need.>

## Deliverables affected
- [ ] Iter2.02 Requirements (scenario step / feature list)
- [ ] Iter2.03 Changes (which change)
- [ ] Iter2.04 Prototype (view number, screenshot, navigation diagram)
- [ ] Iter2.05 Experiment Design (variant screenshots, task script)
- [ ] Iter2.07 Journal (alternative design worth recording)
- [ ] None

## Checklist
- [ ] CLAUDE.md updated (state, why, deliverable)
- [ ] CHANGELOG.md line added
- [ ] Screenshots replaced if visuals changed
- [ ] Ran the full easy scenario after the change
- [ ] AI assistance logged in CLAUDE.md if used
```

Ticking a deliverable box means you also tell its owner in the group chat. The box is a reminder, not a notification.

---

## 4. Commit messages

Short imperative subject, view number where relevant:

```
View 6: add Autosaved chip and Discard take confirmation
Fix HE #2: single play/pause toggle keeps playback position
A/B: variant B loop selection with drag handles
Docs: update CLAUDE.md navigation map after View 9 split
```

Avoid "update", "fix stuff", "changes". In Week 12 someone will read `git log` to write the Journal.

---

## 5. How the prototype must behave (from the Iteration 2 brief)

These are rubric requirements, not style choices. Check new code against them.

- **Easy scenario only.** If a feature isn't in the Iter2.02 easy scenario, it doesn't get built. Borrowed hard-scenario features and exceptional cases must be named in the Requirements doc first.
- **6 to 14 views.** Count before adding a new one. Record the count in `CLAUDE.md`.
- **No login, registration or profile screens.** The brief tells us to drop them.
- **Simulation is allowed and expected.** The AI coach, audio-to-score sync and pitch detection are scripted. Keep all scripted data in `/src/data` so it is easy to find and describe in Iter2.04. Never let simulated output look random between runs: participants and markers should see the same thing every time.
- **Safe path warning.** When a user taps something outside the scripted path, show a clear message that the feature isn't part of this prototype, and a way back. Don't leave dead buttons.
- **Mobile first.** ResoNote is a phone app because Clarence practises on the MRT and between classes. Test at phone width before every PR.
- **Keep the three Sev 4 / Sev 3 fixes intact.** Changes 1 to 3 in Iter2.03 (take actions and autosave, play/pause toggle with "End take", drag-handle loop selection) are graded deliverables. Don't refactor them away without updating Iter2.03.

---

## 6. A/B experiment rules

The experiment must run with at least 20 real participants, automated and web-based, with no team member intervening.

- **Variants come from one codebase.** Select them with a URL parameter or route (for example `?v=A`, `?v=B`), not two separate copies of the app. Two copies drift apart and break the "one independent variable" requirement.
- **Only the independent variable differs.** Any other difference between A and B is a confound we would have to declare in the Journal. Reviewers of an `ab/` PR should diff the two variants specifically for this.
- **Log the dependent variables in the prototype**, or make sure the testing tool (Maze, Loop11 or similar) can capture them. Document how in `CLAUDE.md` under "A/B experiment variants".
- **No personal data.** Don't log names, emails or student IDs. Participant demographics go through the survey tool, not our code.
- **Freeze before launch.** Once the experiment link goes out:
  - Tag the commit: `git tag experiment-v1`.
  - No merges to `main` that touch the experiment views until data collection ends. Work on a branch.
  - Mark the freeze in `CLAUDE.md` with the date and tag.
  - If a real bug forces a change mid-experiment, record it in the Decision log with the date and how many participants had already finished. It goes into Iter2.06 and the Journal as a validity threat.
- **Never fill in responses ourselves or generate them with an LLM.** The rubric says so explicitly.

---

## 7. Screenshots and the navigation diagram

Iter2.04 needs at least one screenshot per view and a navigation diagram with every branch labelled. Prof Ben marked us down in Iteration 1 for unlabelled branches.

- When a PR changes how a view looks, replace its screenshot in `/docs/screenshots` in the same PR.
- When a PR adds, removes or rewires a view, update the Navigation map in `CLAUDE.md` in the same PR. The diagram in Iter2.04 is drawn from it.
- Keep old screenshots of designs we dropped in `/docs/screenshots/alternatives`. The Journal asks for alternative designs with screenshots, and they are hard to recreate later.

---

## 8. Using AI tools in this repo

AI coding assistants are allowed. The course requires us to declare it.

- `CLAUDE.md` is read automatically by Claude Code. Keep it accurate so the assistant works from the real prototype.
- After a session where AI wrote or substantially changed code or copy, add a row to the AI assistance log in `CLAUDE.md`: what it drafted and what you changed, tested or decided. This feeds the Journal's LLM declaration.
- Read and run AI-generated code before opening a PR. You are the author of record.
- AI must not produce empathy quotes, interview answers or experiment data. Those must come from real people.

---

## 9. Writing style for docs and UI text

Anything in this repo may end up pasted into a deliverable, so write it that way the first time.

- Concrete and specific. "Flags bar 42 as rushed by about an eighth note" beats "gives helpful feedback".
- No em-dashes. Plain hyphens or colons are fine.
- Spell the product **ResoNote** and the group type **a cappella**.
- When explaining an unfixed problem or a severity rating, describe user impact, frequency and workarounds. Don't write "it's more of a missing feature" or "users can work it out".
- Don't describe users by "learning styles". Refer to what participants told us they actually do.

---

## 10. Weekly routine

Matches the suggested Iteration 2 schedule (W8 design, W9 to W10 build, W11 experiment, W12 analysis and pitch video, W13 present).

- **Start of week:** pull `main`, read the `CLAUDE.md` diff since last week, pick up an unassigned view or fix.
- **During the week:** small PRs, each with its `CLAUDE.md` update.
- **End of week:** one person (rotating) checks that `CLAUDE.md` matches the deployed prototype, adds a weekly summary to the Decision log, and posts in the group chat which Drive deliverables need updating. That summary is the raw material for the Journal's weekly entry.

---

## 11. Before submission (Week 12)

- [ ] `CLAUDE.md` matches the deployed prototype exactly.
- [ ] View count is between 6 and 14 and matches Iter2.04.
- [ ] Every view has a current screenshot; navigation diagram has every branch labelled.
- [ ] Iter2.03 Changes describes what the prototype actually does for each fix.
- [ ] Iter2.05 screenshots show the variants as participants saw them (use the `experiment-v1` tag).
- [ ] AI assistance log copied into the Iter2.07 Journal declaration.
- [ ] Prototype link in Iter2.01 Overview points to the final deployment.
- [ ] `App Tools Used` in Iter2.01 lists the real stack, not the template placeholder.
