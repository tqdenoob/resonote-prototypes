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

## Current prototype state (last updated: 2026-10-27 by Tan Qi)

`index.html` is the whole prototype: one self-contained HTML file, plain JavaScript, no build step. **11 views** (the brief allows 6-14). Views 2-4 (setup) open as one popup over the Music Library rather than full screens, so adding a song feels like onboarding the user can leave at any point. The score is printed on a full-width white "paper" band (two lines on the workspace, three while recording), the one surface that isn't a card; section headings are sentence case. Colour rule: one background, one main, one accent. Blue = actions and selection, orange = highlights (light orange = check / needs work, solid orange = fix first), green = good, red = errors, recording and delete. A "Prototype guide" panel beside the phone lists the views, their HE fixes and what is simulated, and lets you jump to any view. The phone screen is **402 × 830 pt** (iPhone 16 Pro width) inside a 12 px bezel, so the frame is about 2:1 like a real iPhone body. The app is **light mode only**, whatever the phone's theme. Every tap target is at least 44 px. **Every main screen opens with a page title** (Young Serif, 27 px) and one line saying what you do there, e.g. "Practise your part: Loop a passage, slow it down, then record a take for the coach." The small header above it carries context (song, part), not the task. Recording keeps only its header so nothing distracts while singing. **The Practice Workspace is the hub:** drills, the last take's feedback and recording all start there, and Take Feedback and the drill both go Back to it.

