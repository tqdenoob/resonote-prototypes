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

## One main design

`index.html` is the only design. Every change, fix or experiment variant goes into it, never into a new copy. A/B variants are switched inside `index.html` with a URL parameter (collab.md §6). When a design is dropped, save screenshots to `docs/screenshots/alternatives/` before removing its code.

## Current prototype state (last updated: 2026-10-26 by Tan Qi)

`index.html` is the whole prototype: one self-contained HTML file, plain JavaScript, no build step. **11 views** (the brief allows 6-14). Views 2-4 (setup) open as one popup over the Music Library rather than full screens, so adding a song feels like onboarding the user can leave at any point. A "Prototype guide" panel beside the phone lists the views, their HE fixes and what is simulated, and lets you jump to any view. The phone screen is **402 × 830 pt** (iPhone 16 Pro width) inside a 12 px bezel, so the frame is about 2:1 like a real iPhone body. The app is **light mode only**, whatever the phone's theme. Every tap target is at least 44 px.

| # | View | Hash link | What it does | Simulated? | Low-fi source (Iter1.4) | Owner |
|---|------|-----------|--------------|------------|------------------------|-------|
| 1 | Music Library | `#library` | Personal greeting at the top ("Evening, Clarence" style: a time-of-day phrase, then the name; "Nicely sung, Clarence" once bar 42 is mastered) with a one-line reminder about Wednesday's practice. Song list, search with "No results" state, + Add song opens the setup popup. A setup closed halfway shows as a "Setup not finished · Step n of 3" row that resumes it | 2 older songs pre-loaded; only Viva La Vida opens | View 1 | Tan Qi |
| 2 | Import Score + Audio | `#import` | **Popup** over the library. Pick score and learning track, required song title, Step 1 of 3, Help and Close (X) top-right | File picker is a scripted list of Telegram downloads | View 3 | Tan Qi |
| 3 | Choose Your Part | `#parts` | **Popup**, Step 2 of 3. Pick part, voice range shown, Hear preview, Back and Close (X) | Parts "detected" from the score; only Tenor continues | View 4 | Tan Qi |
| 4 | Sync Check | `#sync` | **Popup**, Step 3 of 3, Back and Close (X). The learning track is drawn as an audio waveform (orange count-in clicks, then the sung notes). Slide the learning track until its first sung note sits on bar 1; Play, Set marker, Undo; Step 3 of 3. Confirming while still off opens a "Track is still n s off" warning | Sync detection scripted; correct offset is -3.48 s | View 5 | Tan Qi |
| 5 | Practice Workspace | `#workspace` | Score with playhead, loop timeline with drag handles, tempo (− / + with hold, 1-BPM slider, or typed BPM), metronome, part volumes, keyboard, play/pause, Record take. First take asks for the microphone with a reason | Reference audio is a Web Audio synth | View 6 | Tan Qi |
| 6 | Sing Along + Recording | `#record` | Count-in ("Get ready", meter says "Starts after the count-in"), then "Recording", scrolling score, live level meter, End take, Cancel with confirmation | No microphone; meter animation is fixed | View 7 | Tan Qi |
| 7 | Take Feedback | `#feedback` | Overall + Pitch / Timing / Held notes with (i) and labels, bar-by-bar strip with symbols (✓ good, ? check, ! fix first), "Fix this first: bar 42", "Hear what went wrong" button, Autosaved (kept 7 days), Re-record take, Save to history, Discard take on its own row | Scores scripted per take number | Views 8 + 9 | Tan Qi |
| 8 | Understand the Issue | `#issue` | Your take / reference / both, pitch overlay chart, three numbered problems in plain words (tap to hear that part), "Show music details" | "Your take" is the reference played flat, rushed and cut short | View 10 | Tan Qi |
| 9 | Targeted Drill | `#drill` | Drill bar 42 to 2 clean takes in a row at 100%, guidance off. The coach sets tempo and guidance and offers an Adjust sheet after 2 misses (the old Version A is archived, see A/B section) | Take results scripted | Views 11-14 | Tan Qi |
| 10 | Passage Complete | `#complete` | Bar 42 mastered, before/after playback, bars still to fix (tap to loop), three labelled next steps | Before/after scores scripted | View 15 | Tan Qi |
| 11 | Session Summary | `#summary` | Session saved, time, takes with breakdown, mastered bar, still to fix before Wednesday, reminder switch | Time counted from page load | View 16 | Tan Qi |

