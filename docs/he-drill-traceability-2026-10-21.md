# HE to Hi-Fi Drill Traceability

**G1T2 · ResoNote**

Links each of the 20 problems in `Iter1.5 Heuristic Evaluation (Revised).md` to the high-fidelity design we have now. Prepared 21 Oct 2026. Feedback only: nothing in the prototype or the HE file was changed.

> **LLM declaration:** this mapping was AI-drafted from the prototype's source code. The team should check each row against the running prototype before quoting it in Iter2.03 Changes or Iter2.04 Prototype.

---

## 1. Scope

- **Design checked:** `~/Downloads/ResoNote Hi-Fi Prototype.html` (Claude Design export, 12 Oct 2026).
- **Views in that file:** one view, **Drill, bar 14**, in two versions:
  - **Version A (control, user-controlled support):** the user sets tempo with − / + buttons or a slider, and switches Guidance (count-in and pitch line) on or off.
  - **Version B (treatment, adaptive support):** the coach sets tempo and guidance in three steps ("Guided, slower", "Guided, full speed", "On your own"), and after 2 misses in a row offers an "Adjust" sheet (Slow down / Shorten the passage / Restore guidance).
- **Shared by both:** "Song A · Soprano", badge "Bar 14 · late entry", score excerpt of bars 13 to 15 with bar 14 highlighted, goal "2 clean attempts in a row at 100% tempo, guidance off", attempt history, "Play bar 14" / "Pause" toggle, "Record attempt" / "Finish attempt", a "Checking your attempt…" sheet with MODERATOR ONLY Clean / Missed buttons, a "Bar 14 mastered" sheet and a "How this drill works" help sheet.
- **Not in this file:** Library, Import, Vocal Parts, Sync Check, Practice Workspace, Sing Along, Take Feedback and AI Coach. Most HE problems sit on those views, so many rows below are "Not in this file". They need checking again once those views are built.

**Status key**

| Status | Meaning |
|---|---|
| Fixed | The HE fix is implemented on this view. |
| Partial | Some of the fix is here; the rest is missing or lives on another view. |
| Pattern applied | The problem's view isn't here, but this view follows the lesson of the fix. |
| Gap | The fix should apply here and doesn't, or something here repeats the problem. |
| Not in this file | The problem belongs to a view that isn't in this design. |

---

## 2. Traceability table

