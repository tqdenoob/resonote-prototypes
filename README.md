# ResoNote prototypes (G1T2)

IS211 Interaction Design and Prototyping, Iteration 2.

**Live:** https://tqdenoob.github.io/resonote-prototypes/

**There is one design: `index.html`.** Every change goes into it. Don't add parallel copies or new design files; keep old versions as screenshots in `docs/screenshots/alternatives/`.

| Path | What it is |
|---|---|
| `index.html` | **Prototype 2.0: the full high-fidelity prototype.** 11 clickable views covering the Iteration 2 easy scenario (Clarence learns the tenor part of "Viva La Vida"). |
| `docs/screenshots/alternatives/` | Screenshots of the designs we dropped (20 Oct parallel designs, 21 Oct drill, 26 Oct A/B drill), for the Journal. The code is in git history before PR #4. |
| `docs/` | Revised Iter1.5 heuristic evaluation and the HE-to-drill traceability notes. |
| `CLAUDE.md` | Current prototype state, navigation map, simulation, HE fixes, A/B, decision and AI logs. **Update it in every PR.** |
| `collab.md` | How the team works in this repo. |

## Viewing the prototype

Open `index.html` in a browser, or the live link. No install or build step.

- The panel next to the phone lists every view and its HE fixes, and jumps to any view.
- Direct links: add a view name after `#`, e.g. `#workspace`, `#feedback`, `#drill`.
- Sound plays after your first tap. Turn your volume up.

## Editing the prototype

`index.html` is one self-contained file. Scripted data (tenor notes, feedback scores, drill results) is at the top of the `<script>`. Each view is a function in `SCREENS`. Colours are `:root` tokens at the top of the `<style>`. The app is light mode only.

## Hosting

GitHub Pages serves the `main` branch root. Merging to `main` updates the live site within a minute or two.

## Notes

- All song data, scores and coach feedback are scripted placeholders, not real user results.
- Drafted with Claude (AI). Declare this in the Iteration 2 Journal, along with what the team changed. See the AI assistance log in `CLAUDE.md`.
