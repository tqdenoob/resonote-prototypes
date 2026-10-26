# CLAUDE.md: ResoNote Iteration 2 prototype

Team G1T2, IS211 Interaction Design and Prototyping, AY2026-27 Term 1. Read `collab.md` before your first commit: every PR that changes what the prototype does or looks like must update this file.

Live site (GitHub Pages, `main` branch root): https://tqdenoob.github.io/resonote-prototypes/

## Project in one paragraph

Singers in vocal music CCAs (choirs and a cappella groups) learn their parts alone between combined rehearsals. Members who cannot sight-read juggle a PDF score, a learning track, a metronome and a piano app that don't sync, struggle with fast tempos and complex rhythms, and get no feedback on pitch or timing until the music director corrects them at rehearsal. ResoNote is a mobile app: import the score and learning track, pick your part, and practise in one workspace (score with playhead, loop, tempo, metronome, keyboard). Record a passage and an AI coach, simulated in this prototype, scores pitch, timing and held notes, names one bar to fix first, explains it, and runs a drill that adapts to how the singer is doing.

> Source: Iter2.01 Overview is still a draft. When it is finalised, replace this paragraph with its problem and solution statements.

## Easy scenario being prototyped

From Iter2.02 Requirements, Scenario 1 (Easy): "Learn and master a new part before combined practice".

- Sunday evening, on the MRT home to Bedok. The SMU VOIX music director has shared the PDF score and MIDI learning track for **"Viva La Vida"** on Telegram, for **Wednesday's** combined practice.
- Clarence imports both files and picks **tenor**. The learning track has a **2-bar count-in** that isn't on the score, so he corrects the offset (about a minute) until playback follows the score from bar 1.
- At home he gets stuck at the **bridge, bars 33-48** (a jump, then a fast eighth-note run at **bar 40**). He loops the bridge at **half speed** with a steady beat, checks notes on the keyboard, and raises the tempo back to full speed.
- He records the passage. The coach flags **bar 42** as the one to fix first: flat on the high notes, rushing the eighth-note run, cutting the held note short. He hears his take against the reference.
- Drill: slower with a guided count-in, then full speed on his own. **He misses twice at full speed**, so the drill switches to **one beat at a time**, then puts the bar back together. He sings bar 42 cleanly and masters it.
- He reviews the session summary and the suggested passage for next time.

Borrowed from the hard scenario: the manual sync correction and the adjust-drill path (after 2 misses). Exceptional cases added: an invalid file (a photo instead of a PDF), an empty song title, a search with no results, discarding a take, and a loop outside the scripted bars.

## Product voice

In-app copy is **casual, concise and playful** (decided 2026-10-26 by Tan Qi). Short sentences, contractions, a light joke where it costs nothing ("Fix it once, win twice", "Nailed it!"). Rules:

- **Keep labels the deliverables cite.** Buttons and states named in Iter2.03, the HE table and the navigation map stay literal: Play / Pause / Resume, Sing & record, End take, Re-record passage, Save to history, Discard take, Autosaved, Fix this first, Needs work / Good / Excellent, Step n of 3, Required, Lined up, Confirm sync. Playfulness goes in headings, hints, toasts, sheets, help tips and coach messages.
- **Errors stay clear first, cheeky second.** Say what's wrong and how to fix it ("IMG_4021.HEIC is a photo, not a score. Pick the PDF.").
- **Coach feedback keeps the numbers.** Cents, beats and seconds stay in the explanations; only the phrasing loosens.
- **Same voice in drill Versions A and B**, so tone doesn't become a confound in the A/B test.
- The guide panel beside the phone is documentation for evaluators, not product copy, and stays neutral.

## Current prototype state (last updated: 2026-10-26 by Tan Qi)

`index.html` is the whole prototype: one self-contained HTML file, plain JavaScript, no build step. **11 views** (the brief allows 6-14). A "Prototype guide" panel beside the phone lists the views, their HE fixes and what is simulated, and lets you jump to any view.

