# Fjordigital Ad Mockups

Live previews of Meta ad mockups for Fjordigital clients. Used for client review before campaigns go live in Ads Manager.

## Live URL

After enabling GitHub Pages: `https://<your-github-username>.github.io/fjordigital-mockups/`

## Structure

```
fjordigital-mockups/
├── index.html                                 ← landing page listing all mockups
├── eirs-helsehus/
│   └── 260508_chiropractor_split-test_v1/
│       ├── index.html                          ← the mockup
│       └── assets/
│           ├── creative-a-leg-knee.png
│           └── creative-b-lower-back.png
└── <other-clients>/
```

## Naming convention

```
YYMMDD_<service>_<purpose>_v<n>/
```

- `YYMMDD` — date the mockup was generated
- `<service>` — chiropractor, vo2-max, etc. (matches `clients/<klient>/raw/` subfolders)
- `<purpose>` — split-test, single-creative, retargeting, etc.
- `v<n>` — version, increments per purpose

## Adding a new mockup

1. Create `<klient>/<YYMMDD>_<service>_<purpose>_v<n>/`
2. Drop `index.html` + `assets/` inside
3. Add a row to root `index.html`
4. `git add . && git commit -m "Add <klient> <purpose>" && git push`
5. Pages serves it at `/<klient>/<folder>/` within ~1 minute

## What this repo MUST NOT contain

- HANDOFF.md files (sensitive client info)
- Contracts, CLTV models, pricing internals
- Client emails, billing details
- Anything from `clients/<klient>/` other than the mockup HTML + needed image assets

Mockup content itself (proposed copy, creatives, public clinic name) is fine — it's marketing material that goes public anyway when ads launch.
