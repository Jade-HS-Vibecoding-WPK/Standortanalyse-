# Konzeptblatt – Standortanalyse-App (Arbeitstitel folgt)

Stand: 17.11.2026, 16:55 – Schritte 1–7 gebaut, Schritt 7 (PDF-Export) noch nicht mit echten Daten getestet
**Aktuelle Datei im Projekt: `claude/standortanalyse_zwischenstand_2026-11-17.html`**
(ältere Datei `claude/standortanalyse_zwischenstand_2026-11-16.html` ist überholt)

## Morgen weitermachen – hier ansetzen
1. Datei `standortanalyse_zwischenstand_2026-11-17.html` herunterladen und im Browser öffnen (Safari/Firefox).
2. **PDF-Export testen:** Ausschnitt laden (1:2.500) → Layer einschalten → Abschnitt „PDF-Export“: Format, hoch/quer, Maßstab, Titel → „Rahmen auf der Karte zeigen“ → ggf. „Daten für den Rahmen laden“ → „PDF erstellen“.
   - Prüfen: Wird ein PDF heruntergeladen? Sieht es gut aus? Maßstab stimmt? (bei 1:2.500 muss die 100-m-Leiste 4 cm lang sein)
   - A4/A3 zuerst, dann A2/A1 (große Formate brauchen 10–30 s).
3. Danach Schritt 8: Feinschliff, Tablet-Test, Name der App.

## Grundprinzip (gilt im aktuellen Stand)
- Funktioniert für alle Orte in Deutschland, Daten live aus OpenStreetMap über Overpass (Internet nötig)
- Ladezeit je nach Serverauslastung ca. 1–2 Minuten (bei 1:2.500)
- Stadtwahl per Suchfeld und/oder freiem Zoomen/Verschieben; neuer Ort/Ausschnitt → alte Daten werden verworfen
- Daten per Knopf „Daten für diesen Ausschnitt laden“; bei Fehlern „Fehlende Daten nachladen“ (holt nur Fehlendes)
- Oberfläche auf Deutsch, für Laptop/Beamer und Tablet
- Layer-Menü: Hauptgruppen aufklappbar, Gruppenschalter „alle an/aus“ + Einzelschalter je Unterkategorie
- Anzahl gefundener Objekte neben jedem Layer; Legende unten rechts (nur aktive Layer)
- Straßennamen der Grundkarte ausschaltbar
- Info-Fenster beim Anklicken: Kategorie, Name, Art, Adresse, Öffnungszeiten, bei Haltestellen die Linien (Bus/S-Bahn), Link zu OSM

## Maßstab & PDF-Export
- Bildschirm: feste Stufen 1:500 / 1:1.000 / 1:2.000 / 1:2.500 / 1:5.000 (Bildschirm-Maßstab nur ungefähr, 96 dpi)
- PDF-Export (Schritt 7): Formate A4–A1, hoch/quer, Maßstab 1:500–1:5.000, Titel frei
  - Rahmen in Blattgröße in der Kartenmitte, Karte darunter verschieben
  - Blatt: Karte im exakten Maßstab, Titel, Legende (passt sich an: mehr Spalten/kleinere Schrift), Nordpfeil, Maßstabsleiste, „M 1:x“, Format, Datum, Quelle „© OpenStreetMap-Mitwirkende (ODbL) · Grundkarte OpenFreeMap, © OpenMapTiles“
  - Auflösung Kartenbild: A4/A3 200 dpi, A2 150 dpi, A1 120 dpi
  - PDF-Bibliothek jsPDF 2.5.1 (wird beim ersten Export aus dem Internet geladen)

## Layer (aktueller Stand = Version OHNE „Punkt 1“, bewusst so gewählt)
**Mobilität:** Buslinien #e3c46b · Bushaltestellen #c9a43a · Fern-/Regionalbahn #9e3128 · S-Bahn #c4473a · U-Bahn #d26a55 · Straßenbahn #de9378 · Bahnhöfe/Haltestellen #7f2820 · Hauptverkehrsstraßen #6a8caf · Parkplätze #a9bfd6 · Radwege #cf7fb0 · Fußwege #efc6df
- Linien liegen nebeneinander (Auto Mitte, Rad daneben, Bus außen; Gleise Mitte, S-Bahn daneben)

