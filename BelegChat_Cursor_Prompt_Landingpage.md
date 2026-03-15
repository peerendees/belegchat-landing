# Cursor-Prompt: BelegChat Landingpage

---

## Schritt 0 — Vorbereitung

### 0a — BelegChat-App-Repo bereinigen (separater Schritt, vor der Landingpage)

Das bestehende BelegChat-App-Repo enthält noch Altinhalte, die vor der Weiterarbeit zu entfernen sind. Öffne das Repo lokal und führe folgendes aus:

1. Lösche alle Dateien und Ordner mit Ausnahme von:
   - `.git/`
   - `.cursor/`
   - `.gitmodules`
   - `.gitignore`

2. Suche und ersetze alle Vorkommen von „Archivator" im gesamten Repo. Der einzig gültige Produktname ist **BelegChat**. Nach der Bereinigung committen und pushen:
   ```bash
   git add .
   git commit -m "chore: Repo bereinigt, Archivator-Verweise entfernt"
   git push origin main
   ```

### 0b — Landingpage-Verzeichnis vorbereiten

Das Landingpage-Verzeichnis (`belegchat-landing`) ist leer und bereit. Keine Bereinigung notwendig.

1. Kopiere die Logo-Dateien in `/assets/images/`:
   - `logo_farbe_v3.webp` — BERENT Wortschriftzug "Beratung+Entwicklung"
   - `BE_Farbe_V3.png` — BERENT Signet (B+E Icon), als Favicon

2. Das Projekt basiert auf dem Template-Repo `peerendees/berent-website-template`. Die BERENT-CI-Rules sind als Git-Submodul unter `.cursor/rules/` eingebunden (`peerendees/berent-website-rules`). Lies `@.cursor/rules/berent-ci.mdc` und `@.cursor/rules/project-workflow.mdc` bevor du irgendetwas baust.

---

## Schritt 1 — Schriften lokal hosten (DSGVO-Pflicht)

Verwende **keine** Google Fonts CDN-Links (`fonts.googleapis.com`). Das Laden von Schriften über Google-Server überträgt IP-Adressen an US-Server und ist ohne Einwilligung ein DSGVO-Verstoß (LG München, 2022).

Stattdessen:

1. Lege den Ordner `/assets/fonts/` an.
2. Platziere dort die folgenden WOFF2-Dateien (Open Font License, frei verwendbar):
   - `bebas-neue-regular.woff2`
   - `lora-300.woff2`
   - `lora-400.woff2`
   - `lora-600.woff2`
3. Lade die Dateien von `fonts.google.com/download` herunter oder bitte den Nutzer, sie manuell zu hinterlegen.
4. Binde sie ausschließlich per `@font-face` in der CSS ein — kein externer Request.

```css
@font-face {
  font-family: 'Bebas Neue';
  src: url('/assets/fonts/bebas-neue-regular.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
}
@font-face {
  font-family: 'Lora';
  src: url('/assets/fonts/lora-400.woff2') format('woff2');
  font-weight: 400;
  font-display: swap;
}
/* analog für 300 und 600 */
```

---

## Schritt 2 — Kontext und Produktidentität

Du baust die Landingpage für **BelegChat** — eine deutsche SaaS-Plattform für digitale Belegerfassung und DATEV-Export. Die Zielgruppe sind Selbstständige und Kleinunternehmer in Deutschland.

**Was diese Seite ist:** Eine Informations- und Registrierungsseite im MVP-Stadium. Sie zeigt, was BelegChat tut und weshalb Threema der einzige Eingabekanal ist. Sie lädt zur Anmeldung als Beta-Tester ein.

**Was diese Seite nicht ist:** Eine App-Oberfläche. Es werden keine Funktionen beworben, die noch nicht existieren.

**Alleinstellungsmerkmal:** BelegChat nutzt Threema Work Gateway als technologische Basis. Das ist kein Zufall — es ist die Entscheidung für maximale Datensicherheit, Ende-zu-Ende-Verschlüsselung und DSGVO-Konformität von Grund auf. Kein anderes Buchhaltungstool in Deutschland setzt auf diesen Kanal.

---

## Schritt 3 — BERENT Corporate Identity

Alle CI-Details stehen in `@.cursor/rules/berent-ci.mdc`. Die wichtigsten Punkte für diese Seite:

```
Hintergrund:      #090806
Kupfer (Primär):  #B5742A  — Headlines, Buttons, Borders
Gold:             #E8C98A  — ausschließlich für das + Symbol
Fließtext:        #C4BCB1
Sekundärtext:     #9A8870
Card-BG:          #110E0A
Border:           #2A2118
```

- Kein `#000000`, kein `#FFFFFF`
- Headlines: Bebas Neue, UPPERCASE, `letter-spacing: 0.06em`
- Fließtext: Lora, kein `font-style: italic`
- Das `+` Symbol immer in Gold `#E8C98A`, nie in Kupfer

