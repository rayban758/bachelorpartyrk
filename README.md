# Crystal Springs Bachelor Weekend — Setup

A single-page site the 12 of you share. Votes, itinerary edits, and check-ins are saved as **commits to this repo** (in `data.json`), so GitHub itself is the memory and the full change history lives at the "View change history" link on the site.

## 1. Create the repo
1. On GitHub, create a new repo (e.g. `bachelor-party`). Public is simplest for Pages; private works too with Pages enabled.
2. Upload `index.html` to the repo root.

## 2. Point the site at your repo
Open `index.html` and edit these two lines near the top of the `<script>`:

```js
const GH = {
  owner: 'YOUR_GITHUB_USERNAME',   // <-- your GitHub username
  repo: 'bachelor-party',          // <-- the repo name
  ...
```

## 3. Turn on GitHub Pages
Repo → **Settings → Pages** → Source: "Deploy from a branch" → Branch: `main`, folder `/ (root)` → Save.
Your site goes live at `https://YOUR_USERNAME.github.io/bachelor-party/` in a minute or two.

## 4. Create the group token (this is what lets people save)
1. GitHub → Settings → Developer settings → **Fine-grained personal access tokens** → Generate new token.
2. Repository access: **Only select repositories** → pick this repo only.
3. Permissions: **Contents → Read and write**. Nothing else.
4. Set an expiration shortly after the trip (e.g. Aug 31).
5. Copy the token and share it with the group chat.

When each guy opens the site, it asks once for the token and remembers it in his browser. Without a token the site is read-only.

**Heads up on the tradeoff:** everyone with the token can write to this one repo. Because it's fine-grained and scoped to only this repo with only Contents access, that's the whole blast radius — but don't reuse a token that touches anything else, and revoke it after the trip.

## 5. First load
The first person with a token to open the site auto-creates `data.json` with the default activity list. Every vote after that shows up as a commit like `Ray updated activities_v2`.

## Local testing
Opening `index.html` directly from disk works for reading; some browsers block `fetch` from `file://`, so for local testing run `python3 -m http.server` in the folder and open `http://localhost:8000`.

## Note on the two versions
- `index.html` — the GitHub-hosted version (this one). No AI features, because the Claude API can only be called from inside a Claude artifact.
- `bachelor-party-fable.html` — the Claude-artifact version with the Fable concierge and auto-itinerary drafting. Use it inside Claude; it can't be hosted on Pages.