**Grün:** Spielplätze #bccb72 · Private Grünflächen #cbd8c2 · Öffentliche Grünflächen #94b98a (Parks, Rasen, Wiesen, Friedhöfe, Wald) · Aufenthaltsflächen #93c2ae (inkl. Bänke) · Bäume #557d4f

**Nutzungen (nur Gebäude werden eingefärbt):**
- Gesundheit: Krankenhäuser #a9383d · Zahnärzte #f5ccc6 · Fachärzte #ec9d93 · Allgemeinärzte #d9625f · Apotheken #c0517a
- Einkaufen: Supermärkte #4874a6 · Bäckereien #7ea3cf · Drogerien #4c9aa6 · Wochenmärkte #2f5b85 · Sonstige Läden #c4d8ee
- Freizeit: Gastronomie #e9c24f · Kultur #cf9532 · Sport #f3e2a2 (Sportplätze als Fläche mit Kontur #c8a94e) · Bars & Nachtleben #a8913f
- Bildung: Kitas #dcd0ec · Grundschulen #b49fdc · Weiterführende Schulen #8a6dc0 · Hochschulen #5c4795 · Bibliotheken #b083b8
- Wohnen #f2b37a: ausdrücklich als Wohnhaus eingetragen + Gebäude ohne Nutzung im Wohngebiet
- Regeln: Punkt im Gebäude → Gebäude; Punkt bis 20 m neben Gebäude → nächstes Gebäude; Fläche (z. B. Schulgelände) → alle Gebäude darauf; Gebäude ohne bekannte Nutzung bleiben grau

## Technik
- Eine HTML-Datei, per Doppelklick im Browser (getestet: Firefox/Windows, Safari/Mac)
- MapLibre GL 4.7.1; Grundkarte OpenFreeMap Positron (Notfall Esri Light Gray)
- Suche: Nominatim, Ersatz Photon
- Overpass: Hauptserver overpass-api.de, Ersatz mail.ru / private.coffee / kumi.systems; max. 2 Abfragen gleichzeitig; bei „zu viele Anfragen“ (429) 20/40 s warten und denselben Server erneut fragen; App merkt sich zuletzt funktionierende Server
- Statusanzeige + Ladeprotokoll in der Seitenleiste

## Entscheidungen & Erkenntnisse (Verlauf)
- CARTO-Karten verlangen bei lokalen Dateien einen API-Schlüssel → nicht nutzbar
- Bei Claude veröffentlichte Link-Seiten können keine externen Kartendaten laden → HTML-Datei
- Schnelle Variante „Nutzungen aus der Grundkarte“ (OpenFreeMap-Kacheln) getestet und **verworfen**: Nutzungen fehlerhaft (u. a. ganze Häuserblöcke als Ärzte, weil die Grundkarte vielen Gebäuden dieselbe Kennung gibt). Ein Fix wurde gebaut, das Team bleibt aber bei der Overpass-Version.
- „Punkt 1“ (Ärzte zusammengefasst, Krankenhäuser extra, ohne Bänke/private Gärten) wurde gebaut, das Team hat sich am 17.11. bewusst für die Version **ohne** Punkt 1 entschieden.
- Eigene Datenkacheln (PMTiles) verworfen: kein Rechner mit 16 GB RAM, keine Zeit für Einrichtung.
- Offene Idee für mehr Tempo: **GitHub Actions** bereitet OSM-Daten wöchentlich automatisch auf, App liegt auf GitHub Pages (Link). Team hat GitHub-Konto; geht auch ohne Claude-Zugriff (Dateien hochladen + Klicks). Noch nicht entschieden („erstmal noch nicht“).
- Weitere geprüfte Quellen verworfen: ohsome-API (v1 wird am 30.11.2026 abgeschaltet, v2 braucht API-Schlüssel), Google Places (kostenpflichtig/Lizenz), Open Data der Städte (uneinheitlich).

## Fahrplan
1. ✅ Kartengerüst: Karte, Suche, Maßstab
2. ✅ Layer-Menü + Legende
3. ✅ Grün
4. ✅ Mobilität
5. ✅ Nutzungen
6. ✅ Info beim Anklicken
7. 🔧 PDF-Export im Maßstab – gebaut, **Test mit echten Daten steht aus**
8. Feinschliff, Tablet-Test, Namensgebung
9. (optional) Online stellen über GitHub Pages / schnellere Daten über GitHub Actions

## Arbeitsweise
Schrittweise, nach jedem Schritt kurze Pause zum Nachvollziehen und Feedback.