**BERENT-Logo (Navigation, links oben):**
Verwende das Wortlogo `assets/images/logo_farbe_v3.webp` — der vollständige Schriftzug "BERENT — Beratung+Entwicklung". Es erscheint links oben in der Navigation als klickbarer Link auf `https://berent.ai`, klein und diskret. Maximalhöhe in der Nav: 32px.

```html
<a href="https://berent.ai" class="berent-brand" aria-label="BERENT.AI — Beratung und Entwicklung">
  <img src="/assets/images/logo_farbe_v3.webp" alt="BERENT — Beratung + Entwicklung" height="32">
</a>
```

Das BERENT-Logo erscheint auch im Footer (Höhe 24px), links neben den Pflichtlinks.

**Favicon:** Verwende `assets/images/BE_Farbe_V3.png` als Favicon:
```html
<link rel="icon" type="image/png" href="/assets/images/BE_Farbe_V3.png">
```

**Hinweis:** Beide Logo-Dateien haben einen dunklen Hintergrund (`#090806`), der sich nahtlos in den Seitenhintergrund einfügt.

---

## Schritt 4 — Seitenstruktur

Baue eine einzelne `index.html` mit folgendem Aufbau:

### Navigation (sticky, `#090806` Hintergrund)
- Links: BERENT-Logo (klein, diskret) + Wortmarke `BELEGCHAT` in Kupfer
- Mitte: Anker-Links `FUNKTIONSWEISE` · `SICHERHEIT` · `PREISE` · `FAQ`
- Rechts: Button `BETA-ZUGANG SICHERN` — Kupfer-Hintergrund, Text in `#090806`
- Mobil: Hamburger-Menü

### Hero
- H1 (Bebas Neue, groß): `BELEGE PER THREEMA EINSCHICKEN. FERTIG FÜR DEN STEUERBERATER.`
- Unterzeile (Lora 18px, `#C4BCB1`): „BelegChat erfasst deine Belege automatisch, ordnet sie buchhalterisch ein und erstellt auf Knopfdruck eine DATEV-Exportdatei — GoBD-konform, DSGVO-sicher, ohne Papierchaos."
- Primär-Button: `JETZT ALS BETA-TESTER EINSCHREIBEN` → `#registrierung` (Anker)
- Sekundär-Link: `Wie es funktioniert ↓` → `#funktionsweise`
- Hintergrund: `#090806`, kein Bild, kein Gradient

### Vertrauensleiste
Schmale Zeile, `#110E0A` Hintergrund, fünf Punkte mit `+` in Gold als Bullet:
- GoBD-konform
- DSGVO-sicher
- Ende-zu-Ende-verschlüsselt via Threema
- DATEV-Export auf Knopfdruck
- Keine App-Installation notwendig

### Funktionsweise (id="funktionsweise")
Drei Schritte, horizontal auf Desktop, vertikal auf Mobil. Nummerierung in Kupfer.

```
+ EINSCHICKEN       Foto oder PDF per Threema senden
+ ERKENNEN          OCR liest, KI schlägt Buchungskonto vor
+ EXPORTIEREN       DATEV-Datei herunterladen — Steuerberater importiert direkt
```

Hinweistext darunter (Lora, `#9A8870`):
„Kein Upload-Portal. Keine neue App. Nur Threema — den Messenger, dem du bereits vertraust."

### Weshalb ausschließlich Threema? (id="sicherheit")
H2: `WESHALB NUR THREEMA?`

Vier Punkte mit `+` Icon:
- Keine Telefonnummer, keine E-Mail-Adresse erforderlich
- Ende-zu-Ende-verschlüsselt — kein Dritter, auch nicht BelegChat, kann mitlesen
- Keine Metadatenspeicherung — Threema erfasst nicht, wer wann was schickt
- DSGVO-konform by Design — Schweizer Datenschutzstandard

Infokasten (`#1A1208` Hintergrund, Kupfer-Border links `4px solid #B5742A`, Lora):
> „BelegChat verarbeitet ausschließlich Inhalte, die du aktiv einsendest. Personenbezogene Daten und Buchungsdaten werden getrennt gespeichert. Eine Weitergabe an Dritte findet nicht statt."

**Technologie-Block darunter:**
H3: `DIE TECHNOLOGIE DAHINTER`

Zwei Punkte ausführlicher erklärt:

**Threema Work Gateway**
Das Herzstück von BelegChat. Jeder Kunde erhält eine dedizierte Threema-Gateway-ID — einen verschlüsselten Eingangskanal, der ausschließlich für diesen einen Buchungskreis existiert. Nachrichten und Anhänge werden Ende-zu-Ende-verschlüsselt übertragen. Kein Server liest mit, bevor die Entschlüsselung auf der BelegChat-Seite stattfindet. Das ist kein Standard in der Branche — es ist die bewusste Entscheidung für maximale Vertraulichkeit.

