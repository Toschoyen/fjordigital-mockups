# Fjordigital Ad Mockups

Obfuskert preview-host for Meta-annonser. Klient får én unik URL — det finnes ingen landing page, ingen klient-listing, og ingen indexering.

## Repo URL

`https://github.com/Toschoyen/fjordigital-mockups`

## Pages base URL

`https://toschoyen.github.io/fjordigital-mockups/`

Root-URL gir 404 by design. Kun direktelinker til hver mockup virker.

## Struktur

```
fjordigital-mockups/
├── README.md           ← kun synlig på github.com (ikke på Pages)
├── robots.txt          ← Disallow: / (blokker søkemotorer)
├── 404.html            ← ren feilmelding, ingen leak
└── m/                  ← obfuskert namespace (404 ved direkte besøk)
    └── <klient>-<kampanje>-<random8hex>/
        ├── index.html  ← har <meta name="robots" content="noindex">
        └── assets/
```

## Live-URLer (intern referanse — IKKE del med klient-X andre klienters URL)

| Klient | Mockup | URL |
|---|---|---|
| Eirs Helsehus | M1 chiro split-test v1 | `https://toschoyen.github.io/fjordigital-mockups/m/eirs-helsehus-m1-9c51282a/` |

## Naming-konvensjon for mappe i `m/`

```
<klient>-<kampanje-id>-<8-char-random-hex>
```

- Klient + kampanje-ID for intern gjenkjennelse
- Random hex-suffix gjør URLen ugjettbar fra utsiden
- Generer slug: `openssl rand -hex 4`

## Security-modell

**Hva er beskyttet:**
- Klient kan ikke navigere "opp" og se andre klienter (ingen listing-pages, root → 404)
- Søkemotorer blokkert (robots.txt + noindex meta)
- Mappenavn er ugjettbart (random hex-suffix)
- Custom 404 lekker ingen info

**Hva er IKKE beskyttet (krever privat repo):**
- `github.com/Toschoyen/fjordigital-mockups` viser hele tre-strukturen for alle som finner repo-URLen
- Klient kan forwarde sin URL til tredjepart
- Ved ekte sensitive klient-data: bytt til Cloudflare Pages eller Netlify med privat GitHub-repo, eller GH Pro ($4/mnd) for privat Pages

## Legge til ny mockup

```bash
SLUG=$(openssl rand -hex 4)
KLIENT="<klient-slug>"   # eks: kawasaki, spir-helse
KAMPANJE="<kampanje-id>" # eks: m1-chiro, q3-retargeting
mkdir -p "m/$KLIENT-$KAMPANJE-$SLUG/assets"
# kopier inn index.html + assets/
git add .
git commit -m "Add $KLIENT $KAMPANJE mockup ($SLUG)"
git push
```

URL etter ~1 min: `https://toschoyen.github.io/fjordigital-mockups/m/<klient>-<kampanje>-<slug>/`

## ALDRI commit til dette repoet

- `HANDOFF*.md`
- Kontrakter (`*kontrakt*`, `*contract*`)
- CLTV-modeller, prising, e-postdetaljer
- Alt fra `clients/<klient>/` annet enn mockup-HTML + nødvendige bilder

`.gitignore` har safety-net for disse mønstrene.