| HE # | Sev | Problem | Where in the Drill design | Version A | Version B | Status | Iter2.03 says |
|---|---|---|---|---|---|---|---|
| 1 | 4 | Missing take actions and recovery controls | Every attempt is logged as a chip, e.g. "#3 · 80% · guided", with a tick (clean) or cross (missed). "Record attempt" is always available for another try. No "Autosaved" chip, "Save to history" or "Discard take" here; the header back button is labelled "Back to take feedback", where Change 1 should live. | Same | Same | Partial | Fixed (Change 1) |
| 2 | 4 | Pause and stop reset playback and are easily confused | One toggle switches between "Play bar 14" (play icon) and "Pause" (pause icon). Help text: "Tap again to pause; it keeps your place." Recording ends with a separate dark "Finish attempt" button (square icon), visually distinct from playback. **Pausing still resets the playhead** (see Gap 1). | Same | Same | Partial (labels fixed, behaviour not) | Fixed (Change 2) |
| 3 | 3 | No back button on Sync Check | Not in this file. The Drill header has a back button in the same top-left position. | n/a | n/a | Not in this file | Fixed |
| 4 | 3 | Loop range can only be chosen by reading the score | Loop is fixed to bar 14, chosen for the user ("Looping bar 14"). Version B can narrow it to "Looping bar 14 · beats 1–2". No drag handles on this view. | Fixed loop | Fixed loop, can shorten | Not in this file (Practice Workspace) | Fixed (Change 3) |
| 5 | 3 | Help button moves and doesn't cover all features | "?" button ("Help for this screen") fixed top-right in both versions. The help sheet covers every control on the screen: A explains Play, Tempo, Guidance, Record; B explains Play, Record and how the coach changes settings. It is a bottom sheet, not the dimmed spotlight overlay described in the fix. | Covers all 4 controls | Covers all controls + coach rules | Partial | Not fixed (help removed) |
| 6 | 3 | No warning when audio doesn't match score | Not in this file. | n/a | n/a | Not in this file | Deferred (hard scenario) |
| 7 | 3 | No way to fix a mistake mid-take | The drill records only bar 14, so a mistake costs one bar, not the whole take. Version B's "Shorten the passage" narrows it further to beats 1 and 2. This is passage-level re-recording. | Bar 14 only | Bar 14 or beats 1–2 | Partial | Deferred |
| 8 | 3 | Feedback scores have no explanation | Checking sheet says "Listening for pitch and timing in bar 14". The badge names the issue ("late entry"). The result is only "Missed. Try again." (A) or "Not quite. Same settings, once more." (B), with no reason. Metric tooltips belong on Take Feedback. | Result text only | Coach message only | Partial | Fixed (tooltips, labels) |
| 9 | 3 | No indication the recording is clean | While recording, the only signal is a blinking red "Recording" dot. No input-level meter. | None | None | Gap | Fixed (simulated meter) |
| 10 | 2 | Manual sync gives limited visual feedback | Not in this file. | n/a | n/a | Not in this file | Deferred |
| 11 | 2 | No error state for mistyped search | Not in this file. | n/a | n/a | Not in this file | Deferred |
| 12 | 2 | Unable to add a song to a playlist | Not in this file. | n/a | n/a | Not in this file | Deferred |
| 13 | 2 | Song title field has no required indicator | Not in this file. | n/a | n/a | Not in this file | Deferred |
| 14 | 2 | AI Coach can only reference one take | Attempt history shows the last 6 attempts with tempo, guidance and result, so progress across attempts is visible without remembering it. B's coach message reacts to the run of attempts ("1 of 2 clean on your own. One more like that."). | History chips | History chips + coach message | Pattern applied | Deferred |
| 15 | 2 | First setup screen doesn't show progress | Both: goal slots change from "Attempt 1" / "Attempt 2" to "Clean 1" / "Clean 2". B: "Step 1 of 3 · Guided, slower" with a 3-segment progress bar. | Goal slots | Goal slots + step indicator | Pattern applied | Fixed (step indicator) |
| 16 | 2 | Voice range dropdown purpose unclear | Not in this file. The part is shown as plain text, "Song A · Soprano". | n/a | n/a | Not in this file | Deferred |
| 17 | 2 | Tempo slider makes exact BPM hard | A: − / + buttons in 5% steps plus a slider (50% to 100%, step 5), with a live readout such as "77 BPM · 80%". No typed BPM input. B: tempo is read-only and set by the coach, which is the independent variable, so the fix doesn't apply. | Partial | n/a by design | Partial (A) | Deferred |
| 18 | 2 | Keyboard toggle has no on/off state | No keyboard on this view. A's Guidance switch shows the word "On" or "Off" next to the switch and sets `aria-pressed`. B shows Guidance "On" / "Off" as read-only text. | Visible state | Visible state | Pattern applied | Deferred |
| 19 | 0 | Record icon may not be recognised | "Record attempt" pairs a filled dot with a text label. | Same | Same | Consistent with keep-icon decision | Kept |
| 20 | 0 | Align Score buttons don't function | Not in this file. On the Drill, all main controls work, **but the header back button and "Continue" on "Bar 14 mastered" do nothing** (see Gap 6). | Same | Same | Gap (dead buttons) | Fixed |

