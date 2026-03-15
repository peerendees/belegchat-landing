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

### Hero-Hintergrund (optional)

Für die Hero-Sektion kann ein Bild unter `assets/images/hero.webp` hinterlegt werden. Ohne Datei bleibt der Hintergrund Anthrazit.

**Vorschläge für ein passendes Bild ohne großen Aufwand:**

- **Unsplash / Pexels (kostenlos):** Suche z. B. nach „office desk“, „receipt“, „document“, „minimal workspace“ — lizenzfrei, oft in hoher Auflösung. Bild herunterladen, in WebP konvertieren (z. B. [Squoosh](https://squoosh.app)), als `hero.webp` speichern.
- **Eigenes Foto:** Schreibtisch, Ordner mit Belegen oder ein ruhiges Büro-Setting; mit dem Handy reicht oft. Für Web schmal zuschneiden (z. B. 1600×900 px) und als WebP exportieren.
- **KI-generiert:** Dienste wie DALL·E, Midjourney oder Stable Diffusion mit Prompt z. B. „minimalistischer Schreibtisch mit Dokumenten, dunkler Hintergrund, professionell“ — dann in WebP konvertieren und einbinden.

## Lokal ansehen

Einfach `index.html` im Browser öffnen oder einen lokalen Server starten:

```bash
npx serve .
```

## Optional: BERENT-CI-Rules (Submodul)

Falls du die BERENT Rules zu Beginn vergessen hast einzubinden, kannst du das **Setup-Skript** aus dem Rules-Repo ausführen:

```bash
cd /pfad/zum/belegchat-landing
curl -sSL https://raw.githubusercontent.com/peerendees/berent-website-rules/main/setup.sh | bash
```

Das Skript heißt **`setup.sh`** und bindet das Rules-Repo als Submodule unter `.cursor/rules` ein. Danach:

```bash
git add .gitmodules .cursor/rules
git commit -m "Rules als Submodule einbinden"
git push origin main
```

**Manuell** (ohne Script):

```bash
git submodule add https://github.com/peerendees/berent-website-rules.git .cursor/rules
```

**Vercel:** In den Projekteinstellungen „Include Git submodules“ aktivieren.

## Deployment

Vercel deployt automatisch aus `main`. Zieldomain: **belegchat.de**.

---

© 2026 BelegChat · BERENT — Beratung+Entwicklung
