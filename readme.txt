================================================================================
  Reisetagebuch – Progressive Web App (PWA)
  Version 2.0 | Live: https://wistefa.github.io/Reisetagebuch/
================================================================================

ÜBERSICHT
---------
Das Reisetagebuch ist eine browserbasierte App (PWA) zum Festhalten von
Reiseerlebnissen. Sie läuft vollständig lokal im Browser – ohne Server,
ohne Login, ohne dauerhafte Internetverbindung (nach dem ersten Laden).
Optimiert für iPhone, iPad und Desktop.


WAS KANN DIE APP?
-----------------

1. STARTSEITE – ALLE REISEN
   - Beliebig viele Reisen anlegen, bearbeiten und löschen
   - Kacheln mit Cover-Foto (erstes Foto aus den Einträgen), Reisename,
     Zielort, Zeitraum und Anzahl Einträge
   - Neue Reise mit Name, Zielort, Abreise- und Rückkehrdatum

2. REISE-ÜBERSICHT – TAGESEINTRÄGE
   - Chronologische Liste aller Tageseinträge als Karten
   - Jede Karte zeigt: Datum, Wochentag, Ort, Text-Vorschau, Foto-Vorschau
   - Neuen Tageseintrag hinzufügen (+ Button)

3. TAGESEINTRAG – ERFASSEN & BEARBEITEN
   - Datum (frei wählbar)
   - Ort / Stadt (manuell eingeben)
   - Kartenvorschau: Ort per „🗺️ Karte"-Button auf OpenStreetMap anzeigen
   - Freier Tagebuchtext (mehrzeilig)
   - Fotos aus der iPhone/iPad-Fotomediathek hinzufügen (mehrere gleichzeitig)
   - Jedes Foto mit einer Bildunterschrift versehen

4. TAGESEINTRAG – ANSICHT
   - Datum groß im Journal-Stil (Wochentag, Tag + Monat, Jahr)
   - Ort mit interaktiver Kartenvorschau (OpenStreetMap)
   - Alle Fotos mit Bildunterschriften
   - Tagebuchtext

5. LAYOUT-EDITOR – PDF MIT TEXTFLUSS
   Über den Button „📐 PDF" in der Eintrag-Ansicht öffnet sich der
   Layout-Editor. Hier wird das PDF visuell gestaltet bevor es erzeugt wird.

   Bedienung:
   - Linkes Panel: alle Fotos des Eintrags als Vorschau
   - iPad / Touch: Foto antippen (wird orange markiert) → Drop-Zone im
     Text antippen → Foto erscheint an dieser Stelle
   - Mac / Desktop: Foto per Drag & Drop in eine Drop-Zone ziehen
   - Text fließt automatisch um die Fotos herum (Float-Layout)
   - Foto anklicken/antippen → Buttons erscheinen: ◀ Links · ■ Mitte · Rechts ▶
   - Breite per Schieberegler oder ↘-Anfasser anpassen
   - Position im Text: Buttons „▲ Höher" und „▼ Tiefer"
   - Rechtes Panel: alle Einstellungen für das ausgewählte Foto

   Layout speichern und wiederherstellen:
   - Button „💾 Layout speichern" sichert die Anordnung im Eintrag
   - Beim nächsten Öffnen des Editors wird das Layout automatisch geladen
   - Orangener Punkt am 📐 PDF Button = Layout bereits gespeichert
   - Ideal für lange Reisen: jeden Tag Layout einrichten, speichern,
     später in Ruhe das PDF erzeugen

   PDF-Ausgabe:
   - Text fließt seitlich neben den Fotos (Spaltenlayout)
   - Fotos können links, rechts oder zentriert (volle Breite) platziert werden
   - Seitenkopf: Datum, Wochentag, Ort
   - Seitenfußzeile: Reisename, Seitenzahl

