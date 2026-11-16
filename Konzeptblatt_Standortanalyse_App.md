# Konzeptblatt – Standortanalyse-App (Arbeitstitel folgt)

Stand: 16.11.2026, 14:55 – Schritte 1–4 fertig, Schritt 5 (Nutzungen) in Arbeit
Aktuelle Datei im Projekt: `claude/standortanalyse_zwischenstand_2026-11-16.html`

## Grundprinzip
- Funktioniert für alle Orte in Deutschland, Daten live aus OpenStreetMap (Internet nötig)
- Stadtwahl per Suchfeld und/oder freiem Zoomen/Verschieben
- Daten werden per Knopf „Daten für diesen Ausschnitt laden“ geladen
- Oberfläche auf Deutsch, für Laptop/Beamer und Tablet
- Layer-Menü: Hauptgruppen aufklappbar, jede Unterkategorie mit eigenem Schalter, jede Gruppe zusätzlich mit Schalter „alle an/aus“
- Anzahl gefundener Objekte neben jedem Layer
- Legende als Kasten unten rechts auf der Karte, zeigt nur aktive Layer
- Straßennamen der Grundkarte ausschaltbar
- Klick auf Gebäude/Haltestelle zeigt Infos (Name, Art, bei Haltestellen die Linien) – folgt in Schritt 6
- Dezente, leicht entsättigte Farben; Unterscheidung innerhalb einer Gruppe über Helligkeit/Unterton

## Maßstab & Export
- Auswahlmenü mit festen Stufen: 1:500 / 1:1.000 / 1:2.000 / 1:2.500 / 1:5.000
- Freies Herauszoomen zum Navigieren möglich (dann nur Grundkarte)
- Daten-Knopf nur zwischen 1:500 und 1:5.000 aktiv
- Bildschirm-Maßstab ist nur ungefähr (Annahme 96 dpi); exakter Maßstab über PDF-Export (Schritt 7)

