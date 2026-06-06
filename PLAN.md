# PLAN – DMK Bau Startseite (Astro-Nachbau)

---

## 1. Komponentenliste

| Datei | Verantwortlich für |
|---|---|
| `src/layouts/BaseLayout.astro` | `<html>`, `<head>`, Meta/OG-Tags, Font-Preload, JSON-LD, Slot für Seiteninhalt |
| `src/components/Header.astro` | Sticky Header, Logo, Nav-Links, Burger-Toggle (vanilla JS via `<script>`) |
| `src/components/Hero.astro` | Hero-Section: Bild-Overlay, H1, Lead, Claim, CTAs, 4 Trust-Badges |
| `src/components/Unternehmen.astro` | Section 2: Headline, 4 Bullet-Punkte (Glasskarten), Inhaber-Foto + Caption |
| `src/components/Leistungen.astro` | Section 3: 8-Karten-Grid mit Bild, Titel, Text, Chip, grünem Button |
| `src/components/Bewertungen.astro` | Section 4: Bewertungs-Slider (horizontal scroll + Prev/Next-Pfeile + Volltext-Modal) |
| `src/components/FAQ.astro` | Section 5: 2-Spalten-Akkordeon mit CSS-Grid-Row-Trick |
| `src/components/Kontakt.astro` | Section 6: Info-Karte (Telefon, Bullets, Map-Placeholder), Kontaktformular |
| `src/components/SideDock.astro` | Schwebende Kontaktkarte rechts (WhatsApp, Mobil, Festnetz, E-Mail, Adresse) |
| `src/components/PartnerSlider.astro` | CSS-Marquee mit 5 Partner-Logos (kein JS nötig) |
| `src/components/Footer.astro` | 4-Spalten-Footer (Unternehmen, Rechtliches, Kontakt, Social) + Copyright |
| `src/components/LeistungenModals.astro` | 3 Auswahl-Modals (Innenausbau, Badsanierung, Außenanlagen) mit Unterseiten-Links |
| `src/components/CookieBanner.astro` | Consent-Banner (Notwendig/Statistik/Marketing, localStorage, DSGVO) |

---

## 2. Baureihenfolge (Sektion für Sektion)

1. **Astro-Gerüst** – `npm create astro`, Static-Output konfigurieren, `public/images/` mit Originals befüllen
2. **BaseLayout** – `<head>` komplett: Charset, Viewport, Title, Meta-Description, OG, Font-Preload, Favicon, LocalBusiness JSON-LD, Design-Tokens als `:root`-Variablen, global CSS-Reset
3. **Header** – Logo, Nav-Links, Burger-Menü; JS-Toggle
4. **Hero** – Hintergrundbild-Overlay, H1, Lead, Claim, zwei CTAs, Trust-Rail (4 Badges)
5. **Unternehmen** (Sec 2) – Text-Spalte + Foto-Spalte, 4 Glasskarten-Bullets
6. **Leistungen** (Sec 3) – 8-Karten-Grid; Button auf Karte 1–3 öffnet Modals
7. **LeistungenModals** – 3 Modals (Innenausbau, Bad, Außen); JS öffnet/schließt
8. **Bewertungen** (Sec 4) – Slider mit 10 Reviews; Prev/Next; Volltext-Modal
9. **FAQ** (Sec 5) – 2-Spalten-Akkordeon; CSS Grid Row Transition
10. **Kontakt** (Sec 6) – Info-Karte + Map-Placeholder + Formular
11. **SideDock** – Floating-Panel rechts; Toggle-JS
12. **PartnerSlider** – Pure-CSS-Marquee
13. **Footer** + Social-Buttons + Modals einbinden
14. **CookieBanner** – localStorage-Logik
15. **SEO-Feinschliff** – sitemap.xml, robots.txt, OG-Bild festlegen

---

## 3. Design-Tokens & CSS-Erkenntnisse