| # | View | Hash link | What it does | Simulated? | Low-fi source (Iter1.4) | Owner |
|---|------|-----------|--------------|------------|------------------------|-------|
| 1 | Music Library | `#library` | Song list, search with "No results" state, + Add song | 2 older songs pre-loaded; only Viva La Vida opens | View 1 | Tan Qi |
| 2 | Import Score + Audio | `#import` | Pick score and learning track, required song title, Step 1 of 3 | File picker is a scripted list of Telegram downloads | View 3 | Tan Qi |
| 3 | Choose Your Part | `#parts` | Pick part, voice range shown, Hear preview, Step 2 of 3 | Parts "detected" from the score; only Tenor continues | View 4 | Tan Qi |
| 4 | Sync Check | `#sync` | Slide the learning track until its first sung note sits on bar 1; Play, Set marker, Undo; Step 3 of 3 | Sync detection scripted; correct offset is -3.48 s | View 5 | Tan Qi |
| 5 | Practice Workspace | `#workspace` | Score with playhead, loop timeline with drag handles, tempo (typed BPM), metronome, part volumes, keyboard, play/pause, Sing & record | Reference audio is a Web Audio synth | View 6 | Tan Qi |
| 6 | Sing Along + Recording | `#record` | Count-in, scrolling score, live level meter ("Hearing you · nice level"), End take, Cancel with confirmation ("Scrap this take?") | No microphone; meter animation is fixed | View 7 | Tan Qi |
| 7 | Take Feedback | `#feedback` | Overall + Pitch / Timing / Held notes with (i) and labels, bar-by-bar strip, "Fix this first: bar 42", Autosaved, Re-record passage, Save to history, Discard take | Scores scripted per take number | Views 8 + 9 | Tan Qi |
| 8 | Understand the Issue | `#issue` | Your take vs reference playback, pitch overlay chart, three plain-language explanations | "Your take" is the reference played flat, rushed and cut short | View 10 | Tan Qi |
| 9 | Targeted Drill | `#drill` | Drill bar 42 to 2 clean takes in a row at 100%, guidance off. Version A or B (see A/B section) | Take results scripted | Views 11-14 | Tan Qi |
| 10 | Passage Complete | `#complete` | Bar 42 mastered, remaining bars to check, three labelled next steps | Before/after scores scripted | View 15 | Tan Qi |
| 11 | Session Summary | `#summary` | Time, takes, mastered bar, all takes, suggested next passage | Time counted from page load | View 16 | Tan Qi |