**Colour scheme (26 Oct, three-tone):** cream background (#F9F8F3 app, #ECF0F1 page, white cards), blue main (#1C70AD), orange accent (#B35C14, soft #FCEBDA). Green (#1A7F45) and red (#C0392B) are kept only as universal indicators (good; error, recording, delete). Why: the 26 Oct "Gamified Studio" trial used seven hues (sky blue, orange, yellow, coral, mint plus deeper text shades), which made it hard to tell which colour meant what; three tones keep the meaning of each colour obvious. All text colours keep 4.5:1 contrast. The Gamified Studio palette is screenshotted in `docs/screenshots/alternatives/2026-10-26-colour-gamified-*.png` and the indigo/orange original in `2026-10-26-colour-original-*.png`. Deliverables touched: Iter2.04 Prototype (every view screenshot), Iter2.07 Journal (alternative designs).

| # | View | Hash link | What it does | Simulated? | Low-fi source (Iter1.4) | Owner |
|---|------|-----------|--------------|------------|------------------------|-------|
| 1 | Music Library | `#library` | Personal greeting at the top ("Evening, Clarence" style: a time-of-day phrase, then the name; "Nicely sung, Clarence" once bar 42 is mastered), always on one line, with a small blue sound-wave icon. Song list, search with "No results" state, + Add song opens the setup popup. A setup closed halfway shows as a "Setup not finished · Step n of 3" row that resumes it | 2 older songs pre-loaded; only Viva La Vida opens | View 1 | Tan Qi |
| 2 | Import Score + Audio | `#import` | **Popup** over the library. Title "Add a song"; the step bar says what's next ("Next: choose your part"). Pick score and learning track, required song title, Step 1 of 3, Help and Close (X) top-right | File picker is a scripted list of Telegram downloads | View 3 | Tan Qi |
| 3 | Choose Your Part | `#parts` | **Popup**, Step 2 of 3, title "Choose your part". Pick part, voice range shown, Hear preview, Back and Close (X) | Parts "detected" from the score; only Tenor continues | View 4 | Tan Qi |
| 4 | Line Up the Track (was "Sync Check") | `#sync` | **Popup**, Step 3 of 3 ("Last step"), Back and Close (X). Title "Line up the track", then "The track starts 2 bars early" in plain words. Footer button "Confirm line-up". The learning track is drawn as an audio waveform (amber count-in clicks labelled "count-in, not on the score", then the sung notes). Slide the track until its first sung note sits on the "Line up here" marker; the slider has 0 in the middle (earlier left, later right) and one status badge shows the gap ("3.48 s off" / "Lined up"). Play, Set marker, Undo, with a hint explaining Set marker. Confirming while still off opens a "Track is still n s off" warning | Sync detection scripted; correct offset is -3.48 s | View 5 | Tan Qi |
| 5 | Practice Workspace | `#workspace` | **The hub.** Title "Practise your part". Two lines of the score (8 bars) on a paper band with playhead, loop timeline with drag handles, tempo (− / + with hold, 1-BPM slider, or typed BPM), metronome, part volumes, keyboard, play/pause, Record take. A **Coach card** under the loop has "Open drills" (opens the Drills sheet: bar 42 first with its coach video, then bars 38, 40, 35, 46, each looped at half speed; before any take it offers "Record bars 33-48") and, once there is a take, "Last take · See feedback". First take asks for the microphone with a reason | Reference audio is a Web Audio synth | View 6 | Tan Qi |
| 6 | Sing Along + Recording | `#record` | Count-in ("Get ready", big beat number "n of 4", meter says "Listening after the count-in"), then "Recording", three lines of the score to read ahead with a progress bar under them, live level meter, End take; **Cancel** is a labelled text button top-left with confirmation | No microphone; meter animation is fixed | View 7 | Tan Qi |
| 7 | Take Feedback | `#feedback` | Title "Take n feedback". Order: overall ring (coloured by its label), then **"Fix this first: bar 42" with "Bar score 58 / 100"** and "Hear what went wrong", then Pitch / Timing / Held notes with (i) and labels (the (i) opens an explanation inline under the score bar, closed by (i) again or its ×), bar-by-bar strip with symbols (✓ good, ? check, ! fix first) that **scrolls sideways** with fixed 30 px cells and opens centred on the fix-first bar, then This take: Autosaved (kept 7 days), Save to history, Discard take. Footer: **Re-record take** and **Start drill** | Scores scripted per take number | Views 8 + 9 | Tan Qi |
| 8 | Understand the Issue | `#issue` | One three-way player (Your take / Reference / Both), pitch overlay chart, three numbered problems in plain words (tap to hear that part), "Show music details" | "Your take" is the reference played flat, rushed and cut short | View 10 | Tan Qi |
| 9 | Targeted Drill | `#drill` | Opens from **Open drills** (workspace) or **Start drill** (Take Feedback). Title "Drill bar 42", then a **coach demo video** ("How to sing bar 42", 0:25, captions on; Play / Pause / Hide; collapses to a "Watch" row after the first take). After 2 misses, "one beat at a time" swaps in a 0:15 beat-by-beat video. Drill bar 42 to 2 clean takes in a row at 100%, guidance off. The coach sets tempo and guidance and offers an Adjust sheet after 2 misses (the old Version A is archived, see A/B section) | Take results scripted. Coach video is Wizard-of-Oz (see Simulation) | Views 11-14 | Tan Qi |
| 10 | Passage Complete | `#complete` | Bar 42 mastered, one sentence "Bar score 58 → 92 in 9 drill takes, about 8 minutes" (replaces stat tiles), before/after playback, bars still to fix (tap to loop), three labelled next steps | Before/after scores scripted | View 15 | Tan Qi |
| 11 | Session Summary | `#summary` | Session saved, tonight's win (bar score 58 → 92), minutes practised with takes (drill row shows "9 takes · 2 missed"), mastered bar, still to fix before Wednesday, reminder switch | Time counted from page load | View 16 | Tan Qi |

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
- **Line Up the Track (Step 3 of 3, was Sync Check)**
  - Back → Choose Your Part
  - Play / Set marker / Undo / slider / − + → stay
  - "Confirm line-up" when lined up → Practice Workspace
  - "Confirm line-up" when still off → sheet: "Keep lining up" → stay / "Confirm anyway" → Practice Workspace with a warning toast
- **Practice Workspace**
  - Back → Music Library
  - "Open drills" (Coach card) → Drills sheet:
    - before any take: "Record bars 33-48" → Sing Along + Recording (mic prompt first if needed) / "Not now" or X → stay
    - after a take: "Bar 42" → Targeted Drill / "Bar 38", "Bar 40", "Bar 35", "Bar 46" → stay on the workspace, looping that bar at half speed / X → stay
  - "Last take · See feedback" (Coach card, after a take) → Take Feedback for the latest take
  - Play ↔ Pause/Resume, restart-to-loop-start, loop handles, tempo, metronome, part volumes sheet, keyboard → stay
  - First "Record take" of the session → sheet: "Allow microphone" → continues / "Not now" → stay (if blocked in the guide: "Microphone is off" → "Try again" / "Not now")
  - "Record take" with loop = bars 33-48 → Sing Along + Recording
  - "Record take" with any other loop → sheet: "Use bars 33-48" → Recording / "Keep my loop" → stay
- **Sing Along + Recording**
  - "End take", or the loop ends → "Checking your take…" → Take Feedback
  - "Cancel" (text button, top-left) → sheet: "Delete recording" → Practice Workspace / "Keep recording" → stay
- **Take Feedback**
  - Back → Practice Workspace
  - "Hear what went wrong" → Understand the Issue
  - "Re-record take" (footer) → Sing Along + Recording
  - "Save to history" → toggles saved, stay
  - "Discard take" → sheet: "Discard take" → Practice Workspace / "Keep take" → stay
  - "Start drill" → Targeted Drill
- **Understand the Issue**
  - Back / "Back" → Take Feedback
  - Play your take / Play reference / Hear both / tap a problem → stay
  - "Start drill" → Targeted Drill
- **Targeted Drill**
  - Back → Practice Workspace
  - Coach video: Play ↔ Pause / "Watch again", "Hide" ↔ "Watch" → stay
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
- **Coach feedback:** take 1 = 72 overall (pitch 64, timing 70, held notes 78); take 2 = 76; take 3+ = 79. Priority is always bar 42, scored 58 before the drill and 92 after (`BAR42`); the same two numbers appear on Take Feedback, the mastered sheet, Passage Complete and Session Summary.
- **Drill results:** the first 2 takes at the goal settings (whole bar, 100%, guidance off) are missed, pitch then timing. Every other take is clean. Discarding a take undoes its effect. With the default "one beat at a time" adjustment the drill takes 9 takes (2 missed); jumping straight to Passage Complete or Session Summary from the guide uses the same numbers.
- **Coach demo video (Wizard-of-Oz):** no real video. `COACH_VID` holds two timed scripts: `bar` (0:25, 6 captions, plays bar 42 at half then full speed) and `beats` (0:15, one beat at a time at half speed). The frame is a dark panel with the five notes of bar 42 as bars; the notes the caption talks about light up orange and a playhead follows the synth. In the real app this would be a short recorded clip of a vocal coach. Playing the reference or recording stops the video.
- **Safe-path warnings:** other songs, other parts and loops other than bars 33-48 show a message with a way back. No dead buttons.

## Heuristic evaluation changes implemented

| HE # | Severity | Change in prototype | View(s) | Iter2.03 section |
|---|---|---|---|---|
| 1 | 4 | "Autosaved" chip (kept 7 days), "Re-record take" in the footer (always visible), "Save to history", "Discard take" on its own row with confirmation; drill takes autosaved with play back and discard; Cancel recording is a labelled button with confirmation | 6, 7, 9 | Change 1 (**label changed from "Re-record passage"**) |
| 2 | 4 | One Play/Pause/Resume toggle that keeps position (dashed playhead when paused); recording ends with "End take" | 5, 6, 9 | Change 2 |
| 4 | 3 | Loop chosen by dragging two handles on a waveform timeline labelled Intro / Verse 1 / Verse 2 / Chorus / Bridge / Final chorus, live bar and time readout, arrow keys also move handles | 5 | Change 3 |
| 3 | 3 | Back button top-left on setup steps 2 and 3 (step 3 renamed from "Sync Check" to "Line up the track"); Close (X) top-right on all three setup steps, which keeps progress; setup is a popup over the library, not a sequence of full screens | 2, 3, 4 | Smaller fixes (**update wording: Close (X) and popup**) |
| 5 | 3 | Help (?) fixed top-right on every view; overlay dims the screen, outlines each control and places the tip beside it. Every main screen also has a page title and a one-line purpose | all | **Not fixed list: needs updating to "fixed"** |
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
| 2026-10-26 | Headings and the library greeting in Young Serif (replaces Fraunces from the greeting PR), everything else stays Figtree | One serif across the app instead of two. A serif on page titles gives ResoNote a printed-music feel and separates headings from controls; Young Serif is less common than the usual Playfair/Fraunces choices. Only page titles (`.h1`) and the guide titles use it, so buttons, labels and numbers keep Figtree | Bodoni Moda (too thin at phone sizes), Newsreader, a single sans family | Iter2.04 Prototype (all view screenshots retaken after merge) |

| Date | Decision | Why | Alternatives tried | Affects deliverable |
|---|---|---|---|---|
| 2026-10-27 | Take Feedback: metric (i) explanation sits inline under its score bar with its own × close; bar-by-bar strip scrolls sideways with fixed-width cells | Team usability check: the explanation floated over the (i) button and stayed put when scrolling (it shared the `.tip` class with the Help tour bubble), so closing it meant scrolling to find a hidden button. The strip squeezed 16 bars into one row, too small to read, and a longer loop (e.g. bars 31-60) would not fit at all | Floating popover anchored to the button; wrapping the strip onto several rows (loses the left-to-right reading of the song) | Iter2.04 Prototype, View 7 screenshot |
| 2026-10-27 | Practice Workspace becomes the hub: a Coach card with "Open drills" and "Last take · See feedback"; drill Back goes to the workspace; Take Feedback keeps "Start drill" as a shortcut | Tan Qi: the workspace is where practising and singing happen, so drills should start there with a clear button. Before this, drills could only be reached from Take Feedback, so a singer back on the workspace had no way back to a drill | Drills only from the workspace (removing Start drill); a Practise / Drill tab inside the workspace; a bottom tab bar (see Open issues) | Iter2.02 feature list (drills from the workspace, coach video); Iter2.04 View 5 and 9 screenshots and navigation diagram; Iter2.05 script if it says "Start drill"; Iter2.07 Journal (before screenshots `docs/screenshots/alternatives/2026-10-27-before-titles-*.png`) |
| 2026-10-27 | Each drill opens with a coach demo video (simulated), with a separate beat-by-beat video after the adjust step | Tan Qi asked for video practice in drills. Watching a coach sing the bar before trying it gives the singer a model to copy, closer to "just as their own choir teacher would" (Iter2.01 solution). Empathy: P5 wanted explanations, P7 only learnt his mistakes when the music director corrected him | Bouncing-ball sing-along video; a separate drill video library | Iter2.01 solution wording; Iter2.04 View 9 and simulation section; Iter2.07 Journal |
| 2026-10-27 | Page titles on every main screen; "Sync Check" renamed "Line up the track"; setup step bar says what comes next | Tan Qi: titles should be bigger and clearer so people know what they are doing, especially on the busy workspace. "Sync" is jargon; "line up the track" says the action | Keeping the 16 px header title only | Iter2.04 all screenshots (views 2-5, 7, 9) and navigation diagram (view 4 name, "Confirm line-up"); Iter2.03 HE #3 wording (view name); Iter2.05 script if it names "Sync Check" |
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
| 2026-10-26 | UI/UX audit fixes: score as the hero (bigger staff, 2 lines on the workspace, 3 while recording, on a paper band); Take Feedback reordered so "Fix this first" follows the overall score and Re-record take moves to the footer; one colour rule (green good, amber check, orange fix first, blue actions); Cancel recording is a labelled button; Sync slider centred on 0 with one status and a "Line up here" target; bar 42 score (58) shown on Feedback; sentence-case headings, flat lists and no stat tiles; drill CTA renamed "Start drill" | A UI/UX audit (ui-ux-pro-max checklist, bencium and frontend-design skills) found: the score had the least space on the screens where Clarence relies on it most; the one-priority message and the Sev 4 HE #1 Re-record were below the fold; "Good" was blue in one place and green in another; a back arrow deleted the take; the sync slider put 0 at 80%; 58 appeared on Passage Complete with no earlier source and the guide fallback said 4 clean when the scripted path gives 7; tracked ALL-CAPS labels, identical cards and stat tiles read as a template | Screenshots before the change: `docs/screenshots/alternatives/2026-10-26-pre-audit-*.png` | Iter2.04 screenshots of views 4-11 and navigation diagram labels ("Start drill", "Cancel"); Iter2.03 Change 1 (Re-record take now in the footer, Cancel button) and Change 2 unchanged; Iter2.05 script if it says "Start drill on bar 42"; Iter2.07 Journal alternative designs |
| 2026-10-26 | One main design: removed the parallel designs, design-a/b/c, shared CSS and alternatives/ | Several copies drift apart and confuse which one is current; all future work goes into `index.html` | Keeping old designs in the repo | Iter2.07 Journal uses the screenshots in `docs/screenshots/alternatives/` |

## AI assistance log
| 2026-10-26 | Tan Qi | Claude | Mapping the Gamified Studio colours onto a three-tone palette (CSS tokens) | Tan Qi set the rule: one background, one main, one accent, plus universal indicator colours |
| 2026-10-26 | Tan Qi | Claude | Shortlist of font pairings and the CSS change applying Young Serif to headings | Tan Qi chose Young Serif with the existing Figtree |

| 2026-10-27 | Tan Qi | Claude | CSS/JS fix for the inline metric explanation and the scrolling bar strip | Tan Qi found both problems in a usability check and proposed the scroll bar |

| Date | Who | Tool | What was AI-drafted | What we changed or added |
|---|---|---|---|---|
| 2026-10-27 | Tan Qi | Claude Code | Workspace Coach card, Drills sheet, simulated coach video scripts and captions, page titles and the "Line up the track" wording | Ideas and direction from Tan Qi (workspace as hub, drill videos, clearer titles); Tan Qi chose coach demo video and keeping Start drill on feedback. To fill in after the team checks it on a phone |
| 2026-10-20 | Tan Qi | Claude | The three parallel designs (A, B, C), README | To fill in |
| 2026-10-21 | Tan Qi | Claude | Drill HE-fix rebuild, HE traceability doc, revised Iter1.5 HE text | To fill in |
| 2026-10-26 | Tan Qi | Claude Code | Full hi-fi prototype (`index.html`), this CLAUDE.md, CHANGELOG | To fill in after the team tests it on a phone |
| 2026-10-26 | Tan Qi | Claude Code | Scale-to-fit for the phone frame | To fill in |
| 2026-10-26 | Tan Qi | Claude Code | UX checklist, the audit of all 11 views and the fixes in this PR | To fill in after the team checks the fixes on a phone |
| 2026-10-26 | Tan Qi | Claude Code | Setup popup for views 2-4 (code and this CLAUDE.md entry) | Idea from Tan Qi (setup felt like a trapped screen); to fill in after the team tries it |
| 2026-10-26 | Tan Qi | Claude Code | UI/UX audit of all 11 views and the fixes in this PR (score as hero, feedback order, colour rule, Cancel, sync, numbers, headings) | Tan Qi asked for the audit and chose which findings to fix; to fill in after the team checks it on a phone |

## Open issues

- **Navigation model (27 Oct, proposal, team to decide):** no bottom tab bar for now. ResoNote's screens are steps in one task (practise → record → feedback → drill), not sibling sections, and a tab bar would need top-level places the easy scenario doesn't have (history, profile), which would be dead tabs. Instead: the Practice Workspace is the hub, every screen is at most one Back away from it (Understand the Issue is two), and the Coach card gives direct entry to drills and the last take. If the team wants a tab bar later, the candidate is a per-song strip (Practise / Feedback / Drills) at the top of the workspace, not an app-wide bottom bar.
- Coach video captions were written by us, not a vocal coach; ask the Participant 9 music director to check the wording.

- Team to confirm the 3-metric scorecard and the merged views before Iter2.04 screenshots.
- Iter2.03: move #5 to fixed; mention #10, #11, #13, #14, #16, #17, #18 as smaller fixes; Change 2 label is "End take" everywhere; Change 1 label is now "Re-record take".
- Iter2.01: prototype link = https://tqdenoob.github.io/resonote-prototypes/ ; "App Tools Used" = HTML, CSS, JavaScript, Web Audio API, GitHub Pages, Claude (AI-assisted).
- A/B: pick DVs, add logging or a testing tool, add participant mode, resolve the A-variant confound, then freeze.
- Not yet tested on a real phone (only headless Chrome at 390 px and desktop). One-handed reach and screen-reader checks from the UX checklist are still open.
- Staff has no clef or key signature; the arrangement is shown in C for simplicity.
- Audit findings not fixed yet: Passage Complete and Session Summary still repeat the "still to fix" list and Complete has 3 stacked footer buttons; drill "Takes / No takes yet" label is weak; loop section labels clip at 375 px; sheets don't move keyboard focus into themselves (only the setup popup has `aria-modal`); 11 px labels on the timeline and bar strip; on phones ≤480 px the app sits inside a rounded frame; the desktop phone frame has no status bar.
