# Pull Request #1

Ask someone out as if it were a code review.

They open the link, a terminal boots, and a pull request appears:
`feat: add <them> to my Friday night` — one commit into `main`, with a diff,
CI checks, and two review buttons.

`Approve & merge` works. `Request changes` does not. It breaks out of the
layout, goes `position: fixed`, and runs from the cursor while relabelling
itself (`merge conflict`, `CI failed`, `npm ERR! peer dep missing`,
`branch protection enabled`). After fifteen escapes it gives up, turns green,
and merges anyway.

## Use it

Open the deployed page with `#build` on the end:

```
https://<your-pages-url>/#build
```

Fill in the names, hit **Generate link**, send the link.

## How it works

One static HTML file. No backend, no database, no dependencies, no build step.
The names and the note are base64-encoded into the URL fragment, so the whole
message travels in the link itself and nothing is ever stored server-side.

That also means **anyone holding the link can decode it** — it is obscured,
not encrypted. Don't put anything in the note you'd mind being forwarded.

## Details

- Cursor-repulsion physics on desktop; teleport-on-`pointerdown` for touch,
  because `pointermove` doesn't fire on a phone until a finger is already down
- Honours `prefers-reduced-motion` throughout
- Keyboard accessible — the button is reachable by `Tab` and dodges on focus
- Canvas code-rain background, canvas confetti, WebAudio blips, no libraries
