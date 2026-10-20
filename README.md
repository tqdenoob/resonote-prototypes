# ResoNote parallel prototypes (G1T2)

Three parallel UI designs for ResoNote's Iteration 2 easy scenario. They are static screens only, with no app logic.

| Folder | Design | Idea |
|---|---|---|
| `design-a/` | Score-first | Sheet music is the workspace; loops and mistakes are marked on the score |
| `design-b/` | Timeline-first | No score; colour-coded waveform of song sections plus lyrics |
| `design-c/` | Coach-first | The AI coach runs the session as a chat |

Each design has the same 10 screens: Library, Import, Pick part, Sync check, Practice workspace, Recording, Scorecard, Understand the issue, Drill, Session summary.

## Viewing

Open `index.html` in a browser. No install or build step is needed.

## Editing

- Every screen is a `<figure class="shot">` block in that design's `index.html`, with a comment above it (`<!-- 5 Workspace -->`). Edit the HTML inside `.screen`.
- Colours and fonts for each design are at the top of its `style.css` (`:root` variables).
- `shared/board.css` holds the phone frame and page layout used by all three designs.
- Design A: score lines are SVG symbols (`#line37`, `#line41`, `#line45`) near the top of `design-a/index.html`. Edit them once and every screen updates.
- Design B: the song sections are the `#sections` symbol near the top of `design-b/index.html`. The waveform bar shapes in the masks are generated data and are fine to leave alone.
- Captions under each phone explain the screen. The yellow/pink tags list which Iteration 1 heuristic evaluation problems it fixes.

## Hosting

The site is served with GitHub Pages from the `main` branch root. Pushing to `main` updates the live site within a minute or two.

## Notes

- "Northern Lights", the lyrics and every score are made-up placeholder data, not real user results.
- These designs were drafted with Claude (AI). Declare this in the Iteration 2 Journal, along with what the team changed.