### Farbpalette (exakt aus Original-CSS)

| Token | Wert | Verwendung |
|---|---|---|
| `--brand` | `#369142` | Primärfarbe Grün (Header-BG, Buttons, Akzente) |
| `--brand-2` | `#2B7A37` | Dunkleres Grün (Hover, Verläufe) |
| `--brand-alt` | `#3A7D44` | Leicht abweichendes Grün (Sec 4, Footer, Dock) |
| `--brand-alt-2` | `#2E6C3A` | Dunkel-Pendant zu brand-alt |
| `--text` | `#1f1f1f` | Fließtext |
| `--muted` | `#6b7280` | Sekundärtext |
| `--muted-2` | `#4a5157` | Dunklerer Subtext (Sec 2/3/5) |
| `--card` | `#ffffff` | Karten-Hintergrund |
| `--bg` | `#f9fafb` | Seiten-Hintergrund |
| `--ring` | `#e3e8ee` | Border-Farbe |
| `--shadow` | `0 12px 38px rgba(0,0,0,.08)` | Card-Shadow |
| `--radius` | `18px` | Border-Radius Cards |
| `--speed` | `160ms` | Standard-Transition-Dauer |
| Gold/Stars | `#FFD166` / `#FFC107` | Sternbewertungen |
| Google Green | `#34A853` | "Verifiziert via Google"-Label |
| Cookie Green | `#4CAF50` | Cookie-Banner-Akzent |

### Schriften

- **Familie:** `"Quicksand", system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif`
- **Gewichte:** 400, 500, 600, 700, 800 (Google Fonts: 400;600;700)
- **Laden:** Non-render-blocking via `rel="preload"` + `onload` + `<noscript>`-Fallback

### Spacing-System

| Bereich | Wert |
|---|---|
| Linker Einzug alle Hauptsektionen (≥1200px) | `200px` |
| Linker Einzug @max-width 1200px | `140px` |
| Linker Einzug @max-width 900px | `26px` |
| Section-Padding (top/bottom) | `70px` (FAQ `70px / 84px`, Kontakt `70px / 90px`) |
| Container max-width (Hero, Sec 2–4) | `1440px` |
| Container max-width (Footer) | `1200px` |

### Breakpoints

| px | Änderung |
|---|---|
| 400 | Trust-Rail 2-spaltig |
| 520 | Kontakt-Phones 2-spaltig; Sec6-Title-Sub font-size |
| 560 | Sub-List in Mega-Menu 2-spaltig |
| 600 | Partner-Section Padding reduziert, Logos verkleinert |
| 640 | Formular-Fieldset 2-spaltig |
| 768 | Leistungen-Grid 2-spaltig; diverse Mobile-Tweaks |
| 820 | Footer 4-spaltig |
| 900 | Hero-Overlay-Gradient ändert sich; Padding → 26px links; Hero min-height auto |
| 980 | Sec 2 Grid 2-spaltig; FAQ 2-spaltig; Kontakt 2-spaltig |
| 1024 | Nav: Burger-Toggle sichtbar, Menu wird Dropdown |
| 1100 | Leistungen 3-spaltig |
| 1200 | Padding → 140px links |
| 1400 | Leistungen 4-spaltig |

### Animationen & Transitions (exakt)