Dropped from Iter1.4: View 2 App Usage Tutorial (removed from the Iteration 2 easy scenario, see Iter2.03). Per-screen help is kept instead (see HE #5).

## Navigation map

Source for the Iter2.04 navigation diagram. Every branch is labelled with the control that triggers it. Every view also has **Help (?)**, which opens a step-by-step overlay and returns to the same view.

- **Music Library**
  - "+ Add song" → setup popup at Import (or at the step where setup was closed)
  - Tap "Setup not finished" row → setup popup at the step where it was closed
  - Tap "Viva La Vida" (after setup) → Practice Workspace
  - Tap another song → off-path message, stay
  - Search with no match → "No songs match" + "Clear search", stay
- **Setup popup (views 2-4), shown over the Music Library.** On every step: Close (X) or Escape → Music Library, progress kept, toast "Setup saved. Tap the song to finish." (no toast if nothing was picked yet)
- **Import (Step 1 of 3)**
  - "Choose" → file sheet → pick file → Import (invalid photo shows an error and stays)
  - "Next" (enabled only with score, track and title) → Choose Your Part
- **Choose Your Part (Step 2 of 3)**
  - Back → Import
  - "Hear" → plays the part, stay
  - "Continue" with Tenor → Sync Check; with another part → off-path message, stay
- **Sync Check (Step 3 of 3)**
  - Back → Choose Your Part
  - Play / Set marker / Undo / slider / − + → stay
  - "Confirm sync" when lined up → Practice Workspace
  - "Confirm sync" when still off → sheet: "Keep lining up" → stay / "Confirm anyway" → Practice Workspace with a warning toast
- **Practice Workspace**
  - Back → Music Library
  - Play ↔ Pause/Resume, restart-to-loop-start, loop handles, tempo, metronome, part volumes sheet, keyboard → stay
  - First "Record take" of the session → sheet: "Allow microphone" → continues / "Not now" → stay (if blocked in the guide: "Microphone is off" → "Try again" / "Not now")
  - "Record take" with loop = bars 33-48 → Sing Along + Recording
  - "Record take" with any other loop → sheet: "Use bars 33-48" → Recording / "Keep my loop" → stay
- **Sing Along + Recording**
  - "End take", or the loop ends → "Checking your take…" → Take Feedback
  - "Cancel" → sheet: "Delete recording" → Practice Workspace / "Keep recording" → stay
- **Take Feedback**
  - Back → Practice Workspace
  - "Hear what went wrong" → Understand the Issue
  - "Re-record take" → Sing Along + Recording
  - "Save to history" → toggles saved, stay
  - "Discard take" → sheet: "Discard take" → Practice Workspace / "Keep take" → stay
  - "Start drill on bar 42" → Targeted Drill
- **Understand the Issue**
  - Back / "Back" → Take Feedback
  - Play your take / Play reference / Hear both / tap a problem → stay
  - "Start drill on bar 42" → Targeted Drill
- **Targeted Drill**
  - Back → Take Feedback
  - "Play bar 42" ↔ Pause/Resume, "Record take" → "End take" → checking → result, stay
  - "Play back take #n" → stay
  - "Discard take" → sheet: discard / keep → stay
  - 2 misses → Adjust sheet: one beat at a time / slow down / bring back guidance → "Try again" → stay
  - Goal met → "Bar 42 mastered" sheet: "Continue" → Passage Complete / "Practise this bar again" → resets drill
- **Passage Complete**
  - Back → Targeted Drill
  - "Practise bar 38 next" or tap a bar in "Still to fix" → Practice Workspace (loops that bar, half speed)
  - "Repeat bar 42 drill" → Targeted Drill (reset)
  - "End session" → Session Summary
- **Session Summary** (no back button: the session is saved)
  - "Practise bar 38 now" or tap a bar → Practice Workspace
  - "Back to library" → Music Library

## Simulation and Wizard-of-Oz

All scripted data is at the top of the `<script>` in `index.html`: `NOTES` / `BRIDGE` (tenor line), `TAKE_SCRIPT` (feedback scores), `BAR_STRIP` (bar colours), `MISS` (miss reasons), `CHUNKS` (beat-by-beat steps). Results are the same on every run.

- **Audio:** Web Audio triangle-wave synth of the tenor line; other parts are a soft chord on each beat; metronome clicks. Sound starts after the first tap (browser rule).
- **Import:** no real files. The picker lists 2 scripted files per slot. `IMG_4021.HEIC` triggers the invalid-file error.
- **Sync:** the learning-track waveform is generated from the scripted notes (`syncWave()`), so it looks the same every run. The track has a scripted 2-bar count-in at 138 BPM (3.48 s). "Lined up" shows within 0.12 s. Confirming with a gap opens a warning sheet; "Confirm anyway" continues with a toast and plays aligned anyway.
- **Recording:** no microphone access. The microphone prompt is a scripted sheet; "Microphone: blocked" in the guide shows the blocked state. The level meter is a fixed animation. The take length is real (time from start to End take).
- **Coach feedback:** take 1 = 72 overall (pitch 64, timing 70, held notes 78); take 2 = 76; take 3+ = 79. Priority is always bar 42.
- **Drill results:** the first 2 takes at the goal settings (whole bar, 100%, guidance off) are missed, pitch then timing. Every other take is clean. Discarding a take undoes its effect.
- **Safe-path warnings:** other songs, other parts and loops other than bars 33-48 show a message with a way back. No dead buttons.

## Heuristic evaluation changes implemented

| HE # | Severity | Change in prototype | View(s) | Iter2.03 section |
|---|---|---|---|---|
| 1 | 4 | "Autosaved" chip (kept 7 days), "Re-record take", "Save to history", "Discard take" on its own row with confirmation; drill takes autosaved with play back and discard | 7, 9 | Change 1 (**label changed from "Re-record passage"**) |
| 2 | 4 | One Play/Pause/Resume toggle that keeps position (dashed playhead when paused); recording ends with "End take" | 5, 6, 9 | Change 2 |
| 4 | 3 | Loop chosen by dragging two handles on a waveform timeline labelled Intro / Verse 1 / Verse 2 / Chorus / Bridge / Final chorus, live bar and time readout, arrow keys also move handles | 5 | Change 3 |
| 3 | 3 | Back button top-left on setup steps 2 and 3; Close (X) top-right on all three setup steps, which keeps progress; setup is a popup over the library, not a sequence of full screens | 2, 3, 4 | Smaller fixes (**update wording: Close (X) and popup**) |
| 5 | 3 | Help (?) fixed top-right on every view; overlay dims the screen, outlines each control and places the tip beside it | all | **Not fixed list: needs updating to "fixed"** |
| 8 | 3 | (i) explanation and Needs work / Good / Excellent label per metric; issues named in plain words; missed drill takes say why | 7, 8, 9 | Smaller fixes |
| 9 | 3 | Live input-level meter, "Voice picked up · good level" | 6, 9 | Smaller fixes |
| 10 | 2 | Track moves against a fixed bar 1 marker while dragging | 4 | Not listed |
| 11 | 2 | "No songs match" message with "Clear search" | 1 | Not listed |
| 13 | 2 | Song title marked Required, Next disabled with a reason, inline error | 2 | Not listed |
| 14 | 2 | "+4 since take 1" on feedback; all takes listed on the summary | 7, 11 | Not listed |
| 15 | 2 | "Step n of 3" with progress bar on all three setup steps | 2, 3, 4 | Smaller fixes |
| 16 | 2 | "Voice range: E3-G4" under each part, with an explanation | 3 | Not listed |
| 17 | 2 | − / + in 1-BPM steps (hold to repeat), a 1-BPM slider, or tap the BPM to type 69-138 with an inline error | 5 | Not listed |
| 18 | 2 | Keyboard, metronome and loop switches show the word On / Off | 5 | Not listed |
| 19 | 0 | Record buttons keep a filled-dot icon with a text label | 5, 9 | Kept |
| 20 | 0 | Sync Play, Set marker and Undo all work | 4 | Smaller fixes |

Not addressed: #6 (audio/score mismatch warning, hard scenario), #7 (segmented re-record inside a take; the drill's beat-by-beat mode partly covers it), #12 (playlists).

## A/B experiment variants

Status: **candidate, not frozen.** The experiment design (Iter2.05) hasn't been decided.

- **Archived 2026-10-26:** the main prototype now has only the coach-adapts drill (old Version B). The version with the A/B switch (`?v=A` / `?v=B`, Version A = user sets tempo and guidance) was removed from the repo on 26 Oct. Screenshots are in `docs/screenshots/alternatives/2026-10-26-ab-drill-version-a.png` and `-b.png`; the code is in git history before PR #4.
- **If we run the drill A/B:** rebuild Version A and the `?v=` switch inside `index.html` (recover the old code from git history) so both variants share every other screen.
- **Still to do before launch:** pick DVs, log them or use a testing tool (Maze, Loop11), add a participant mode that hides the guide panel, decide whether A and B follow the same scripted outcome sequence, then tag `experiment-v1` and freeze (collab.md §6).

## Decision log

| Date | Decision | Why | Alternatives tried | Affects deliverable |
|---|---|---|---|---|
| 2026-10-20 | Three parallel designs (score-first, timeline-first, coach-first) | Avoid design fixation before committing to hi-fi | n/a | Iter2.07 Journal (alternative designs); screenshots in `docs/screenshots/alternatives/` |
| 2026-10-21 | Drill rebuilt with HE fixes; moderator panel kept | Apply Iter1.5 fixes to the 12 Oct Claude Design drill | 12 Oct drill (playhead reset on pause, "Finish attempt") | Iter2.03; screenshot in `docs/screenshots/alternatives/` |
| 2026-10-26 | Full hi-fi prototype, 11 views, becomes the site root | Cover the whole easy scenario from Iter2.02 in one clickable file | Separate per-view files (rejected: harder to keep consistent) | Iter2.04 all views; Iter2.01 prototype link |
| 2026-10-26 | Library greets the singer by name with a time-of-day phrase | Makes the app feel like Clarence's own practice space; the subline keeps Wednesday's deadline in view (persona: anxious before combined practice) | Plain "ResoNote / Your songs" header (previous version) | Iter2.04 View 1 screenshot |
| 2026-10-26 | Phone frame 402 x 830 with a 12 px bezel | Previous 390 x 844 with a thin border looked too tall and narrow next to a real iPhone | 390 x 844 (iPhone 14 screen) | All Iter2.04 screenshots |
| 2026-10-26 | Scorecard uses 3 metrics: Pitch, Timing, Held notes | Matches what evaluators saw and the scenario's three problems at bar 42 | 4 metrics incl. rhythm and diction (Iter1.4 View 8) | Iter2.04 View 7; Iter1.5 #8 open question. **Team to confirm.** |
| 2026-10-26 | Views 8+9 merged into Take Feedback; Views 11-14 merged into one Drill view | Fewer screens on the main path; one priority stays visible with the scores | Separate scorecard and priority screens (low-fi) | Iter2.04 navigation diagram |
| 2026-10-26 | Help overlay kept on every view | Already built; fixes HE #5 | Removing help (Iter2.03 current text) | Iter2.03 "not fixed" list |
| 2026-10-26 | Moderator judging replaced by scripted results | Brief requires the experiment to run with no team intervention | MODERATOR ONLY Clean/Missed buttons | Iter2.05 |
| 2026-10-26 | Recording limited to bars 33-48 | Coach feedback is scripted for the bridge only | Free recording with generic feedback | Iter2.04 simulation section |
| 2026-10-26 | Phone frame scales down to fit the window height (never above 390x844) | At full size the frame was taller than a laptop screen, so the bottom buttons were cut off | Shortening the phone instead (rejected: crowds the screens) | None; Iter2.04 screenshots can still be taken at full size on a tall window |
| 2026-10-26 | App forced to light mode | Dark mode wasn't designed or tested for the experiment; one theme keeps screenshots and participants' view identical | Following the phone theme | Iter2.04 screenshots |
| 2026-10-26 | UX checklist fixes: sync warning, bar-strip symbols, 44 px targets, larger type, contrast, one record label, count-in state, mic prompt | A mobile UX checklist (Nielsen, Apple HIG, Material 3, WCAG 2.2) run on all 11 views found 2 Sev 3, 8 Sev 2 and 4 Sev 1 problems | n/a | Iter2.03 Change 1 label; Iter2.04 screenshots of views 4-7, navigation diagram (mic and sync sheets); Iter2.05 script if it says "Sing & record" |
| 2026-10-26 | Version A drill archived; main prototype keeps the coach-adapts drill only | The 26 Oct screen rewrite was built without the A/B switch | Porting Version A into the rewrite (deferred until the experiment is decided) | Iter2.05 |
| 2026-10-26 | Setup (views 2-4) becomes a popup over the library with Close (X) on every step; closing keeps progress and leaves a "Setup not finished" row | Full-screen setup steps felt like a trap: the only way out of step 1 was a back arrow and steps 2-3 could only go back one step. A popup reads as onboarding you can step out of, and the library stays visible behind it | Full-screen steps (screenshots `docs/screenshots/alternatives/2026-10-26-setup-fullscreen-*.png`) | Iter2.04 views 2-4 screenshots and navigation diagram; Iter2.03 HE #3 wording; Iter2.07 Journal alternative design |
| 2026-10-26 | One main design: removed the parallel designs, design-a/b/c, shared CSS and alternatives/ | Several copies drift apart and confuse which one is current; all future work goes into `index.html` | Keeping old designs in the repo | Iter2.07 Journal uses the screenshots in `docs/screenshots/alternatives/` |

## AI assistance log

| Date | Who | Tool | What was AI-drafted | What we changed or added |
|---|---|---|---|---|
| 2026-10-20 | Tan Qi | Claude | The three parallel designs (A, B, C), README | To fill in |
| 2026-10-21 | Tan Qi | Claude | Drill HE-fix rebuild, HE traceability doc, revised Iter1.5 HE text | To fill in |
| 2026-10-26 | Tan Qi | Claude Code | Full hi-fi prototype (`index.html`), this CLAUDE.md, CHANGELOG | To fill in after the team tests it on a phone |
| 2026-10-26 | Tan Qi | Claude Code | Scale-to-fit for the phone frame | To fill in |
| 2026-10-26 | Tan Qi | Claude Code | UX checklist, the audit of all 11 views and the fixes in this PR | To fill in after the team checks the fixes on a phone |
| 2026-10-26 | Tan Qi | Claude Code | Setup popup for views 2-4 (code and this CLAUDE.md entry) | Idea from Tan Qi (setup felt like a trapped screen); to fill in after the team tries it |

## Open issues

- Team to confirm the 3-metric scorecard and the merged views before Iter2.04 screenshots.
- Iter2.03: move #5 to fixed; mention #10, #11, #13, #14, #16, #17, #18 as smaller fixes; Change 2 label is "End take" everywhere; Change 1 label is now "Re-record take".
- Iter2.01: prototype link = https://tqdenoob.github.io/resonote-prototypes/ ; "App Tools Used" = HTML, CSS, JavaScript, Web Audio API, GitHub Pages, Claude (AI-assisted).
- A/B: pick DVs, add logging or a testing tool, add participant mode, resolve the A-variant confound, then freeze.
- Not yet tested on a real phone (only headless Chrome at 390 px and desktop). One-handed reach and screen-reader checks from the UX checklist are still open.
- Staff has no clef or key signature; the arrangement is shown in C for simplicity.