**Counts for this file:** 0 fully fixed, 6 partial (#1, #2, #5, #7, #8, #17), 4 pattern applied (#14, #15, #18, #19), 2 gaps (#9, #20 type), 8 not in this file (#3, #4, #6, #10 to #13, #16).

---

## 3. Gaps and inconsistencies to fix

1. **HE #2 regression: pause loses the place on screen.** Pausing removes the `ph-run` class from the playhead. The CSS hides the playhead (`.ph` has `opacity: 0`) and restarts its animation from the start of bar 14 on resume. The help text promises "it keeps your place", so the design repeats the Sev 4 problem we said we fixed. Suggested fix: keep the class and set `animation-play-state: paused`. Also, the playhead moves at a fixed 2.4 s per bar whatever the tempo, so at 60% it runs ahead of the audio.
2. **Label mismatch for ending a recording.** Iter2.03 Change 2 says the button is relabelled "End take". The Drill says "Finish attempt". Pick one term and use it on every view, the Changes doc and the experiment script.
3. **Iter2.03 under-claims #5 and #7.** It lists #5 as not fixed and #7 as deferred, but the Drill partly fixes both (fixed help button with full coverage; passage-level re-record). Either update Iter2.03 to "partially addressed on the Drill view" or remove the help sheet to match the doc. Keeping the help is the better option, since it is already built.
4. **Iter2.03 over-claims #9.** It says a simulated input meter was added, but the Drill records with only a red dot. Add the same simulated meter here, or state in Iter2.03 that it appears only on Sing Along.
5. **HE #8 on the Drill: "Missed" gives no reason.** A user who misses twice doesn't know if the problem was pitch or timing. Suggested: name the failed dimension, e.g. "Missed: entered late on beat 1". In Version B this also matters for the Adjust sheet, which suggests a change without saying why.
6. **Dead buttons.** The header back button and "Continue" on "Bar 14 mastered" have no handler. collab.md §5 requires a "this isn't part of the prototype" message with a way back instead of dead buttons, and dead buttons are what evaluators flagged as #20.
7. **Experiment validity: MODERATOR ONLY buttons.** Each attempt is judged by someone tapping Clean or Missed. The Iteration 2 brief requires the experiment to be automated with no team intervention. Before this screen goes into Iter2.05, replace the moderator step with a scripted result (for example, a fixed sequence of outcomes per attempt) or let participants self-report, and declare the choice as a limitation.
8. **Open question from Iter1.5 #8.** The revised HE still asks whether the scorecard has 3 metrics (Pitch Accuracy, Timing, Held Notes) or 4 (pitch, rhythm, timing, diction). The Drill checks only pitch and timing. Decide the metric set and make Take Feedback, the Drill and Iter2.04 agree.

---

## 4. Suggested rows for the repo CLAUDE.md

For the "Heuristic evaluation changes implemented" table (collab.md §1). Only rows with something on the Drill view are listed.

| HE # | Severity | Change in prototype | View(s) | Iter2.03 section |
|---|---|---|---|---|
| 1 | 4 | Attempt history chips keep every drill attempt visible (autosave, save, discard still to build on Take Feedback) | Drill A, B | Change 1 |
| 2 | 4 | Single "Play bar 14" / "Pause" toggle; separate "Finish attempt" button (playhead still resets on pause, see Gap 1) | Drill A, B | Change 2 |
| 5 | 3 | Fixed top-right help button; help sheet covers every control on the Drill | Drill A, B | Not fixed list (needs update) |
| 7 | 3 | Drill re-records bar 14 only; B can shorten to beats 1–2 | Drill A, B | Not fixed list (needs update) |
| 8 | 3 | Checking sheet names what is judged (pitch and timing); result lacks a reason | Drill A, B | Smaller fixes |
| 15 | 2 | Goal slots and B's "Step 1 of 3" indicator | Drill A, B | Smaller fixes (pattern) |
| 17 | 2 | − / + buttons with BPM and % readout beside the slider | Drill A | Not listed |
| 18 | 2 | Guidance switch shows "On" / "Off" | Drill A | Not listed |

---

## 5. Updated design (21 Oct 2026)

The table above describes the **12 Oct** design. `ResoNote Hi-Fi Drill (HE fixes).html` in this folder rebuilds both Drill versions with these fixes:

| Gap above | HE # | What the 21 Oct file does |
|---|---|---|
| 1 | 2 | Pause keeps the playhead on the same beat (shown dashed); the button reads "Resume" and continues from there. Playhead speed follows the tempo. |
| 2 | 2 | "Finish attempt" renamed "End take"; "attempt" renamed "take" throughout. |
| (new) | 1 | "Autosaved · n takes" label; latest take has "Play back take #n" and "Discard take" with a confirmation sheet. Discarding undoes the take's effect on the goal and, in B, on the coach's settings. |
| 4 | 9 | Simulated live input-level meter with "Voice picked up · good level" while recording. |
| 5 | 8 | Moderator marks "Missed: timing" or "Missed: pitch"; the result, history chip and B's Adjust sheet all state the reason. |
| 3 | 5 | Help button fixed top-right opens a step-by-step overlay: screen dimmed, control outlined, tip placed beside it. |
| (new) | 17 | Version A only: tap the BPM value to type 48 to 96, with an inline error for other values; slider moves in 1 BPM steps. |
| 6 | 20 | Back and "Continue" show "This button isn't part of the prototype" instead of doing nothing. |

**Still open:** Gap 7 (MODERATOR ONLY judging still needs a team member) and Gap 8 (3 vs 4 scorecard metrics). Gap 3 also still needs Iter2.03 updating, since the Drill now partly fixes #5 and #7.

---

## 6. Next check

Rerun this mapping when the other views are exported, especially Practice Workspace (#2, #4, #17, #18), Take Feedback (#1, #8, #14) and Sing Along (#9), since those carry the three graded changes in Iter2.03.