| Element | Eigenschaft | Wert |
|---|---|---|
| Hero-Card (initial) | `animation` | `fadeUp 820ms cubic-bezier(.2,.7,.2,1) both` |
| `@keyframes fadeUp` | from→to | `opacity:0; translateY(26px)` → `opacity:1; translateY(0)` |
| Sec 6 Grid-Kinder | `animation` | `fadeUp6 .6s cubic-bezier(.2,.7,.2,1) both` (gleiche Keyframes) |
| Partner-Marquee | `animation` | `partner-marquee 70s linear infinite`; `translateX(0)` → `translateX(-50%)` |
| Partner hover | `animation-play-state` | `paused` (Slider stoppt) |
| Partner-Logo hover | `transform` | `scale(1.15)` + `filter:none` (Farbe erscheint) |
| Leistungen Card hover | `transform` + `box-shadow` | `translateY(-3px)` + `0 12px 24px rgba(0,0,0,.12)` in `0.25s ease` |
| Leistungen Card Bild hover | `transform` | `scale(1.05)` in `0.4s ease` |
| FAQ Akkordeon (CSS Grid-Trick) | `grid-template-rows` | `0fr` → `1fr` in `0.25s ease` + padding `0.25s ease` |
| FAQ Item hover | `transform` | `translateY(-1px)` + border + shadow in `0.2s` |
| Mobile-Menü | `max-height` + `opacity` + `transform` | `0; 0; translateY(-8px)` → `260px; 1; translateY(0)` in `.26s / .2s / .22s ease` |
| Trust-Badge hover | `transform` + `background` + `border` | `translateY(-2px)` in `0.18s ease` |
| `.btn-primary` hover | `transform` + `filter` | `translateY(-2px)` + `brightness(0.95)` in `.15s / .2s` |
| `.btn-ghost` hover | `background` + `border` | in `0.2s` |
| Bewertungen Modal | `transform` + `opacity` | `scale(.96); 0` → `scale(1); 1` in `0.2s ease` |
| Reviews Card hover | `transform` + `box-shadow` | `translateY(-2px)` in `0.25s` |
| SideDock Panel | `transform` + `opacity` + `visibility` | `translateX(100%)` → `translateX(0)` in `.35s / .25s ease; step-end` |
| SideDock Item hover | `transform` + `color` | `translateX(-2px)` in `0.18s ease` |
| Footer Social-Button hover | `transform` | `translateY(-4px)` in `0.25s ease` |
| Footer Link hover | `transform` + `color` | `translateY(-2px) scale(1.1)` + brand-green in `0.25s ease` |
| Geo-Highlight hover | `background-image` | Grüngelber Unterstrich `rgba(54,145,66,.45)` |
| Card (global) hover | `transform` | `translateY(-4px)` + shadow in `var(--speed)=160ms` |

---

## 4. JavaScript-Bausteine & Astro-Islands

Alle Interaktionen sind in **Vanilla JS** geschrieben → kein Framework. In Astro landen die Scripts als `<script>` direkt im `.astro`-File (kein `client:load` nötig).

| Modul | Wo | Art |
|---|---|---|
| Burger-Menü toggle | `Header.astro` | `<script>` (DOMContentLoaded) |
| FAQ-Akkordeon toggle | `FAQ.astro` | `<script>` (inline, querySelectorAll) |
| Bewertungen Slider (prev/next + keyboard) | `Bewertungen.astro` | `<script>` IIFE |
| Bewertungen Volltext-Modal (open/close/Escape) | `Bewertungen.astro` | im selben Script |
| Leistungen-Modal (Innenausbau) | `LeistungenModals.astro` | `<script>` DOMContentLoaded; Trigger: `[data-innenausbau-card]` |
| Leistungen-Modal (Bad) | `LeistungenModals.astro` | dito; Trigger: `[data-bad-card]` |
| Leistungen-Modal (Außen) | `LeistungenModals.astro` | dito; Trigger: `[data-aussen-card]` |
| SideDock toggle | `SideDock.astro` | `<script>` click + outside-click |
| Cookie-Banner show/hide (localStorage) | `CookieBanner.astro` | `<script>` cbAccept/cbSave/cbReject |
| reCAPTCHA Lazy Load via IntersectionObserver | `Kontakt.astro` | `<script>` (Platzhalter: lädt erst nach Consent) |
| Kontaktformular Submit (AJAX) | `Kontakt.astro` | `<script>` (Platzhalter-Endpoint) |
| Erfolgs-Popup nach Formular | `Kontakt.astro` | im selben Script |