**Threema Work**
BelegChat nutzt Threema Work als Kommunikationsbasis. Damit läuft auch die Kundenkommunikation — Onboarding, Support, Updates — ausschließlich über denselben verschlüsselten Kanal. Kein E-Mail-Ticketsystem, keine externen Plattformen.

### Preise (id="preise")
H2: `EHRLICHE PREISE`

Drei Karten, mittlere hervorgehoben (Kupfer-Border):

| Karte | Bezeichnung | Preis |
|---|---|---|
| Standard | Ab offiziellem Launch | 19,95 €/Monat |
| Beta-Einstieg ★ | Jetzt einsteigen, dauerhaft −20 % | 15,95 €/Monat |
| Gründertarif | Max. 20 Plätze — dauerhaft −30 % ab Launch | 9,95 € während Beta / 13,95 € ab Launch |

Hinweis unter den Karten (Lora, klein, `#9A8870`):
„Alle Tarife inklusive bis zu 2 Mandanten und mindestens einer Threema-Work-ID. Abrechnung über Stripe. Monatlich kündbar. Kein Zweijahresabo."

### Registrierung (id="registrierung")
Einfaches Formular: Name, E-Mail, optional Gutschein-Code.
Submit-Button: `JETZT REGISTRIEREN` in Kupfer.
Hinweistext: „Mit der Registrierung stimmst du unseren Nutzungsbedingungen zu. Deine Daten werden ausschließlich zur Kontoverwaltung verwendet."

### FAQ (id="faq")
H2: `HÄUFIGE FRAGEN`

Aufklappbares Akkordeon, kein JavaScript-Framework, nur vanilla JS.
`+`-Symbol in Gold als Öffnen/Schließen-Indikator (dreht sich zu `×`).

**Fragen und vollständig ausformulierte Antworten:**

---

**Was ist BelegChat?**
BelegChat ist eine digitale Buchhaltungshilfe für Selbstständige und Kleinunternehmer in Deutschland. Du schickst deine Belege per Threema ein — BelegChat erkennt sie automatisch, ordnet sie einem Buchungskonto zu und erstellt eine DATEV-Exportdatei für deinen Steuerberater. Alles GoBD-konform, DSGVO-sicher, ohne Papierchaos.

---

**Weshalb muss ich Threema verwenden?**
Threema ist der einzige Messenger, der Ende-zu-Ende-Verschlüsselung mit vollständiger Anonymität verbindet — keine Telefonnummer, keine E-Mail-Adresse erforderlich. Für Belege mit sensiblen Geschäftsdaten ist das keine Komfort-Entscheidung, sondern eine datenschutzrechtliche. BelegChat nutzt darüber hinaus Threema Work Gateway: Jeder Kunde erhält eine eigene, dedizierte Eingangs-ID. Was du einschickst, bleibt ausschließlich in deinem Buchungskreis.

---

**Was ist Threema Work Gateway — und weshalb ist das besonders?**
Threema Work Gateway ist eine API-Schnittstelle, über die Unternehmen verschlüsselte Nachrichten senden und empfangen können — programmatisch, automatisiert, ohne dass ein Mensch mitlesen kann. BelegChat nutzt diese Schnittstelle, um für jeden Kunden einen eigenen, verschlüsselten Eingangskanal zu betreiben. Kein anderes Buchhaltungstool in Deutschland setzt auf diese Technologie. Das ist das Alleinstellungsmerkmal von BelegChat.

---

**Was passiert, wenn ich meine Threema-ID verliere?**
Der Zugang zum BelegChat-Eingang ist an deine Threema-ID gebunden. Geht sie verloren, ist eine Wiederherstellung nicht möglich. Deshalb ist beim Onboarding ein Threema-Backup über den Tresor zwingend erforderlich — du bestätigst diesen Schritt aktiv. Der Betreiber haftet nicht für den Verlust der ID.

---

**Kann ich zwei getrennte Buchungskreise verwalten?**
Ja. Ein Konto unterstützt bis zu zwei Mandanten — zum Beispiel ein Privatunternehmen und ein zweites Geschäft, oder zwei Partner mit je einer eigenen Threema-ID. Jeder Buchungskreis ist strikt getrennt: Kein gegenseitiger Einblick, keine gemeinsamen Daten.

---

**Ist BelegChat GoBD-konform?**
BelegChat stellt die technischen Mittel bereit, die eine GoBD-konforme Arbeitsweise ermöglichen: Belege werden unveränderlich archiviert, alle Änderungen werden protokolliert, verbuchte Buchungssätze sind dauerhaft gesperrt. Die Verantwortung für die Einhaltung der GoBD liegt beim Nutzer — BelegChat ist Werkzeug und Auftragsverarbeiter, keine Buchhaltungssoftware.

