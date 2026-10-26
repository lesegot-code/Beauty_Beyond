# Beauty_Beyond

An interactive birthday experience — a tiny chase, a cipher, and a poem.

Built as a single static site: plain HTML, CSS, and vanilla JavaScript. No
frameworks, no build step, no backend, no dependencies. Open `index.html`
and it works.

---

## What it is

A small, four-stage journey that a person works through on their own:

1. **Catch** — a button that runs away from the cursor. It starts fast and
   gradually slows over ~30 seconds until it can be caught.
2. **Decrypt** — a three-word message arrives as ciphertext. Decode it to
   reveal the phrase underneath.
3. **Transform** — the decoded phrase is `I HATE YOU`, a shared joke. One
   word needs to change. The visitor changes it to `I LOVE YOU`.
4. **Read** — the poem. A frosted-glass card floating over a living rose
   field, with falling petals.

The poem is an original piece written for the recipient, inspired by
William Shakespeare's Sonnet 130. It is the point of the whole thing; everything
before it is a reason to arrive at it.

---

## Files
```
Beauty_Beyond/
├── Poems           Poem versions and improvements
├── index.html      Stage 1 — the runaway button
├── puzzle.html     Stages 2 & 3 — cipher and transformation
├── poem.html       Stage 4 — the poem
└── README.md
```


Each page is self-contained. There is no shared CSS or JS file, on purpose:
any one stage can be opened, shown, or debugged on its own without the
others. If `puzzle.html` ever breaks, `index.html` still works.

---

## Running it

**Locally:** just open `index.html` in a browser. That's it. No server
required, though if you want the page-to-page navigation to behave exactly
like production, serve the folder:

```bash
# Python 3
python3 -m http.server 8000

# or Node
npx serve .
```

Then visit http://localhost:8000.

__Deploying__: it's a static site. Drag the folder into Netlify Drop, push
to GitHub Pages, or host it anywhere that serves files. No configuration
needed.

## How it works
__Stage 1__ — the runaway button (index.html)
The button is position: fixed and its position is driven by JavaScript in
viewport pixels, where left/top represent the button's centre.

It flees when the cursor comes within ~2cm (76px).

Its speed decays linearly over 30 seconds, so it becomes catchable.

It stays at least ~3cm (113px) from every viewport edge.

A bounce flag flips every 2 seconds, changing how momentum is handled
(elastic pinball vs. heavy drag). This gives the chase a rhythm.

Touch devices can't chase with a cursor, so the button requires 7 taps
instead. The number is never revealed — hints escalate instead.

__tages 2 & 3__ — cipher and transformation (puzzle.html)

The cipher is A1Z1 (A=1 … Z=26). The ciphertext decodes to I HATE YOU.

After 12 seconds, a hint appears offering the method, not the answer. There
is no attempt limit and no lockout — it's a birthday gift, not a captcha.

The transformation is one intentional tap: HATE is a replaceable tile, and
the picker offers LOVE (correct) alongside MISS and LIKE (decoys). The
wrong options are gentle nudges toward the right one, not obstacles.

__Stage 4__ — the poem (poem.html)
A frosted-glass card (backdrop-filter: blur(18px)) over a layered
background: a wine gradient, three drifting light orbs, and rose petals
falling at three depths (far, mid, near) to create parallax.

