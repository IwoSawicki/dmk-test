# DMK Bau – Website-Nachbau

## Ziel
1:1-Nachbau der bestehenden Website dmk-bau.de als erstes Projekt.
Zuerst nur die **Startseite**. Unterseiten kommen später in einer zweiten Phase.
Die Seite soll optisch und im Verhalten nicht vom Original zu unterscheiden sein.

## Stack
- Astro, statisches Output (kein SSR nötig).
- Styling: scoped CSS direkt in den Astro-Komponenten. Werte (Farben, Abstände,
  Schriftgrößen) **exakt aus dem Original-CSS übernehmen**, nicht schätzen.
- Interaktivität nur dort als JS-Island, wo das Original sie hat. Sonst kein JS.
- Keine zusätzlichen Libraries ohne Rückfrage.

## Quelle
- Die komplette Originalseite liegt gespiegelt in `./original/` (HTML, CSS, JS, Bilder).
- `./original/` ist die **Wahrheit** für alle Texte, Farben, Abstände, Schriften,
  Animationen und Bilder. Im Zweifel dort nachschauen, nicht raten.
- Bilder aus `./original/images/` direkt übernehmen (WebP), nicht neu generieren.

## Genauigkeitsregeln
- Exakte Hex-Farben, px-/rem-Werte und Schriftgrößen aus dem Original.
- Schriften identisch einbinden (gleiche font-family und Gewichte).
- Hover-States, Transitions und Scroll-Animationen identisch: gleiche Dauer, gleiches Easing.
- Responsive Verhalten an denselben Breakpoints.
- Alle deutschen Texte 1:1 aus dem Original übernehmen, nichts umformulieren.

## Sektionen der Startseite (als Komponenten)
1. Sticky-Header: Logo + Navigation (Unternehmen, Leistungen, Kontaktformular, Telefon-CTA)
2. Hero: Headline, Beschreibung, zwei CTAs, Google-Bewertungs-Badge, drei Trust-Badges
3. Über uns / Unternehmen: Werte, vier Punkte, Foto + Name des Inhabers
4. Leistungen: Grid mit Leistungs-Karten (Bild, Titel, Text, Link)
5. Bewertungen: Google-Reviews-Bereich
6. FAQ: Akkordeon
7. Kontakt: Text, Direktkontakt, eingebettete Google Map, Kontaktformular
8. Partner-/Marken-Logo-Slider
9. Footer: Unternehmen, Rechtliches, Kontakt, Social, Copyright

## Interaktive Komponenten (Verhalten 1:1)
- Sticky-Header
- Leistungs-Auswahl-Modals ("Welche Art von Badsanierung / Außenanlage / Innenausbau planen Sie?")
- FAQ-Akkordeon
- Cookie-Consent-Banner (Notwendig / Statistik / Marketing; Alle akzeptieren / Auswahl speichern / Ablehnen)
- Kontaktformular + "Vielen Dank"-Bestätigung
- WhatsApp-Button (schwebend)
- Partner-Logo-Slider

## Dynamische / Backend-abhängige Teile → vorerst nur Platzhalter mit Kommentar
- Formular-Versand (Endpoint kommt später)
- reCAPTCHA (erst nach Cookie-Consent laden)
- Google-Bewertungen (Widget/Daten kommen später)
- Google-Maps-Einbettung (erst nach Consent laden)
Diese nicht weglassen, sondern klar kommentiert als Platzhalter anlegen.

## Eckdaten (Quelle: Original; im Zweifel ./original/)
- Inhaber: Dariusz Krzysztoń
- Adresse: Heidelberger Straße 5, 64385 Reichelsheim (Odenwald)
- Mobil: 0160 7791280 · Festnetz: 06164 5039805
- E-Mail: info@dmk-bau.de
- Öffnungszeiten: Mo–Fr 09:00–17:00, Sa–So geschlossen
- Social: Facebook, Instagram (@dmkbau), TikTok (@dmkbau)

## SEO (gleich ins Template, da es später wiederverwendet wird)
- Saubere title / meta-description / OG-Tags pro Seite (aus Original übernehmen)
- LocalBusiness JSON-LD mit den Eckdaten oben
- sitemap.xml + robots.txt

## DSGVO
- reCAPTCHA und Google Maps erst nach aktiver Einwilligung über das Consent-Banner laden.

## Arbeitsweise
- Erst Plan, dann Code. Vor größeren Schritten kurz abstimmen.
- In kleinen Schritten bauen: eine Sektion fertig und geprüft, dann die nächste.
- **Bei Unklarheiten nachfragen, statt zu raten.**
- Sauberes, semantisches, wartbares Markup. Keine toten Reste.