## Grundkarte (immer sichtbar)
- OpenFreeMap Positron: Hintergrund weiß, Straßen grau, Gebäude hellgrau, Wasser zartes Graublau (#dde7ee)

## 1. Mobilität
| Layer | Farbe | Quelle in OSM |
|---|---|---|
| Buslinien | #e3c46b | Bus-Linienverläufe (Relationen), auf Ausschnitt zugeschnitten |
| Bushaltestellen | #c9a43a | highway=bus_stop |
| Fern- & Regionalbahn | #9e3128 | railway=rail ohne Nebengleise |
| S-Bahn | #c4473a | S-Bahn-Linien (route=light_rail, Linien „S + Nummer“), railway=light_rail |
| U-Bahn | #d26a55 | railway=subway |
| Straßenbahn | #de9378 | railway=tram |
| Bahnhöfe & Haltestellen | #7f2820 | railway=station/halt/tram_stop |
| Hauptverkehrsstraßen | #6a8caf | Autobahn bis Nebenstraße (secondary) |
| Parkplätze | #a9bfd6 | amenity=parking ohne Tiefgaragen |
| Radwege | #cf7fb0 | Radwege, Fahrradstraßen, Straßen mit Radspur |
| Fußwege | #efc6df | footway, pedestrian, path, steps, living_street |

- Linien liegen nebeneinander statt übereinander (Auto Mitte, Rad daneben, Bus außen; Gleise Mitte, S-Bahn daneben)
- Eine Straße kann gleichzeitig in „Auto“ und „Rad“ erscheinen

## 2. Grün
| Layer | Farbe | Quelle in OSM |
|---|---|---|
| Spielplätze | #bccb72 | leisure=playground |
| Private Grünflächen | #cbd8c2 | private Gärten, Kleingärten |
| Öffentliche Grünflächen | #94b98a | Parks, Gärten, Rasen, Wiesen, Friedhöfe, Wald, Gebüsch |
| Aufenthaltsflächen | #93c2ae | Plätze, Fußgängerzonen-Flächen, Picknickplätze, Sitzbänke |
| Bäume | #557d4f | Einzelbäume, Baumreihen (Punkte vergrößert) |

## 3. Nutzungen (nur Gebäude werden eingefärbt)
| Gruppe | Layer und Farben |
|---|---|
| Gesundheit | Krankenhaus #a9383d · Allgemeinarzt #d9625f · Apotheke #c0517a · Facharzt #ec9d93 · Zahnarzt #f5ccc6 |
| Einkaufen | Wochenmarkt #2f5b85 · Supermarkt #4874a6 · Drogerie #4c9aa6 · Bäckerei #7ea3cf · Sonstige Läden #c4d8ee |
| Freizeit | Bars #a8913f · Kultur #cf9532 · Gastronomie #e9c24f · Sport #f3e2a2 (Kontur #c8a94e) |
| Bildung | Hochschule #5c4795 · Weiterführende Schule #8a6dc0 · Bibliothek #b083b8 · Grundschule #b49fdc · Kita #dcd0ec |
| Wohnen | #f2b37a |

Regeln:
- Punkt im Gebäude → Gebäude wird eingefärbt; Punkt bis 20 m neben einem Gebäude → nächstes Gebäude
- Fläche (z. B. Schulgelände) → alle Gebäude darauf; Flächen ohne Gebäude entfallen – Ausnahme Sport: Sportplätze bleiben als Fläche mit Kontur sichtbar
- Mehrere Nutzungen in einem Haus → Gebäude in allen passenden Layern, sichtbar ist die im Menü weiter oben stehende
- Wohnen: ausdrücklich als Wohnhaus eingetragene Gebäude + Gebäude ohne Nutzung in Wohngebieten (abgestimmt)
- Gebäude ohne bekannte Nutzung bleiben grau (abgestimmt)

## Technik
- Eine einzelne HTML-Datei, per Doppelklick im Browser geöffnet (getestet: Firefox, Windows, eduroam)
- Kartenbibliothek MapLibre GL 4.7.1; Grundkarte OpenFreeMap Positron (ohne API-Schlüssel), Notfall: Esri Light Gray
- Ortssuche Nominatim, Ersatz Photon
- Fachdaten über Overpass (4 Server: overpass-api.de, private.coffee, mail.ru, kumi.systems), 60 s Zeitlimit pro Server, max. 2 Abfragen gleichzeitig, Gebäude nur als Umriss geladen
- Statusanzeige + Ladeprotokoll in der Seitenleiste
- Erkenntnisse: CARTO verlangt bei lokalen Dateien einen API-Schlüssel → nicht nutzbar. Bei Claude veröffentlichte Link-Seiten können keine externen Kartendaten laden und keine PDFs erzeugen → daher HTML-Datei. Später online stellen z. B. über GitHub Pages.

## Offene Punkte
- **Ladezeit zu lang** (ca. 2–3 min, Grün erschien in der vorletzten Version gar nicht). Neueste Version mit Zeitlimit und Ladeprotokoll ist noch nicht getestet → als Nächstes bei 1:2.500 testen und Screenshot des Ladeprotokolls auswerten.
- Vorschlag (noch offen): Knöpfe „Ausschnitt speichern / öffnen“, damit geladene Daten in der Präsentation sofort und offline verfügbar sind.

## Fahrplan
1. ✅ Kartengerüst: Karte, Suche, Maßstab, Daten-Knopf
2. ✅ Layer-Menü + Legende
3. ✅ Daten laden: Grün
4. ✅ Daten laden: Mobilität
5. 🔧 Daten laden: Nutzungen (funktioniert, Ladezeit wird optimiert)
6. Info beim Anklicken
7. PDF-Export im Maßstab
8. Feinschliff, Tablet-Test, Namensgebung

## Arbeitsweise
Schrittweise, nach jedem Schritt kurze Pause zum Nachvollziehen und Feedback.