Dropped from Iter1.4: View 2 App Usage Tutorial (removed from the Iteration 2 easy scenario, see Iter2.03). Per-screen help is kept instead (see HE #5).

## Navigation map

Source for the Iter2.04 navigation diagram. Every branch is labelled with the control that triggers it. Every view also has **Help (?)**, which opens a step-by-step overlay and returns to the same view.

- **Music Library**
  - "+ Add song" → Import
  - Tap "Viva La Vida" (after import) → Practice Workspace
  - Tap another song → off-path message, stay
  - Search with no match → "Nothing called … yet" + "Clear search", stay
- **Import (Step 1 of 3)**
  - Back → Music Library
  - "Choose" → file sheet → pick file → Import (invalid photo shows an error and stays)
  - "Next" (enabled only with score, track and title) → Choose Your Part
- **Choose Your Part (Step 2 of 3)**
  - Back → Import
  - "Hear" → plays the part, stay
  - "Continue" with Tenor → Sync Check; with another part → off-path message, stay
- **Sync Check (Step 3 of 3)**
  - Back → Choose Your Part
  - Play / Set marker / Undo / slider / − + → stay
  - "Confirm sync" → Practice Workspace
- **Practice Workspace**
  - Back → Music Library
  - Play ↔ Pause/Resume, restart-to-loop-start, loop handles, tempo, metronome, part volumes sheet, keyboard → stay
  - "Sing & record" with loop = bars 33-48 → Sing Along + Recording
  - "Sing & record" with any other loop → sheet: "Set loop to bars 33-48 and record" → Recording / "Keep my loop" → stay
- **Sing Along + Recording**
  - "End take", or the loop ends → "Listening back…" → Take Feedback
  - "Cancel" → sheet "Scrap this take?": "Delete recording" → Practice Workspace / "Keep singing" → stay
- **Take Feedback**
  - Back → Practice Workspace
  - "Hear what went wrong" → Understand the Issue
  - "Re-record passage" → Sing Along + Recording
  - "Save to history" → toggles saved, stay
  - "Discard take" → sheet: "Discard take" → Practice Workspace / "Keep take" → stay
  - "Start drill on bar 42" → Targeted Drill
- **Understand the Issue**
  - Back / "Back" → Take Feedback
  - Play your take / Play reference → stay
  - "Start drill on bar 42" → Targeted Drill
- **Targeted Drill**
  - Back → Take Feedback
  - "Play bar 42" ↔ Pause/Resume, "Record take" → "End take" → checking → result, stay
  - "Play back take #n" → stay
  - "Discard take" → sheet: discard / keep → stay
  - Version B, 2 misses → Adjust sheet: one beat at a time / slow down / bring back guidance → "Try again" → stay
  - Goal met → "Bar 42 mastered" sheet: "Continue" → Passage Complete / "Practise this bar again" → resets drill
- **Passage Complete**
  - Back → Targeted Drill
  - "Next problem: bar 38" → Practice Workspace (loop bars 37-40, half speed)
  - "Repeat drill on bar 42" → Targeted Drill (reset)
  - "End session" → Session Summary
- **Session Summary**
  - Back → Passage Complete
  - "Done" → Music Library

## Simulation and Wizard-of-Oz

All scripted data is at the top of the `<script>` in `index.html`: `NOTES` / `BRIDGE` (tenor line), `TAKE_SCRIPT` (feedback scores), `BAR_STRIP` (bar colours), `MISS` (miss reasons), `CHUNKS` (beat-by-beat steps). Results are the same on every run.

- **Audio:** Web Audio triangle-wave synth of the tenor line; other parts are a soft chord on each beat; metronome clicks. Sound starts after the first tap (browser rule).
- **Import:** no real files. The picker lists 2 scripted files per slot. `IMG_4021.HEIC` triggers the invalid-file error.
- **Sync:** the learning track has a scripted 2-bar count-in at 138 BPM (3.48 s). "Lined up" shows within 0.12 s. Confirming with a gap shows a toast and plays aligned anyway.
- **Recording:** no microphone access. The level meter is a fixed animation. The take length is real (time from start to End take).
- **Coach feedback:** take 1 = 72 overall (pitch 64, timing 70, held notes 78); take 2 = 76; take 3+ = 79. Priority is always bar 42.
- **Drill results:** the first 2 takes at the goal settings (whole bar, 100%, guidance off) are missed, pitch then timing. Every other take is clean. Discarding a take undoes its effect.
- **Safe-path warnings:** other songs, other parts and loops other than bars 33-48 show a message with a way back. No dead buttons.

## Heuristic evaluation changes implemented

| HE # | Severity | Change in prototype | View(s) | Iter2.03 section |
|---|---|---|---|---|
| 1 | 4 | "Autosaved" chip, "Re-record passage", "Save to history", "Discard take" with confirmation; drill takes autosaved with play back and discard | 7, 9 | Change 1 |
| 2 | 4 | One Play/Pause/Resume toggle that keeps position (dashed playhead when paused); recording ends with "End take" | 5, 6, 9 | Change 2 |
| 4 | 3 | Loop chosen by dragging two handles on a waveform timeline labelled Intro / Verse 1 / Verse 2 / Chorus / Bridge / Final chorus, live bar and time readout, arrow keys also move handles | 5 | Change 3 |
| 3 | 3 | Back button top-left on every setup step | 2, 3, 4 | Smaller fixes |
| 5 | 3 | Help (?) fixed top-right on every view; overlay dims the screen, outlines each control and places the tip beside it | all | **Not fixed list: needs updating to "fixed"** |
| 8 | 3 | (i) explanation and Needs work / Good / Excellent label per metric; issues named in plain words; missed drill takes say why | 7, 8, 9 | Smaller fixes |
| 9 | 3 | Live input-level meter, "Hearing you · nice level" | 6, 9 | Smaller fixes |
| 10 | 2 | Track moves against a fixed bar 1 marker while dragging | 4 | Not listed |
| 11 | 2 | "Nothing called \"…\" yet" message with "Clear search" | 1 | Not listed |
| 13 | 2 | Song title marked Required, Next disabled with a reason, inline error | 2 | Not listed |
| 14 | 2 | "+4 since take 1" on feedback; all takes listed on the summary | 7, 11 | Not listed |
| 15 | 2 | "Step n of 3" with progress bar on all three setup steps | 2, 3, 4 | Smaller fixes |
| 16 | 2 | "Voice range: E3-G4" under each part, with an explanation | 3 | Not listed |
| 17 | 2 | Tap the BPM to type an exact value (69-138), inline error outside the range; − / + in 5% steps | 5, 9 (A) | Not listed |
| 18 | 2 | Keyboard (and metronome, loop, guidance) switches show the word On / Off | 5, 9 (A) | Not listed |
| 19 | 0 | Record buttons keep a filled-dot icon with a text label | 5, 9 | Kept |
| 20 | 0 | Sync Play, Set marker and Undo all work | 4 | Smaller fixes |

Not addressed: #6 (audio/score mismatch warning, hard scenario), #7 (segmented re-record inside a take; the drill's beat-by-beat mode partly covers it), #12 (playlists).

## A/B experiment variants

Status: **candidate, not frozen.** The experiment design (Iter2.05) hasn't been decided.

- **Candidate IV:** how drill support is controlled on the Targeted Drill view (Iter1 feedback asked us to compare adaptive drills with ordinary looping).
  - **A (control):** the user sets tempo (− / + or a typed BPM) and switches guidance on or off.
  - **B (treatment):** the coach sets tempo and guidance in 3 steps (Guided slower → Guided full speed → On your own) and after 2 misses offers an Adjust sheet (one beat at a time / slow down / bring back guidance).
  - Everything else on the screen is identical.
- **Selecting a variant:** `?v=A` or `?v=B` in the URL, e.g. `https://tqdenoob.github.io/resonote-prototypes/?v=A#drill`. The guide panel also has an A/B switch. Default is B (it matches the easy scenario).
- **DVs:** not chosen. The prototype doesn't log anything yet. If we use this, decide the DVs and either log them in the page or capture them with the testing tool (Maze, Loop11).
- **Known confound to resolve before launch:** scripted results depend on settings, so A users who never reach 100% with guidance off never see a miss. Decide whether A and B should follow the same scripted outcome sequence.
- **Before launch:** add a participant mode that hides the guide panel and variant switch, then tag `experiment-v1` and freeze (collab.md §6).

## Decision log

| Date | Decision | Why | Alternatives tried | Affects deliverable |
|---|---|---|---|---|
| 2026-10-20 | Three parallel designs (score-first, timeline-first, coach-first) | Avoid design fixation before committing to hi-fi | n/a | Iter2.07 Journal (alternative designs); now in `parallel-designs.html` |
| 2026-10-21 | Drill rebuilt with HE fixes; moderator panel kept | Apply Iter1.5 fixes to the 12 Oct Claude Design drill | 12 Oct drill (playhead reset on pause, "Finish attempt") | Iter2.03; `alternatives/drill-he-fixes-2026-10-21.html` |
| 2026-10-26 | Full hi-fi prototype, 11 views, becomes the site root | Cover the whole easy scenario from Iter2.02 in one clickable file | Separate per-view files (rejected: harder to keep consistent) | Iter2.04 all views; Iter2.01 prototype link |
| 2026-10-26 | Scorecard uses 3 metrics: Pitch, Timing, Held notes | Matches what evaluators saw and the scenario's three problems at bar 42 | 4 metrics incl. rhythm and diction (Iter1.4 View 8) | Iter2.04 View 7; Iter1.5 #8 open question. **Team to confirm.** |
| 2026-10-26 | Views 8+9 merged into Take Feedback; Views 11-14 merged into one Drill view | Fewer screens on the main path; one priority stays visible with the scores | Separate scorecard and priority screens (low-fi) | Iter2.04 navigation diagram |
| 2026-10-26 | Help overlay kept on every view | Already built; fixes HE #5 | Removing help (Iter2.03 current text) | Iter2.03 "not fixed" list |
| 2026-10-26 | Moderator judging replaced by scripted results | Brief requires the experiment to run with no team intervention | MODERATOR ONLY Clean/Missed buttons | Iter2.05 |
| 2026-10-26 | Product voice: casual, concise, playful (see Product voice) | Tan Qi's direction; short, friendly copy suits practice in short pockets (MRT, between classes) | Neutral instructional copy (previous version) | Iter2.04 screenshots of every view; Iter2.03 wording if it quotes on-screen text other than the kept labels; Iter2.05 script if it quotes coach messages |
| 2026-10-26 | Recording limited to bars 33-48 | Coach feedback is scripted for the bridge only | Free recording with generic feedback | Iter2.04 simulation section |

## AI assistance log

| Date | Who | Tool | What was AI-drafted | What we changed or added |
|---|---|---|---|---|
| 2026-10-20 | Tan Qi | Claude | The three parallel designs (A, B, C), README | To fill in |
| 2026-10-21 | Tan Qi | Claude | Drill HE-fix rebuild, HE traceability doc, revised Iter1.5 HE text | To fill in |
| 2026-10-26 | Tan Qi | Claude Code | Full hi-fi prototype (`index.html`), this CLAUDE.md, CHANGELOG | To fill in after the team tests it on a phone |
| 2026-10-26 | Tan Qi | Claude Code | Rewrite of in-app copy to the casual, concise, playful voice | Tan Qi set the voice; team to review the wording on a phone |

## Open issues

- Team to confirm the 3-metric scorecard and the merged views before Iter2.04 screenshots.
- Iter2.03: move #5 to fixed; mention #10, #11, #13, #14, #16, #17, #18 as smaller fixes; Change 2 label is "End take" everywhere.
- Iter2.01: prototype link = https://tqdenoob.github.io/resonote-prototypes/ ; "App Tools Used" = HTML, CSS, JavaScript, Web Audio API, GitHub Pages, Claude (AI-assisted).
- A/B: pick DVs, add logging or a testing tool, add participant mode, resolve the A-variant confound, then freeze.
- Not yet tested on a real phone (only headless Chrome at 390 px and desktop).
- Staff has no clef or key signature; the arrangement is shown in C for simplicity.
