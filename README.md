# ResoNote prototypes (G1T2)

IS211 Interaction Design and Prototyping, Iteration 2.

**Live:** https://tqdenoob.github.io/resonote-prototypes/

| Path | What it is |
|---|---|
| `index.html` | **Prototype 2.0: the full high-fidelity prototype.** 11 clickable views covering the Iteration 2 easy scenario (Clarence learns the tenor part of "Viva La Vida"). |
| `parallel-designs.html` | The three parallel UI designs from 20 Oct (static screens). |
| `design-a/`, `design-b/`, `design-c/` | Score-first, timeline-first and coach-first designs. |
| `alternatives/` | Earlier designs kept for the Journal, e.g. the 21 Oct drill with HE fixes. |
| `docs/` | Revised Iter1.5 heuristic evaluation and the HE-to-drill traceability notes. |
| `CLAUDE.md` | Current prototype state, navigation map, simulation, HE fixes, A/B, decision and AI logs. **Update it in every PR.** |
| `collab.md` | How the team works in this repo. |

## Viewing the prototype

Open `index.html` in a browser, or the live link. No install or build step.

- The panel next to the phone lists every view and its HE fixes, and jumps to any view.
- Direct links: add a view name after `#`, e.g. `#workspace`, `#feedback`, `#drill`.
- Drill version: add `?v=A` or `?v=B`, e.g. `?v=A#drill`.
- Sound plays after your first tap. Turn your volume up.

## Editing the prototype

`index.html` is one self-contained file. Scripted data (tenor notes, feedback scores, drill results) is at the top of the `<script>`. Each view is a function in `SCREENS`. Colours are `:root` tokens at the top of the `<style>`, with a dark theme.

## Editing the parallel designs

- Every screen is a `<figure class="shot">` block in that design's `index.html`, with a comment above it (`<!-- 5 Workspace -->`). Edit the HTML inside `.screen`.
- Colours and fonts for each design are at the top of its `style.css` (`:root` variables).
- `shared/board.css` holds the phone frame and page layout used by all three designs.
- Design A: score lines are SVG symbols (`#line37`, `#line41`, `#line45`) near the top of `design-a/index.html`.
- Design B: the song sections are the `#sections` symbol near the top of `design-b/index.html`.

## Hosting

GitHub Pages serves the `main` branch root. Merging to `main` updates the live site within a minute or two.

## Notes

- All song data, scores and coach feedback are scripted placeholders, not real user results. "Northern Lights" in the parallel designs is made up.
- Drafted with Claude (AI). Declare this in the Iteration 2 Journal, along with what the team changed. See the AI assistance log in `CLAUDE.md`.