---

**Muss mein Steuerberater BelegChat kennen?**
Nein. Dein Steuerberater erhält eine Standard-DATEV-Exportdatei, die er direkt in DATEV Unternehmen online importieren kann. Kein neues Programm, keine Schulung, kein zusätzlicher Aufwand auf seiner Seite.

---

**Was bedeutet Beta-Phase?**
BelegChat befindet sich in der aktiven Entwicklungsphase. Beta-Tester nutzen das Produkt zu einem dauerhaft vergünstigten Preis und geben aktiv Rückmeldung. Im Gegenzug erhalten sie priorisierten Support direkt über Threema Work und dauerhaften Zugang zum vergünstigten Tarif — auch nach dem offiziellen Launch.

---

**Wie werden meine Daten gespeichert?**
Personenbezogene Daten und Buchungsdaten werden in getrennten Datenbanken gespeichert (Zwei-Datenbank-Architektur mit Pseudonymisierung). Belegdateien liegen verschlüsselt im Storage-System. Alle eingehenden Daten kommen Ende-zu-Ende-verschlüsselt über Threema — kein Klartext-Eingang über unsichere Kanäle. Für alle externen Dienstleister (Supabase, Stripe u. a.) bestehen Auftragsverarbeitungsverträge gemäß Art. 28 DSGVO.

---

### Call-to-Action-Banner
Hintergrund Kupfer `#B5742A`, Text `#090806`:
H2: `NOCH 20 GRÜNDER-PLÄTZE VERFÜGBAR`
Unterzeile: „Dauerhaft 30 % unter dem regulären Preis. Solange das Konto aktiv bleibt."
Button: `JETZT EINSCHREIBEN` → `#registrierung`

### Footer
Links: BERENT-Logo (`+` in Gold, `BERENT.AI` in `#9A8870`)
Mitte: `© 2026 BelegChat · belegchat.de`
Rechts: `Impressum` · `Datenschutzerklärung` · `Nutzungsbedingungen`
Ganz unten (klein, `#9A8870`): „Threema ist ein eingetragenes Warenzeichen der Threema GmbH."

---

## Schritt 5 — Cookie-Banner

Einzeiliger Banner, fixiert unten, `#110E0A` Hintergrund, Kupfer-Border oben:
„Diese Seite verwendet Plausible Analytics — datenschutzkonform, ohne personenbezogene Daten. Kein Consent erforderlich."
Button: `VERSTANDEN` — schließt den Banner, setzt Cookie `banner_dismissed=1`.

---

## Schritt 6 — Technische Anforderungen

- Reines HTML/CSS/JS — kein Framework, kein Build-Tool
- Alle Schriften lokal unter `/assets/fonts/` (WOFF2, `@font-face`)
- Kein externer HTTP-Request außer Plausible Analytics (`plausible.io/js/script.js`)
- Vollständig responsiv: Mobile-first, Breakpoints bei 768px und 1200px
- Ladezeit unter 2 Sekunden auf Mobilgeräten (keine unnötigen Assets)
- Semantisches HTML5 (`<nav>`, `<main>`, `<section>`, `<footer>`, `<article>`)
- Barrierefreiheit: `aria-label` auf allen interaktiven Elementen, ausreichende Kontrastverhältnisse
- Akkordeon-FAQ: vanilla JS, kein Framework
- Alle Anker-Links mit `scroll-behavior: smooth`

---

## Schritt 7 — Dateistruktur

```
belegchat-landing/
├── .cursor/
│   └── rules/          ← Git-Submodul: peerendees/berent-website-rules
├── assets/
│   ├── fonts/
│   │   ├── bebas-neue-regular.woff2
│   │   ├── lora-300.woff2
│   │   ├── lora-400.woff2
│   │   └── lora-600.woff2
│   ├── images/
│   │   ├── logo_farbe_v3.webp   ← BERENT Wortlogo (Nav + Footer)
│   │   └── BE_Farbe_V3.png      ← BERENT Signet (Favicon)
│   └── css/
│       └── style.css
├── index.html
├── .gitmodules
├── .gitignore
└── README.md
```

---

## Schritt 8 — Deployment

Nach Fertigstellung und lokalem Review:

```bash
git add .
git commit -m "feat: BelegChat Landingpage MVP"
git push origin main
```

Vercel deployed automatisch über die Verbindung mit `peerendees/belegchat-landing`.
Zieldomain: `belegchat.de` (DNS über Cloudflare einrichten).

---

*Dieser Prompt basiert auf dem BelegChat-Konzeptdokument (Stand März 2026) und den BERENT-CI-Rules unter `.cursor/rules/berent-ci.mdc`.*