> **Kein echtes Astro-Island nötig** (kein React/Vue). Alle `<script>`-Tags werden von Astro gebündelt und ans Ende des `<body>` gestellt.

---

## 5. Dynamische / Backend-Teile → Platzhalter

| Feature | Platzhalter-Strategie |
|---|---|
| **Formular-Endpoint** | `action="/api/contact"` (Kommentar: echte URL kommt später); Submit-Handler zeigt Erfolgs-Popup, wirft keinen Fehler |
| **reCAPTCHA v3** | Script-Tag mit Site-Key vorhanden, aber nur nach Marketing-Consent laden; Im Platzhalter: Consent-Logik prüft `localStorage.cookieConsent.mark` |
| **Google Maps Embed** | `<iframe>` liegt im DOM, wird aber per JS nur eingesetzt, wenn Consent erteilt; Default: Platzhalter-Div mit Adresstext + Link zu Google Maps |
| **Google Bewertungen** | Section 4 enthält die 10 hart codierten Reviews aus dem Original; echter Widget-Endpoint folgt später (Kommentar im Code) |

---

## 6. Offene Fragen an dich

### A) Mega-Menü "Leistungen" im Header
Das Original-HTML enthält einen fertigen JS-Block für ein Mega-Menü (mit Subpanels für Innenausbau, Außen, Rohbau, Immobilien, Fördermittel), aber die zugehörigen HTML-Elemente (`#leistungenBtn`, `#megaMenu`) fehlen im aktuellen Stand – der Nav-Link "Leistungen" ist ein einfaches `<a>`. 

**Frage:** Sollen wir das Mega-Menü komplett implementieren (wäre deutlich aufwendiger), oder reicht der einfache Anchor-Link wie im aktuellen Original-DOM?

### B) Service-Auswahl im Kontaktformular
Das JS-Script im Formular referenziert eine Service-Select-Dropdown-Komponente (`#serviceSelect`, `#serviceTrigger`, Checkboxen pro Gewerk), aber das HTML dafür fehlt im aktuellen Stand. Das Formular hat stattdessen ein `<input type="hidden" value="Allgemeine Anfrage">`.

**Frage:** Service-Dropdown implementieren (wie im JS beschrieben), oder weglassen und beim Hidden-Input bleiben?

### C) Google Maps Consent-Gate
Im Original lädt die Map-iFrame ohne Consent-Prüfung. Laut CLAUDE.md soll sie erst nach aktiver Einwilligung geladen werden (DSGVO-konform).

**Frage:** Soll der Map-Platzhalter einen grünen "Karte laden"-Button zeigen (nach Klick wird Consent gesetzt und iframe eingeblendet), oder reicht ein statischer Platzhalter mit Adresse + "In Google Maps öffnen"-Link?

### D) reCAPTCHA Consent
Aktuell lädt das Original reCAPTCHA per IntersectionObserver sobald der Nutzer ans Formular scrollt – ohne Consent-Prüfung. CLAUDE.md fordert Consent-First.

**Frage:** Formular ohne reCAPTCHA funktionsfähig halten (Submit geht durch, Token ist leer/Platzhalter), oder Formular-Button erst nach Marketing-Consent freischalten?

### E) Favicon-Format
Original nutzt `images/dmk-bau-reichelsheim-favicon.webp`. Astro/Browser erwarten üblicherweise `.ico` oder `.svg`.

**Frage:** WebP-Favicon so übernehmen, oder soll ich zusätzlich ein `.ico` anlegen (gleiche Quelle, nur umgewandelt)?

### F) Öffnungszeiten-Anzeige im Footer
Im Footer steht `©2025 DMK Bau`. Da wir 2026 sind, soll das aktualisiert werden, oder 1:1 aus dem Original übernehmen?

---

*Warte auf Freigabe/Antworten vor dem ersten Sektion-Build.*
