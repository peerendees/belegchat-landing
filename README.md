# BelegChat Landingpage

Informations- und Registrierungsseite für **BelegChat** — digitale Belegerfassung und DATEV-Export per Threema. Zielgruppe: Selbstständige und Kleinunternehmer in Deutschland.

## Technik

- Reines HTML/CSS/JS, kein Framework, kein Build-Tool
- Schriften lokal unter `/assets/fonts/` (DSGVO-konform, kein Google Fonts CDN)
- Analytics: Plausible (datenschutzkonform)

## Assets einrichten

### Schriften (Pflicht)

Lege folgende WOFF2-Dateien in `assets/fonts/` ab:

- `bebas-neue-regular.woff2`
- `lora-300.woff2`
- `lora-400.woff2`
- `lora-600.woff2`

Download z. B. von [Google Fonts](https://fonts.google.com/download?family=Bebas+Neue|Lora) (nur zum lokalen Hosten verwenden).

### Logos

In `assets/images/`:

- `logo_farbe_v3.webp` — BERENT Wortlogo (Nav + Footer)
- `BE_Farbe_V3.png` — BERENT Signet (Favicon)

## Lokal ansehen

Einfach `index.html` im Browser öffnen oder einen lokalen Server starten:

```bash
npx serve .
```

## Optional: BERENT-CI-Rules (Submodul)

Falls du die vollständigen BERENT-CI-Rules nutzen möchtest:

```bash
git submodule add https://github.com/peerendees/berent-website-rules.git .cursor/rules
```

## Deployment

Vercel deployt automatisch aus `main`. Zieldomain: **belegchat.de**.

---

© 2026 BelegChat · BERENT — Beratung+Entwicklung
