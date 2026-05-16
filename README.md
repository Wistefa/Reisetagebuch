# Reisetagebuch PWA

**Live:** https://wistefa.github.io/Reisetagebuch/

Eine browserbasierte Reisetagebuch-App – läuft vollständig lokal ohne Server, ohne Login, ohne Cloud. Optimiert für iPhone, iPad und Desktop.

---

## Features

### Tagebuch
- Beliebig viele Reisen mit Tageseinträgen
- Datum, Ort, freier Text, beliebig viele Fotos mit Bildunterschriften
- Kartenvorschau via OpenStreetMap

### Layout-Editor
Fotos per Drag & Drop (Desktop) oder Tap-to-Place (iPad) im Text positionieren:
- **Links / Rechts:** Text fließt um das Foto herum
- **Zentriert:** Foto über volle Breite
- Breite frei einstellbar, Position im Text verschiebbar
- Layout wird pro Eintrag gespeichert und beim PDF-Export verwendet

### Deckblatt-Editor
Individuelle Titelseite für das Reise-PDF:
- Fotos frei auf der A4-Seite positionieren und skalieren
- Fotozone-Höhe einstellbar (30–75% der Seite)
- Titel, Untertitel, Datum und Einleitungstext editierbar

### PDF-Export
- **Einzelner Eintrag:** PDF mit Layout-Editor-Layout (Textfluss um Fotos)
- **Gesamte Reise:** Deckblatt + alle Einträge mit gespeicherten Layouts
- Emojis werden korrekt gerendert
- DIN A4, druckoptimiert

### Routen-Karte
- KML / GPX importieren und auf Karte anzeigen
- GPX-Export für MapOut und andere Apps

### Export / Import
- Alle Daten (Reisen, Einträge, Fotos) als JSON sichern
- Import auf anderen Geräten möglich (iPhone ↔ iPad)

### PWA
- Installation auf dem Home-Bildschirm (Safari → Teilen → Zum Home-Bildschirm)
- Vollständig offline nutzbar nach erstem Laden

---

## Datenspeicherung

| Daten | Speicherort |
|---|---|
| Reisen & Einträge (Text, Layout) | `localStorage` |
| Fotos | `IndexedDB` |
| Kein Server, keine Cloud | Alles bleibt auf dem Gerät |

> **Tipp:** Regelmäßiger JSON-Export in iCloud Drive schützt vor Datenverlust beim Löschen des Browser-Cache.

---

## Technologie

| Komponente | Technologie |
|---|---|
| Framework | React 18 (CDN / Babel, kein Build) |
| Karte | Leaflet.js + OpenStreetMap |
| PDF | jsPDF (clientseitig) |
| Emoji im PDF | Canvas-Rendering |
| Fotos | IndexedDB |
| Offline | Service Worker |
| Hosting | GitHub Pages |

**Eine einzige `index.html`** – kein Build-Prozess, kein Server, kein Framework-Setup.

---

## Changelog

| Version | Datum | Änderungen |
|---|---|---|
| 2.1 | 16.05.2026 | Deckblatt-Editor (Drag & Drop, editierbare Texte), PDF nutzt Layout-Editor-Layouts, Emoji-PDF-Support, EXIF-Fix, Speicheroptimierung |
| 2.0 | 16.05.2026 | Layout-Editor mit Textfluss, Touch-Support, Layout-Speicherung, GitHub Pages |
| 1.0 | 06.03.2026 | Erste Version: Tagebuch, Fotos, Karte, PDF, PWA |
