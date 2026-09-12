<h1 align="center">Pull Request #1</h1>

<p align="center">
  <em>Ask someone out as if it were a code review.</em>
</p>

<p align="center">
  <a href="https://coderkundu.github.io/date-pr/"><strong>→ Open the live demo</strong></a>
</p>

<p align="center">
  <img alt="dependencies" src="https://img.shields.io/badge/dependencies-0-3fb950">
  <img alt="build step" src="https://img.shields.io/badge/build%20step-none-3fb950">
  <img alt="files" src="https://img.shields.io/badge/files-1-58a6ff">
  <img alt="approval rate" src="https://img.shields.io/badge/approval%20rate-100%25-a371f7">
</p>

---

They open your link. A terminal boots:

```console
$ git clone git@heart:you/them.git
Cloning into 'them'... done.
$ npm run ask-out

> courage@0.1.0 ask-out
> node ./src/say-it.js --nervous

compiling feelings............ ok
resolving 1 conflict (pride).. ok
warning: 0 backup plans found
```

Then a pull request slides in — `feat: add them to my Friday night`, one commit
into `main`, with a diff worth reviewing:

```diff
  export const friday = {
-   plans: null,
-   status: "technically free",
+   plans: "dinner on Friday",
+   status: "booked",
+   nerves: Infinity,      // known issue, tracked in #2
+   backupPlan: null,      // there is no plan B
+   reversible: false,
  };
```

Three checks pass. `lint / overthinking` reports **0 errors, 47 warnings**.
One check stays yellow and blocks the merge: `review / your-decision`.

Two buttons. `Approve & merge`, and `Request changes`.

## The catch

`Request changes` cannot be clicked.

Get close and it breaks out of the layout, goes `position: fixed`, and runs.
The slot it leaves behind renders `404 — button not found`. It shrinks, fades,
and works through its excuses:

| Attempt | Button says |
|:--:|---|
| 1 | Are you sure? |
| 2 | Merge conflict |
| 4 | Rebase and retry |
| 6 | `npm ERR! peer dep missing` |
| 9 | Segmentation fault |
| 11 | Branch protection enabled |
| 14 | I can do this all day |
| 15 | *lgtm, fine* |

Meanwhile `Approve & merge` grows, a `ci-bot` heckles from the comment thread,
and a **reviewer resolve** meter drains from 100% to zero.

On the fifteenth escape the button gives up, turns green, and merges anyway.
Say yes and the last check flips, the badge goes purple, confetti made of
`{}` `</>` `=>` fires from both sides, and the log closes it out:

```console
$ git log --oneline -3
7951fd3 (HEAD -> main) feat: add them to my Friday night
a1c0ffe  chore: rehearse asking 11 times
deadbee  init: notice them across the room
```

## Make your own

**[coderkundu.github.io/date-pr/#build](https://coderkundu.github.io/date-pr/#build)**

Two names, what you're asking for, and the note they see after they approve.
Hit generate, send the link. No signup, no account, nothing to install.

> The configuration is base64-encoded into the URL fragment, so there's no
> backend and nothing is stored anywhere. It also means anyone holding the
> link can decode it — obscured, not encrypted. Don't put anything in the
> note you'd mind being forwarded.

## Under the hood

One HTML file. No framework, no build, no dependencies — the confetti, the
code rain, the typewriter and the sound are all hand-rolled canvas and
WebAudio.

A few things that took more care than expected:

- **Touch needed different physics.** Cursor-repulsion doesn't exist on a
  phone — `pointermove` only fires once a finger is already down. Touch gets
  teleport-on-`pointerdown`, which lands before `click` and so eats the tap.
- **`animation-fill-mode: both` broke `position: fixed`.** It leaves an
  identity `transform` on the element permanently, and a transformed ancestor
  makes `fixed` resolve against *that ancestor* instead of the viewport. The
  button happily fled off-screen where nobody could reach it. Now it reparents
  to `<body>` and clamps against its measured rect rather than trusting the
  maths.
- **The dodge has an ending.** Infinite dodging is annoying, not funny.
- **It stays accessible.** `prefers-reduced-motion` is honoured throughout, and
  the button is reachable by `Tab` — it just dodges on focus and the bot
  acknowledges the attempt.

## Running it locally

```bash
git clone https://github.com/CoderKundu/date-pr.git
```

Open `index.html`. That's the whole thing.

---

<p align="center"><sub>Built with questionable judgement. Good luck.</sub></p>
