# LOCUS. – Standortanalyse für jeden Ort in Deutschland

**LOCUS** zeigt für jeden Ort in Deutschland, wie er angebunden ist, wo es grün ist und wie die Gebäude genutzt werden – Layer für Layer, im Maßstab. Und macht sichtbar, wo es Defizite gibt.

- **App:** `index.html` (Adresse dieser Website)
- **Demo mit Anleitung:** `demo.html` – Braunschweig, Burgplatz, Schritt für Schritt zum Ausprobieren

Studienprojekt Architektur · 2026

---

## Was LOCUS kann

| Bereich | Inhalt |
|---|---|
| **01 Mobilität** | Buslinien und -haltestellen, Fern-/Regionalbahn, S-Bahn & Stadtbahn, U-Bahn, Straßenbahn, Bahnhöfe, Hauptverkehrsstraßen, Parkplätze, Rad- und Fußwege |
| **02 Grün** | Spielplätze, private und öffentliche Grünflächen, Aufenthaltsflächen (inkl. Bänke), Bäume |
| **03 Nutzungen** | Gebäude eingefärbt nach Nutzung: Gesundheit, Einkaufen, Freizeit, Bildung, Wohnen |
| **04 Defizitanalyse** | Umkreis 300 / 500 / 800 m: Haltestellen und Grünflächen in Reichweite, Grünanteil, Linien, potenzielle Bauflächen – mit Steckbrief und Ampeln |

Weitere Funktionen:

- Ortssuche oder rote **Standort-Figur** aus dem Haus auf die Karte ziehen
- feste Maßstäbe 1 : 500 bis 1 : 5.000
- **PDF-Export im Maßstab** (A4–A1, hoch/quer) mit Legende, Nordzeichen und Plankopf
- eigenes **PDF-Blatt „Defizitanalyse“** mit Umkreiskarte, Legende und Steckbrief
- Info-Fenster beim Anklicken (Name, Adresse, Öffnungszeiten, Linien an Haltestellen, Link zu OpenStreetMap)
- Kartenbeschriftung auf Deutsch

## So benutzt ihr LOCUS

1. Website öffnen, auf **„Los geht’s →“** klicken.
2. Ort suchen oder die Figur aus dem Haus auf die Karte ziehen.
3. Maßstab wählen (zum Laden 1 : 5.000 oder näher).
4. Unter **Layer** die gewünschten Gruppen einschalten, dann **„Daten für diesen Ausschnitt laden“**.
5. Optional: **Defizitanalyse** – Umkreis wählen, „Analysieren“.
6. **PDF-Export:** Format, Ausrichtung, Maßstab und Titel wählen, Rahmen auf der Karte zurechtschieben, „PDF erstellen“.

Ein Internetzugang ist nötig. Es wird nichts installiert und keine Anmeldung gebraucht.

## Defizitanalyse – Richtwerte und Quellen

| Thema | Richtwert | Quelle |
|---|---|---|
| Haltestellen erreichbar | Bus/Tram ≤ 400 m, Bahn ≤ 600 m Luftlinie | Leitlinie zur Nahverkehrsplanung in Bayern (Kernbereich Ober-/Mittelzentrum) |
| Grünfläche erreichbar | öffentliche Grünfläche ≥ 0,5 ha in max. 300 m Luftlinie | WHO Europa (2016) |
| Grünanteil | mind. 10 % Grünfläche | BBSR, Handlungsziele Stadtgrün (2018) |
| Linien | gut ab 4 Linien mit Halt im Umkreis | eigene Setzung |

Die Prozentgrenzen der Ampeln (gut / mittel / Defizit) sind eigene Setzungen auf Basis dieser Richtwerte.

## Grenzen

