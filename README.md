# Draft-engine

A single-page browser tool that turns a competitive drafting framework into live
pick and ban recommendations, evaluated against the current draft state.

**[Live →](https://tylerolder-png.github.io/Draft-engine/)**

## Design constraints

The tool had to open instantly and run alongside another app on a phone, mid-draft.
That constraint drove every decision here.

**No backend.** All logic runs client-side against a tier dataset held in the
source. There's no request to wait on, so recommendations update the moment a
selection changes. It also means the whole thing is a static file — nothing to
deploy, nothing to keep running, no cost.

**Deliberately stateless.** No browser storage. Every draft starts clean, so a
refresh resetting the board is the correct behavior rather than data loss. Adding
persistence would have meant adding a "clear" affordance for no benefit.

**One self-contained file.** HTML, CSS, and JavaScript live in `index.html`. When
a balance patch changes the tier values, that's a single-file edit committed
straight through GitHub's web editor — no build step, no local clone, and every
client picks up the change on next load.

**Installable.** Served over HTTPS via GitHub Pages, so it can be added to a phone
home screen from the browser and opens without browser chrome.

## Updating the data

Tier values live in the `DATA` structure near the top of the script block in
`index.html`. Edit the values, commit, and the deployed site updates within a
minute or two.

## Deployment

GitHub Pages, deploying from `main` at root. The entry file must be named
`index.html` for Pages to serve it at the root URL.
