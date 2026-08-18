# Who's Your Pawtner in Crime? 🚨🐾

An 8-question booking quiz that matches you to a real adoptable dog ("inmate") at **Last Chance Ranch — Department of Pawctions**, a small no-kill rescue in South Carolina. Result = your "charge" + your match's Inmate File + Apply for Parole.

Static site: one `index.html`, no build step. Same engine as [fairy-dog-child](https://github.com/selard73/fairy-dog-child).

## Files

- `index.html` — everything (styles, dog data, questions, app)
- `mugshots/<name>.jpg` — one photo per dog (`blue.jpg`, `isaiah.jpg`, `oatmeal.jpg`, `frodo.jpg`, `leroy.jpg`, `sanders.jpg`, `lizzy.jpg`, `princess.jpg`). If a file is missing, a placeholder cell renders instead — nothing breaks.
- `share/<key>.html` — per-dog Facebook share pages (OG tags + redirect). Keys: `oat blu isa fro ler san liz pri`.
- `og.png` — generic link-preview image (TODO: make one, 1200×630, in the Inmate File style).

## Updating dogs

All dog data is the `DOGS` object in `index.html`. Each entry:

```js
key: { num, name, aka, rank, breed, sex, age, weight, status,
       report: [...bullets], notes: [...paragraphs], conditions, hidden?, pair? }
```

- Empty string → renders as "pending".
- `hidden: true` → dog is removed from scoring, the result, and the cell-block grid; its answer points fall to the secondary dog. **Lizzy is hidden until Thumper's status is confirmed.** Flip it to show the "Lizzy & Thumper — must be paroled together" card.
- `pair: {num, name}` → renders as a bonded pair.
- When a dog is adopted: set `hidden: true` (or delete the entry and its answers).

## Questions & scoring

`QUESTIONS` — each answer is `[text, primaryDog(+2), secondaryDog(+1), chargeKey]`. Highest dog score wins (ties random). Most-tallied charge is "what you're in for" (`CHARGES`). Each active dog is primary on 4 answers.

## Links

`LINKS` at the top of the script:
- `apply` — adoption application (JotForm) → "Apply for Parole Today"
- `foster` — foster application (JotForm)
- `donate` — Cash App → "Post Bail"
- `page` — Last Chance Ranch Facebook page

Contact shown on the result: (803) 479-8408 · lastchanceranchofsc@gmail.com

## Deploy

Push to GitHub → Render static site (or Netlify), same as fairy-dog-child. **After deploy:** change `og:image` in `index.html` and `share/*.html` to absolute URLs (Facebook needs them), and add a custom domain if desired.

## Sounds

The typewriter click / bell / stamp are synthesized by default (no files). To use real samples, drop `sounds/key.mp3`, `sounds/ding.mp3`, `sounds/stamp.mp3` (`.wav`/`.ogg` also work) — the page picks them up automatically and adds slight pitch variation per keystroke. Mute toggle top-right; preference is remembered.