- Alle Entfernungen sind **Luftlinie**, keine echten Fußwege.
- Grundlage sind **OpenStreetMap-Daten** – fehlt dort etwas, fehlt es auch in LOCUS. Auf dem Land ist oft weniger erfasst als in der Stadt.
- „Unbebaute Flächen in Blöcken“ können auch Gärten oder Höfe sein – ein Hinweis, kein Befund.
- Gebäude ohne bekannte Nutzung in Wohngebieten werden als „Wohnen (vermutet)“ gezeigt.
- Takte und Fahrpläne sind nicht erfasst.
- Der Maßstab auf dem Bildschirm ist nur ungefähr (96 dpi); exakt ist er im PDF.

## Dateien

| Datei | Inhalt |
|---|---|
| `index.html` | die App (eine einzige Datei, läuft im Browser) |
| `demo.html` | Demo mit Anleitung und fest eingebauten Daten für Braunschweig, Burgplatz |
| `README.md` | diese Beschreibung |

---

## Verwendete Bibliotheken

Alle Bibliotheken werden beim Öffnen von einem öffentlichen CDN geladen (jsDelivr, unpkg oder cdnjs als Ersatz).

| Bibliothek | Version | Wofür | Lizenz |
|---|---|---|---|
| [MapLibre GL JS](https://maplibre.org/) | 4.7.1 | interaktive Karte, Kartenbild für das PDF | BSD-3-Clause |
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | PDF-Erzeugung im Browser (wird erst beim ersten Export geladen) | MIT |
| [D3](https://d3js.org/) | 7 (7.9.0) | Globus auf der Startseite (Projektion und Zeichnen) | ISC |
| [world-atlas](https://github.com/topojson/world-atlas) | 2 (2.0.2), Datei `countries-110m.json` | Ländergrenzen für den Globus | ISC; Daten: Natural Earth (gemeinfrei) |
| [Niedersachsen-Cache](https://jade-hs-vibecoding-wpk.github.io/niedersachsen-cache/) (`nds-cache.js`, Jade Hochschule) | 1.1.0 | vorbereitete OSM-Daten für niedersächsische Städte (schnelleres Laden) | keine Lizenzangabe gefunden – bitte bei der Jade Hochschule erfragen |

Eigener Code (ohne Bibliothek): Laden und Auswerten der Daten, Defizitanalyse, Legende, PDF-Layout, Startseite.
Schrift: Helvetica Neue / Helvetica / Arial des eigenen Systems (keine Web-Schrift).

## Verwendete Dienste und Daten

| Dienst | Wofür | Lizenz / Bedingungen |
|---|---|---|
| [OpenStreetMap](https://www.openstreetmap.org/copyright) | alle Kartendaten | Open Database License (ODbL) – © OpenStreetMap-Mitwirkende |
| [Overpass API](https://wiki.openstreetmap.org/wiki/Overpass_API) – Server overpass-api.de, maps.mail.ru, overpass.private.coffee, overpass.kumi.systems | Abfrage der OSM-Daten | Software: GNU AGPL v3; Nutzung nach den Regeln der jeweiligen Server |
| [OpenFreeMap](https://openfreemap.org/) – Stil „Positron“ | Grundkarte | Projekt: MIT; Kartenschema OpenMapTiles (Code BSD-3-Clause, Design CC BY 4.0); Daten © OpenStreetMap |
| Esri „World Light Gray Base“ | Ersatz-Grundkarte, falls OpenFreeMap nicht erreichbar ist | Esri-Nutzungsbedingungen; Quellen: Esri, HERE, Garmin, © OpenStreetMap-Mitwirkende |
| [Nominatim](https://nominatim.org/) (nominatim.openstreetmap.org) | Ortssuche | Nutzungsrichtlinie der OSMF (höchstens 1 Anfrage pro Sekunde); Daten ODbL |
| [Photon](https://photon.komoot.io/) (komoot) | Ersatz für die Ortssuche | Software: Apache 2.0; faire Nutzung; Daten ODbL |

**Quellenangabe auf Karte und PDF:**
Kartendaten © OpenStreetMap-Mitwirkende (ODbL) · Grundkarte: OpenFreeMap, © OpenMapTiles
