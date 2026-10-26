# Iter1.5 Heuristic Evaluation (Revised)

**G1T2 · ResoNote**

Revised version of our Iteration 1 heuristic evaluation, prepared on 21 Oct 2026. It keeps the problems, sources and severity ratings the team agreed in Week 6, and corrects the inconsistencies found after grading. See the [Revision log](#revision-log) at the end for every change.

---

## Contents

**Severity 4: Usability catastrophe**

1. [Missing take actions and recovery controls](#1-missing-take-actions-and-recovery-controls)
2. [Pause and stop controls reset playback to 0:00 and are easily confused](#2-pause-and-stop-controls-reset-playback-to-000-and-are-easily-confused)

**Severity 3: Major usability problem**

3. [Users cannot return to previous setup steps from the Sync Check screen](#3-users-cannot-return-to-previous-setup-steps-from-the-sync-check-screen)
4. [Loop range can only be chosen by reading the score](#4-loop-range-can-only-be-chosen-by-reading-the-score)
5. [Help button moves between pages and does not cover all features](#5-help-button-moves-between-pages-and-does-not-cover-all-features)
6. [No warning if the audio file does not match the score file](#6-no-warning-if-the-audio-file-does-not-match-the-score-file)
7. [No way to fix a mistake mid-take without redoing the recording](#7-no-way-to-fix-a-mistake-mid-take-without-redoing-the-recording)
8. [Feedback scores have no explanation](#8-feedback-scores-have-no-explanation)
9. [No indication that the recording is clean](#9-no-indication-that-the-recording-is-clean)

**Severity 2: Minor usability problem**

10. [Manual sync gives limited visual feedback when adjusting the alignment](#10-manual-sync-gives-limited-visual-feedback-when-adjusting-the-alignment)
11. [No error state for an incorrectly typed song title in search](#11-no-error-state-for-an-incorrectly-typed-song-title-in-search)
12. [Unable to add a song to a playlist](#12-unable-to-add-a-song-to-a-playlist)
13. [Import screen's "Song title" field has no required indicator](#13-import-screens-song-title-field-has-no-required-indicator)
14. [AI Coach can only reference one take at a time](#14-ai-coach-can-only-reference-one-take-at-a-time)
15. [The first setup screen does not show the user's progress](#15-the-first-setup-screen-does-not-show-the-users-progress)
16. [The purpose of the voice range dropdown is unclear](#16-the-purpose-of-the-voice-range-dropdown-is-unclear)
17. [Tempo slider makes it hard to set an exact BPM](#17-tempo-slider-makes-it-hard-to-set-an-exact-bpm)
18. [Keyboard toggle does not have an on/off indication](#18-keyboard-toggle-does-not-have-an-onoff-indication)

**Severity 0: Not a real usability problem**

19. [Record button icon may not be recognised](#19-record-button-icon-may-not-be-recognised)
20. [Align Score's Play, Set marker and Undo buttons do not function](#20-align-scores-play-set-marker-and-undo-buttons-do-not-function)

---

## Heuristics and severity ratings

| Heuristics | Severity ratings |
|---|---|
| 0. Not related to any heuristic | 0 = Not a real usability problem |
| 1. Visibility of system status | 1 = Cosmetic problem only |
| 2. Match between system and the real world | 2 = Minor usability problem |
| 3. User control and freedom | 3 = Major usability problem |
| 4. Consistency and standards | 4 = Usability catastrophe |
| 5. Error prevention | |
| 6. Recognition rather than recall | |
| 7. Flexibility and efficiency of use | |
| 8. Aesthetic and minimalist design | |
| 9. Help users recognize, diagnose, and recover from errors | |
| 10. Help and documentation | |

**How we rated severity.** Each rating weighs three factors: **impact** (does the problem block the task, slow it down, or only confuse briefly), **frequency** (how often a user in our easy scenario meets it) and **persistence** (whether a workaround exists once the user knows about it). Where we changed an evaluator's rating, the Notes state which of these factors drove the change.

## Evaluators (G1T3)

- [Jarrett Chan](https://drive.google.com/file/d/1JNxDVe0Xw_PF1KXQJOjksUET7HLVYIBI/view?usp=drive_link) (A)
- [Jayden Khoo](https://drive.google.com/file/d/1GNhg7LPOs0VF_2U1U2GlzWBmbEVLEKro/view?usp=drive_link) (B)
- [Nee Wei Xun](https://docs.google.com/document/d/1DrzWTS6_zQELjfGQcuFjOt8pA171XnS6/edit?usp=drive_link&ouid=117854515684283249094&rtpof=true&sd=true) (C)
- [Teh Bo Yan](https://drive.google.com/file/d/1sHpLzaWiRT2AYFXAWustp8gx2IpvLOxj/view?usp=drive_link) (D)
- [Wong Jia Xuan Mabel](https://docs.google.com/document/d/1whtHinmJ5gH_0B502JWBM2VlxIuSe_Lb/edit?usp=drive_link&ouid=117854515684283249094&rtpof=true&sd=true) (E)

> The A to E letters are our mapping of evaluators to source codes. Confirm it against the original evaluator files before reuse.

## Summary

| # | Problem | Source(s) | Heuristic(s) | Original | Final |
|---|---|---|---|---|---|
| 1 | Missing take actions and recovery controls | B1 | 1, 3, 5 | 4 | **4** |
| 2 | Pause and stop controls reset playback and are easily confused | B3, D2, E5 | 1, 3, 4 | 3 | **4** |
| 3 | No back button on Sync Check | A2 | 3 | 3 | **3** |
| 4 | Loop range can only be chosen by reading the score | C3, D5 | 2, 3, 6, 7 | 3 | **3** |
| 5 | Help button moves and does not cover all features | B5, C4 | 4, 10 | 3 | **3** |
| 6 | No warning when audio does not match score | C5 | 1, 5, 9 | 3 | **3** |
| 7 | No way to fix a mistake mid-take | E1 | 3, 6 | 3 | **3** |
| 8 | Feedback scores have no explanation | A5, E3 | 2, 6, 10 | 3 | **3** |
| 9 | No indication the recording is clean | E4 | 1, 5 | 3 | **3** |
| 10 | Manual sync gives limited visual feedback | A1 | 1 | 3 | **2** |
| 11 | No error state for mistyped search | C2 | 1, 9 | 3 | **2** |
| 12 | Unable to add a song to a playlist | D1 | 3, 7 | 3 | **2** |
| 13 | Song title field has no required indicator | D3 | 5 | 3 | **2** |
| 14 | AI Coach can only reference one take | E2 | 2, 6, 7 | 3 | **2** |
| 15 | First setup screen does not show progress | A3 | 1 | 2 | **2** |
| 16 | Voice range dropdown purpose unclear | A4 | 10 | 2 | **2** |
| 17 | Tempo slider makes exact BPM hard | B4 | 3, 7, 8 | 2 | **2** |
| 18 | Keyboard toggle has no on/off state | D4 | 1 | 2 | **2** |
| 19 | Record button icon may not be recognised | B2 | 2, 4, 6 | 3 | **0** |
| 20 | Align Score buttons do not function | C1 | 1, 3, 5 | 4 | **0** |

**Counts:** 20 problems from 25 evaluator findings (A1 to E5, each used once). 2 Severity 4, 7 Severity 3, 9 Severity 2, 2 Severity 0. 8 ratings changed (1 raised, 7 lowered).

---

## Compiled usability problems

### 1. Missing take actions and recovery controls

**Source(s):** B1
**Heuristic(s):** 1. Visibility of system status, 3. User control and freedom, 5. Error prevention
**Severity:** 4 = Usability catastrophe

**Description:** The take feedback screen (View 8) has no clear primary call-to-action to re-record, save or discard the take. Nothing tells the user whether the take has been saved, so accidentally leaving the app could permanently lose the recording and its feedback.

**Fix:**
1. Rename "Repeat passage" to "Re-record passage" so users immediately understand that it returns to the recording screen.
2. Autosave the latest take as a draft, shown by a visible "Autosaved" indicator, so a misclick or app exit does not lose it. Add a "Save to history" button for users who want to keep the take permanently.
3. Add a "Discard take" button that clears the recording and its metrics after a short confirmation.

**Notes:** We agree with Severity 4. Recording a take is the core loop of ResoNote, and losing one wipes out the user's effort with no way to recover it. It affects every user who records. We will add autosave, "Save to history" and "Discard take", and rename the primary button.

---

### 2. Pause and stop controls reset playback to 0:00 and are easily confused

**Source(s):** B3, D2, E5
**Heuristic(s):** 1. Visibility of system status, 3. User control and freedom, 4. Consistency and standards
**Severity:** 4 = Usability catastrophe (raised from 3)

**Description:** On the Practice screen, pressing the play button at the bottom left starts playback and the timestamp runs (Figure 1). Pressing the square button beside it pauses playback, but the timestamp resets to 0:00 (Figure 2). We confirmed that the square icon is intended to act as pause. A filled square is the standard media symbol for "stop", which resets position, not "pause", which keeps it. Standard media players combine play and pause into one button whose icon switches with the playback state. In addition (E5), the Practice screen shows both this small square icon and a separate, larger "Stop" button, with nothing to distinguish them, so users cannot tell whether one stops playback and the other ends the recording.

**Fix:** Keep the playback position when the user pauses, and merge play and pause into one button whose icon changes with the playback state. This also removes the ambiguity of the square icon. Relabel the larger "Stop" button "End take" so it is clearly separate from playback controls.

**Notes:** We raised the severity from 3 to 4 because of frequency. Pausing to replay a tricky phrase is the most common action while learning a part, and every pause loses the user's place, so the problem repeats many times in a single session. We merged E5 (two "stop" controls on the same screen, originally rated 2) into this problem because both come from the same unclear playback controls and share one fix. We will merge play and pause into one toggle, preserve the position, and relabel "Stop" as "End take".

---

### 3. Users cannot return to previous setup steps from the Sync Check screen

**Source(s):** A2
**Heuristic(s):** 3. User control and freedom
**Severity:** 3 = Major usability problem

**Description:** The Sync Check screen is the last setup step, but it has no back or cancel button. To change the vocal part or anything else chosen earlier, users must first enter the practice or alignment screen and then navigate back or cancel. That returns them to the start of setup rather than the previous step, so they repeat the whole process.

**Fix:** Add a back button matching the one on the Import and Vocal Parts screens, so users can return one step and change an earlier choice without restarting setup.

**Notes:** We agree with Severity 3. Every new song goes through setup, and a wrong part selection forces a full restart. We will add the back button.

---

### 4. Loop range can only be chosen by reading the score

**Source(s):** C3, D5
**Heuristic(s):** 2. Match between system and the real world, 3. User control and freedom, 6. Recognition rather than recall, 7. Flexibility and efficiency of use
**Severity:** 3 = Major usability problem

**Description:** The loop section control assumes users can read musical notation to choose loop bounds. Many ResoNote users are not trained sight-readers, so the control does not match how a beginner thinks about the song. The only way to select a loop is to locate the right bars on the score, which forces users to recall and interpret notation instead of simply selecting part of a timeline. Looping is a core feature, so the impact on affected users is high. It does not block everyone, because score-literate users can still use it, and trial-and-error clicking is a slow workaround.

**Fix:** Let users set a custom loop range by dragging start and end handles on a timeline, instead of relying only on presets like bars 1-8 or bars 17-24.

**Notes:** We agree with Severity 3. The users this control excludes are exactly our primary persona, who cannot sight-read. We will add draggable handles on the timeline.

---

### 5. Help button moves between pages and does not cover all features

**Source(s):** B5, C4
**Heuristic(s):** 4. Consistency and standards, 10. Help and documentation
**Severity:** 3 = Major usability problem

**Description:** The help button appears in a different position on different pages. Users build muscle memory for where help is, and a moving button breaks that expectation each time. The help content also skips features, including the metronome and built-in keyboard on the Practice page, so users looking for guidance on those find nothing. The app still works, but the support channel fails exactly when users need it, leaving some features unsupported.

**Fix:**
1. Keep the help button in one fixed position on every page.
2. Show help as a semi-transparent, dismissible overlay so users can still see the feature underneath.
3. In the overlay, dim everything not related to the current tip, outline the targeted control with a coloured border, and place the tip next to it.
4. Cover every feature on each page, including the metronome and keyboard.

**Notes:** We agree with Severity 3. We will fix the help button's position and extend the help content to every feature. (Iteration 2 update: the tutorial and help overlay were removed from our Iteration 2 easy scenario, so this fix is deferred to when they return. See Iter2.03 Changes.)

---

### 6. No warning if the audio file does not match the score file

**Source(s):** C5
**Heuristic(s):** 1. Visibility of system status, 5. Error prevention, 9. Help users recognize, diagnose, and recover from errors
**Severity:** 3 = Major usability problem

**Description:** The app does not check whether the uploaded audio matches the uploaded score, and shows no error when they don't. Beginners who cannot sight-read have no way to tell for themselves whether the audio belongs to the score, so they are left confused about why playback looks wrong. The system proceeds as if everything is fine, hiding its true state. The app does not crash, but it produces misleading results, such as audio out of sync with the score or wrong sections being marked. In a learning tool, that undermines everything that follows.

**Fix:** Show a warning such as "This audio file doesn't seem to match the uploaded score. Playback and markers may be inaccurate." so users can re-check their files. If they proceed anyway, keep a persistent banner visible while that pair is loaded, with an option in the song's file info to re-check the pairing later.

**Notes:** We agree with Severity 3. A mismatched pair also breaks the AI Coach's feedback, because the coach compares the user's singing against the wrong reference. We will add a mismatch warning during import. (Iteration 2 update: this case occurs in our hard scenario, not the easy scenario prototyped in Iteration 2, so the fix is deferred. See Iter2.03 Changes.)

---

### 7. No way to fix a mistake mid-take without redoing the recording

**Source(s):** E1
**Heuristic(s):** 3. User control and freedom, 6. Recognition rather than recall
**Severity:** 3 = Major usability problem

**Description:** On the Practice screen, users can record only a single continuous take: no edits, rewinds or partial re-records. The only control is a stop button. The revisit passages section lets users loop and listen to their mistakes, but not re-record those bars; pressing "Repeat passage" starts a completely new recording. A single mistake anywhere in an 8-bar loop forces the singer to discard the whole take, restart from bar 1 and remember the earlier mistakes themselves. This directly affects the core practice activity and makes long loops tedious, which over time could make users abandon the tool.

**Fix:** In the revisit passages section, after a flagged passage is identified, offer "Re-record this passage" so users can redo just the affected bars without deleting the whole take. TikTok's segmented recording is a familiar model: each segment can be redone without discarding the rest.

**Notes:** We agree with Severity 3. Redoing an entire take for one mistake wastes effort on every recording and is demotivating. We will add passage-level re-recording from the flagged passages list. (Iteration 2 update: deferred, as segmented editing is outside the Iteration 2 easy scenario. See Iter2.03 Changes.)

---

### 8. Feedback scores have no explanation

**Source(s):** A5, E3
**Heuristic(s):** 2. Match between system and the real world, 6. Recognition rather than recall, 10. Help and documentation
**Severity:** 3 = Major usability problem

**Description:** After a recording, the feedback screen shows Pitch Accuracy, Timing and Held Notes as three equally weighted bars, with no explanation of what each metric means. Beginners unfamiliar with music terms cannot tell what to work on unless they ask the AI Coach about each metric one by one in the chat, which is slow and tedious.

**Fix:**
1. Add an (i) tooltip to each metric explaining it in plain language: pitch accuracy means singing the correct notes, timing means singing at the right moment, and held notes means sustaining notes for their full length.
2. Show a simple performance label next to each score, such as "Needs work", "Good" or "Excellent", based on the app's scoring criteria.

**Notes:** We agree with Severity 3. Every user sees this screen after every take, and unexplained numbers stop beginners from knowing how to improve, which is the purpose of the screen. We will add tooltips and performance labels.

---

### 9. No indication that the recording is clean

**Source(s):** E4
**Heuristic(s):** 1. Visibility of system status, 5. Error prevention
**Severity:** 3 = Major usability problem

**Description:** During recording, nothing shows whether the user's voice is being picked up or whether background noise is distorting the take. Users only find out afterwards, when they play the take back (we confirmed this behaviour). If their voice is too soft, not captured at all, or drowned out by a sudden noise, the whole effort is wasted. For an app built around repeated recordings, this is especially frustrating.

**Fix:** Show a live input-level meter (for example, a waveform of the user's voice) throughout recording, not just on playback, so users can see straight away whether their voice is being captured and whether it is too soft, too loud or masked by noise. Background noise suppression can be added alongside it.

**Notes:** We agree with Severity 3. A failed take is only discovered after the user has finished singing, and nothing warns them in time to stop and retry. We will add a live input-level meter to the recording screen.

---

### 10. Manual sync gives limited visual feedback when adjusting the alignment

**Source(s):** A1
**Heuristic(s):** 1. Visibility of system status
**Severity:** 2 = Minor usability problem (lowered from 3)

**Description:** The Manual Sync screen asks users to "slide the audio until the first note lands on bar 1". Moving the slider changes only the offset value (for example "-0.42 s"); the waveform and score stay still. Users get little visual sense of how their adjustment changes the alignment, so it is harder to tell when the first note lines up with bar 1.

**Fix:** Move the recording waveform against the score as the user drags the slider, with a fixed vertical marker at bar 1 as a reference point.

**Notes:** We lowered the severity from 3 to 2 because a workaround exists: the offset value updates live, so users can still align by adjusting it and listening. Manual sync is also only needed when automatic sync fails, so most users rarely see this screen. We will link the waveform to the slider.

---

### 11. No error state for an incorrectly typed song title in search

**Source(s):** C2
**Heuristic(s):** 1. Visibility of system status, 9. Help users recognize, diagnose, and recover from errors
**Severity:** 2 = Minor usability problem (lowered from 3)

**Description:** When a user mistypes a song title in the library search, the results area simply stays blank. The system does not say whether the problem is a spelling mistake or that the song is not in the library, and without a message the user cannot even be sure the search ran, rather than the app freezing. Typos are common, so users will meet this regularly.

**Fix:** Show a "No results found" message whenever a search returns nothing. Suggest songs with similar titles, and consider adding spell-check to the search field (Figure 3).

**Notes:** We lowered the severity from 3 to 2. Users meet the problem often, but its impact is low: the library holds only songs the user has uploaded, so they can clear the search and scroll the list to find the song. Retyping fixes the problem as soon as they notice the typo. We will add a "No results found" state, with title suggestions and spell-check as later improvements.

---

### 12. Unable to add a song to a playlist

**Source(s):** D1
**Heuristic(s):** 3. User control and freedom, 7. Flexibility and efficiency of use
**Severity:** 2 = Minor usability problem (lowered from 3)

**Description:** Opening a song from the library (Figure 4) shows its details, such as bars, parts and the keyboard (Figure 5), but there is no way to add the song to a playlist. Users who learn many songs across concerts or semesters have no way to organise them.

**Fix:** Add an "Add to playlist" button at the top of the song page, next to the Coach button (Figure 6).

**Notes:** We lowered the severity from 3 to 2. Without playlists, users cannot organise their library, but they can still find, open and practise any song, which is the core task. The impact grows as the library grows, so it matters more for long-term users than for someone learning a few songs for one concert. We will add "Add to playlist" on the song page.

---

### 13. Import screen's "Song title" field has no required indicator

**Source(s):** D3
**Heuristic(s):** 5. Error prevention
**Severity:** 2 = Minor usability problem (lowered from 3)

**Description:** On the Import screen, both file upload fields are labelled, and the Next button stays disabled until a score file is uploaded (Figure 7). The "Song title" text box below them has no label or validation, so it is unclear whether it is required or optional. The song title is how the song is identified everywhere else in the app, including playlists and search, so letting a user continue without one creates a problem that is harder to notice and fix later.

**Fix:** Mark the field "Required" to match the file fields (Figure 8), keep the Next button disabled until a title is entered, and show an inline message below the field asking the user to enter a song title (Figure 9).

**Notes:** We lowered the severity from 3 to 2. Users see the Import screen once per song, and nothing breaks at that point. The cost shows up later, when an untitled song is hard to find in search or playlists. We will add the required label, block Next until a title is entered, and add an inline message.

---

### 14. AI Coach can only reference one take at a time

**Source(s):** E2
**Heuristic(s):** 2. Match between system and the real world, 6. Recognition rather than recall, 7. Flexibility and efficiency of use
**Severity:** 2 = Minor usability problem (lowered from 3)

**Description:** The AI Coach analyses one take per conversation, and there is no way to add a second take to the same conversation. Users cannot ask the coach to compare their previous take with the new one, so they must remember earlier feedback themselves or keep notes to tell whether they have improved.

**Fix:** Allow multiple takes in the same AI Coach conversation, so the coach can compare the new take with earlier ones and point out what has improved. Show takes side by side to make progress visible.

**Notes:** We lowered the severity from 3 to 2. Each take still receives complete feedback, so users can always find out what to fix next, which is the coach's main job. What users lose is comparison across takes: tracking improvement means remembering or writing down earlier feedback. That effort grows as users record more takes of the same passage, so the problem matters most for long practice sessions. We will add multi-take comparison to the coach conversation.

---

### 15. The first setup screen does not show the user's progress

**Source(s):** A3
**Heuristic(s):** 1. Visibility of system status
**Severity:** 2 = Minor usability problem

**Description:** The Vocal Parts screen shows "Step 2 of 3" and the Sync Check screen shows "Step 3 of 3", but the Import screen does not show "Step 1 of 3". Users therefore don't know how many steps setup involves when they begin.

**Fix:** Add "Step 1 of 3" to the Import screen, with the same placement and styling as the other two setup screens.

**Notes:** We agree with Severity 2. Users are briefly unsure how long setup will take, but it does not stop them progressing, and the indicator appears from step 2 onwards. We will add the indicator to the Import screen.

---

### 16. The purpose of the voice range dropdown is unclear

**Source(s):** A4
**Heuristic(s):** 10. Help and documentation
**Severity:** 2 = Minor usability problem

**Description:** On the Vocal Parts screen, each part has a dropdown with options such as "High voice", "Medium voice" and "Low voice", but no label explains what it is for. The instructions only ask users to name each part and select the part they sing, so users may not know why they are choosing a voice range or how it affects practice.

**Fix:** Add a "Voice range" label above the dropdown, with a short explanation such as "Select the approximate vocal range for this part". Alternatively, add an information icon that opens a tooltip.

**Notes:** We agree with Severity 2. Users can still choose a value and continue, but an unexplained choice may lead to a wrong selection. We will add the label and tooltip.

---

### 17. Tempo slider makes it hard to set an exact BPM

**Source(s):** B4
**Heuristic(s):** 3. User control and freedom, 7. Flexibility and efficiency of use, 8. Aesthetic and minimalist design
**Severity:** 2 = Minor usability problem

**Description:** On the Practice screen, users can adjust the tempo with a slider, but landing on an exact BPM value is fiddly and slow. Tempo is adjusted often while learning a fast passage, so this small frustration repeats and builds up.

**Fix:**
1. Make the BPM value tappable. Tapping it opens a number input; the user types a value, taps Done, and returns to the Practice screen.
2. Keep the slider, and let users set the step size (for example 1, 5 or 10 BPM) so it moves in larger increments when needed.

**Notes:** We agree with Severity 2. Users can still reach the tempo they want, but each adjustment takes longer than it should. We will add a typed BPM input alongside the slider.

---

### 18. Keyboard toggle does not have an on/off indication

**Source(s):** D4
**Heuristic(s):** 1. Visibility of system status
**Severity:** 2 = Minor usability problem

**Description:** On the song page, the button above the keyboard toggles it on and off (Figure 10). The button looks the same in both states, so users cannot tell whether it is on or off. When the keyboard is hidden, it is also unclear what the button does, and users are likely to work it out only through trial and error (Figure 11).

**Fix:** Turn the toggle into a single button whose label and appearance switch between "Keyboard: On" and "Keyboard: Off" depending on its state.

**Notes:** We agree with Severity 2. The keyboard appearing or disappearing gives immediate feedback once the button is pressed, but users have to try it to find out what it does. We will add a visible on/off state.

---

### 19. Record button icon may not be recognised

**Source(s):** B2
**Heuristic(s):** 2. Match between system and the real world, 4. Consistency and standards, 6. Recognition rather than recall
**Severity:** 0 = Not a real usability problem (lowered from 3)

**Description:** The voice recording button on the chat page is a filled circle inside another circle. The evaluator suggested this is not a common icon and that users may not recognise it, since apps such as WhatsApp and voice recorders use a microphone icon.

**Fix (proposed by evaluator):** Replace it with a microphone icon.

**Notes:** We lowered the severity from 3 to 0. A filled circle inside a ring is the standard record symbol in smartphone camera apps, voice memo apps and digital audio workstations, so it matches users' expectations. We will keep the current icon.

---

### 20. Align Score's Play, Set marker and Undo buttons do not function

**Source(s):** C1
**Heuristic(s):** 1. Visibility of system status, 3. User control and freedom, 5. Error prevention
**Severity:** 0 = Not a real usability problem (lowered from 4)

**Description:** On the Align Score screen, the Play, Set marker and Undo buttons do nothing when pressed. They control the app's primary alignment function, so in a working app this would stop users completing the task.

**Fix (intended behaviour):**
- **Play:** plays the audio, moves the progress indicator along the score, and switches its icon to pause.
- **Set marker:** places a visible marker on the timeline at the selected point.
- **Undo:** visibly reverses the last action.

**Notes:** We lowered the severity from 4 to 0. Our low-fidelity prototype only simulated navigation between views, so these controls were never interactive during the evaluation. This is a limitation of the prototype's fidelity, not a usability problem in the design. The intended behaviour above is implemented in the Iteration 2 high-fidelity prototype.

---

## Figures

The original document's figures were numbered before the problems were sorted by severity, so they appeared out of order. They are renumbered here in document order. Re-insert the images from the original Iter1.5 file under their new numbers.

| New figure | Problem | Shows | Original figure |
|---|---|---|---|
| 1 | #2 | Playback running with timestamp | 6 |
| 2 | #2 | Timestamp reset to 0:00 after pause | 7 |
| 3 | #11 | Example "No results found" fix | unnumbered image |
| 4 | #12 | Library with song selected | 1 |
| 5 | #12 | Song page without playlist option | 2 |
| 6 | #12 | Proposed "Add to playlist" button | 3 |
| 7 | #13 | Next disabled without a score file | 10 |
| 8 | #13 | Proposed "Required" label | 11 (check) |
| 9 | #13 | Proposed disabled Next with inline message | 12 |
| 10 | #18 | Keyboard shown, toggle active | 14 |
| 11 | #18 | Keyboard hidden, toggle unclear | 15 |

---

## Revision log

Changes from the submitted Iter1.5, made after Prof Ben's Iteration 1 feedback and our own review on 21 Oct 2026.

**Feedback from Prof Ben addressed**
- **#11:** removed "The severity of this issue is a 3" from the description, which contradicted the final rating of 2. The downgrade is now justified by impact and workaround, without the defensive line "a search with no results means there are indeed no results".
- **#12:** removed "high-frequency gap", "no workaround available" and "blocks an entire task category" from the description, which argued for a higher rating than the final 2. The note now explains the downgrade by impact on the core task, without "should not hinder".
- **#13:** replaced "users can deduce the solution quickly" with an objective justification (seen once per song, nothing breaks at that point). Fixed the note's claim that Next is disabled when the title is empty; per the description, Next is only gated on the score file.
- **#14:** removed "The severity is major" from the description and replaced "more of a missing feature than a major usability problem" with a justification based on what users can and cannot still do.

**Consistency fixes**
- **Contents:** previously almost every entry linked to the same heading anchor; each now links to its own section.
- **Figures:** renumbered in document order, with a mapping table. #13's fix previously cited "figure 12" twice.
- **Severity labels:** capitalised consistently ("Major usability problem", "Minor usability problem").
- **Heuristic numbers:** now listed in ascending order for every problem (e.g. #6 was "5, 9, 1").
- **Spelling:** "Al Coach" corrected to "AI Coach" in #6; heuristic 9 consistently spelt "recognize" to match the table.
- **#1:** added heuristic 1 (Visibility of system status), since the description explicitly covers the missing "saved" signal.
- **#5:** heuristic 8 removed (the problem is about position and coverage, not visual clutter); the fix list is now numbered and introduced properly.
- **#7, #8, #9:** notes now state the planned action, consistent with #1 to #6.
- **#17:** rewrote the fix to remove the sentence fragment ("Which will return them...") and the unclear "song title page".
- **Notes on #5, #6, #7:** added Iteration 2 updates so they agree with Iter2.03 Changes, which defers these fixes.
- Added a summary table, a severity rating method, and a problem-to-figure mapping.

**Still to check against source files**
- **#8:** the evaluator saw three metrics (Pitch Accuracy, Timing, Held Notes), but Iter1.4 Prototype, View 8, says the scorecard grades four dimensions (pitch, rhythm, timing, diction). Confirm which is correct and make Iter2.04 Prototype match.
- **Evaluator letters A to E:** our assumed mapping of evaluators to source codes; verify against the original evaluator files.
- **Figure 8:** the original number is assumed to be 11.
