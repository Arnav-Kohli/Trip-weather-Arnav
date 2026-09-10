# Should I Go?

Enter a city and your dates. Get a plain-language verdict for every day, one
packing list for the whole trip, and a line telling you which day to spend
outdoors.

**Live:** _(paste the deployed URL here)_

---

## Open it locally

There is no build step, no install, and no dependencies.

```
open index.html          # macOS
xdg-open index.html      # Linux
start index.html         # Windows
```

Double-clicking the file works too. `index.html` is fully self-contained, so it
runs from `file://` — the only thing it needs is a network connection, because
every forecast is fetched live from Open-Meteo at runtime.

No API key is required. Open-Meteo's geocoding and forecast endpoints are
keyless for non-commercial use.

## Deploy it

One static file, nothing to compile:

```
# Netlify — drag this folder onto https://app.netlify.com/drop
# GitHub Pages — push, then Settings → Pages → deploy from branch root
# Vercel — vercel deploy (framework preset: Other)
# Any static host — upload index.html
```

`verdict.js` and `test-verdict.mjs` are **not** needed at runtime. They exist so
the judgement logic can be read and tested on its own; the same code is inlined
into `index.html`. Deploying `index.html` alone is enough.

## Run the tests

```
node test-verdict.mjs
```

72 checks covering the thresholds, the multi-problem ordering, packing-list
grouping and dedupe, the move, and how confidence decays with forecast
distance. No test runner, no dependencies.

## Demo mode

```
index.html?demo=1
```

Fills in Jaipur and the next five days and runs it immediately — for screen
recordings, so a demo never opens with someone mistyping a city. The forecast is
still fetched live; only the typing is skipped.

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app. This is the only file you need to deploy. |
| `verdict.js` | The judgement layer as readable source, imported by the tests. |
| `test-verdict.mjs` | 60 assertions, run with plain `node`. |
| `NOTE.md` | Why the thresholds are where they are, and how the whole thing works. |