6. PDF-EXPORT – KOMPLETTE REISE
   Der Button „📄 PDF" in der Reise-Übersicht erstellt ein druckoptimiertes
   PDF der gesamten Reise für DIN A4:

   Aufbau:
   - Deckblatt: Reisename, Zielort, Zeitraum, Anzahl Einträge
   - Ein Kapitel pro Tageseintrag (jeweils neue Seite)
   - Automatische Seitenumbrüche
   - Fußzeile: Reisename, Datum, Seitenzahl

7. ROUTEN-KARTE
   - KML- oder GPX-Datei importieren (z.B. aus Google Maps)
   - Alle Tageseinträge mit GPS-Koordinaten werden eingezeichnet
   - Export zurück als GPX für MapOut oder andere Apps

8. EXPORT / IMPORT – DATENSICHERUNG
   Über die Buttons 📤 / 📥 auf der Startseite:

   Export (📤):
   - Alle Reisen, Einträge und Fotos als eine JSON-Datei sichern
   - Datei kann in iCloud Drive abgelegt werden

   Import (📥):
   - JSON-Datei laden und alle Daten wiederherstellen
   - Anwendungsfall: Daten zwischen Geräten teilen (iPhone ↔ iPad)

9. PWA – INSTALLATION AUF DEM HOMESCREEN
   - Safari öffnen → https://wistefa.github.io/Reisetagebuch/
   - Teilen-Symbol → „Zum Home-Bildschirm"
   - App startet dann wie eine native App (Vollbild, kein Browser-UI)
   - Funktioniert auch offline nach der ersten Installation


WO WERDEN DIE DATEN GESPEICHERT?
---------------------------------

  DAUERHAFT AUF DEM GERÄT:

  Reisen & Einträge (Text, Ort, Datum, Layout):
  → Browser-localStorage, Schlüssel: "reisetagebuch_trips_v1"
                                      "reisetagebuch_entries_v1"

  Fotos:
  → Browser-IndexedDB, Datenbank: "reisetagebuch_db"
    (IndexedDB ist für große Datenmengen wie Bilder geeignet)

  WICHTIGE HINWEISE:
  - Alle Daten bleiben ausschließlich auf dem jeweiligen Gerät.
  - Kein Server, keine Cloud, keine Datenübertragung ins Internet
    (außer zum Laden der Kartenkacheln von OpenStreetMap).
  - Beim Löschen des Browser-Cache gehen alle Daten verloren.
    → Regelmäßiger Export (📤) in iCloud Drive empfohlen!
  - Auf einem anderen Gerät sind keine Daten vorhanden
    (Übertragung nur per Export/Import möglich).


TECHNISCHE DETAILS
------------------
- Eine einzige HTML-Datei (index.html) – kein Build-Prozess, kein Server
- Framework:       React 18 (via CDN / Babel)
- Karte:           Leaflet.js + OpenStreetMap (kostenlos, kein API-Key)
- Geocoding:       Nominatim / OpenStreetMap (kostenlos, kein API-Key)
- PDF-Erzeugung:   jsPDF (clientseitig im Browser, mit Float-Textfluss)
- Layout-Editor:   Drag & Drop (Desktop) + Tap-to-Place (iPad/Touch)
- Foto-Speicher:   IndexedDB (im Browser des Geräts)
- PWA:             Service Worker (sw.js) für Offline-Betrieb
- PWA-Manifest:    manifest.json (Icons, App-Name, Farben)
- Hosting:         GitHub Pages (https://wistefa.github.io/Reisetagebuch/)


DATEIEN
-------
  index.html         – die komplette App
  manifest.json      – PWA-Konfiguration
  sw.js              – Service Worker für Offline-Betrieb
  icon-192.png       – App-Icon (Android / PWA)
  icon-512.png       – App-Icon (Splash Screen)
  readme.txt         – diese Datei


CHANGELOG
---------
  v2.0  16.05.2026  Layout-Editor mit Textfluss um Fotos, Touch-Support iPad,
                    Layout-Speicherung pro Eintrag, GitHub Pages Hosting
  v1.0  06.03.2026  Erste Version: Tagebuch, Fotos, Karte, PDF, PWA

================================================================================
