# Konzeptblatt – LOCUS. Standortanalyse

Stand: 18.11.2026, 15:00 – Schritte 1–7 fertig und getestet; Swiss Style, Startseite mit Globus-Zoom, Standort-Figur, Demo-Version
**Aktuelle Dateien im Projekt:**
- `claude/LOCUS_stand_2026-11-18.html` – die App
- `claude/LOCUS_demo.html` – Demo mit Anleitung (Vorführmodus)
(ältere Dateien `standortanalyse_zwischenstand_2026-11-16/17.html` sind überholt)

## Branch `schneller-laden`: schneller laden (18.11.2026)
**Nur in diesem Branch.** Auf `main` liegt unverändert der alte Stand – ohne alle Punkte dieses Abschnitts.
- **Reihenfolge beim Laden:** Speicher im Browser → Niedersachsen-Cache → Overpass live (Wettlauf, Neuversuche) → Notfall-Datei (nur Demo-Ort)
- **Speicher im Browser** (IndexedDB, sonst localStorage): geladene Ausschnitte 14 Tage, höchstens 10; derselbe oder ein kleinerer Ausschnitt ist sofort da (ca. 0,5 s, ohne Server). „Neu vom Server laden“ holt frische Daten.
- **Niedersachsen-Cache** (https://jade-hs-vibecoding-wpk.github.io/niedersachsen-cache/): Für Hannover, Braunschweig, Oldenburg, Osnabrück, Wolfsburg, Göttingen, Salzgitter, Hildesheim, Wilhelmshaven und Delmenhorst (jeweils mit ca. 3 km Rand) und seit 19.11. auch rund um Oldenburg für alle Gemeinden über 5.000 Einwohner (rund 135 Gemeinden bis ca. 90 km, z. B. Rastede, Bad Zwischenahn, Elsfleth, Brake, Varel, Cloppenburg, Leer, Emden; genaue Liste in `STAND.md` des Caches) kommen die Daten fertig vorbereitet von GitHub Pages – ca. 1–3 s statt 20–60 s. Datenstand bis gut eine Woche alt (wöchentlich neu); der Status zeigt „Daten aus dem Niedersachsen-Cache (OpenStreetMap, Stand …)“, „Neu vom Server laden“ holt den neuesten Stand live. Anderswo (z. B. Berlin, Lüneburg, Gemeinden unter 5.000 Einwohnern), ohne Internetzugang zum Cache oder in älteren Browsern (Safari vor 16.4, Firefox vor 113) wird wie bisher live geladen.
- **Neuversuche mit wachsender Pause** (3, 6, 12, 24, 30 … s, bis 180 s gesamt), Ersatzserver je 40 s – statt nach 5 schnellen Abweisungen aufzugeben
- **Alle drei Gruppen auf einmal** (`ALLE_GRUPPEN_MITLADEN = true`): Beim Laden kommen immer Mobilität, Grün und Nutzungen in einer Abfrage, angezeigt wird, was eingeschaltet ist; später eingeschaltete Gruppen sind sofort da. **Damit stimmt „geladen wird nur, was eingeschaltet ist“ nicht mehr.** Altes Verhalten: in der HTML-Datei die Zeile `const ALLE_GRUPPEN_MITLADEN = true;` auf `false` ändern (in App und Demo).
- **Notfall-Datei für den Demo-Ort** `LOCUS_demo_daten.js` (Kollwitzplatz, alle Gruppen, Stand 18.11.2026): springt ein, wenn die Server nach 30 s nicht geantwortet haben. Sie muss **neben der HTML-Datei liegen** (gleicher Ordner – beim Doppelklick wie auf GitHub Pages); fehlt sie, wird einfach normal geladen.
- Aufgeräumt: ungenutzte Warteschlange und Serverbewertung entfernt; gespeicherte Daten verkleinert (leere Linienteile außerhalb des Ausschnitts)

## Nächstes Mal weitermachen – hier ansetzen
1. Dateien herunterladen und im Browser öffnen (Safari/Firefox).
2. **Demo testen** (mit echten Daten noch nicht ausprobiert): alle 12 Schritte selbst machen und einmal nur mit „Zeig’s mir“.
3. Offen aus Schritt 8:
   - **Tablet-Test** (iPad: Seitenleiste, Layer, Figur mit dem Finger ziehen, PDF, Demo)
   - **Fußzeile der Startseite:** Platzhalter „Studienprojekt Architektur · 2026“ ersetzen (Namen, Hochschule, Semester)
   - Einleitungssatz der Startseite ggf. anpassen
   - Offene Frage: Soll die Standort-Figur auch im PDF erscheinen (als Standortmarkierung)?
4. Optional, noch nicht entschieden: „Ausschnitt speichern/öffnen“, Online stellen über GitHub Pages, Daten vorbereiten über GitHub Actions.

## Demo-Version (`LOCUS_demo.html`)
- Eigene Datei, startet direkt mit der Anleitung; sonst identisch mit der App (Startseite zeigt „Standortanalyse · Demo“)
- Zuschauer machen jeden Schritt selbst; die Stelle ist rot markiert (pulsierender Rahmen); „Zeig’s mir“ erledigt den Schritt automatisch; erledigte Schritte gehen nach ca. 1 s von allein weiter; „Überspringen“ jederzeit, „×“ beendet die Demo
- Daten werden **live** geladen (ca. 20–30 s, Server können überlastet sein)
- Beispielort für „Zeig’s mir“: Berlin, Prenzlauer Berg (Kollwitzplatz)
- 12 Schritte: 01 Willkommen / „Los geht’s“ · 02 Figur auf die Karte ziehen · 03 Maßstab 1:2.500 · 04 Layer Mobilität + Grün einschalten · 05 Daten laden · 06 Nutzungen dazunehmen (lädt automatisch nach) · 07 Etwas anklicken (Info-Fenster) · 08 Legende · 09 PDF vorbereiten (A4 quer, 1:2.500, Rahmen) · 10 PDF erstellen · 11 Figur zurück ins Haus · 12 Fertig (Nochmal / Demo beenden)
- Wird per Skript aus der App erzeugt (Hauptdatei + Anleitungsteil); nach Änderungen an der App die Demo neu erzeugen, damit beide gleich bleiben

## Name & Gestaltung
- Name: **LOCUS.** (roter Punkt)
- Swiss Style: Helvetica, Schwarz/Weiß, dünne Linien, Rot #e2001a nur als Akzent, keine runden Ecken, nummerierte Abschnitte (rote Nummern)
- **Startseite:** 12-Spalten-Raster, großes „LOCUS.“, Einleitungssatz, drei Spalten 01 Mobilität / 02 Grün / 03 Nutzungen, Knopf „Los geht’s →“; rechts ein **sich drehender Globus mit Deutschland in Rot**.
- **Übergang Startseite → Karte (4 s):** Texte blenden aus, Globus dreht Deutschland nach vorne, zoomt bildfüllend heran, bis Deutschland so groß ist wie auf der Karte dahinter (Rot wird heller, rote Kontur bleibt), dann Überblenden in die Karte.
- **Zurück (Klick auf das Logo, 2 s):** Globus erscheint groß über der Karte und zoomt wieder heraus, Texte blenden ein.
- Ohne Globus (kein Internet) oder bei „Bewegung reduzieren“ im System: einfaches Überblenden.
- Seitenleiste: 01 Ort · 02 Maßstab · 03 Layer · 04 Daten · 05 Grundkarte · 06 PDF-Export · 07 Status
- Oben auf der Karte: „☰“ (Seitenleiste), „Legende“ (ein/aus, wird im Browser gemerkt) und das **Haus mit der Standort-Figur**

## Standort-Figur
- Rote Maßstabsfigur, wohnt in einem kleinen Haus (Giebeldach), das genau so hoch ist wie die Knöpfe
- Aus dem Haus auf die Karte ziehen → Figur bleibt dort stehen, Karte fliegt auf **1 : 5.000** heran (Daten direkt ladbar)
- Auf der Karte weiterziehen → Karte zoomt auf den neuen Punkt; einfacher Klick bewirkt nichts
- Entfernen: zurück ins Haus ziehen (Haus wird rot umrandet, sobald die Figur darüber schwebt) oder Doppelklick
- Außerhalb der geladenen Daten abgesetzt → alte Daten werden verworfen (wie bei der Ortssuche)
- Funktioniert mit Maus, Stift und Finger (Tablet)
- Erscheint bisher nicht im PDF

## Grundprinzip
- Funktioniert für alle Orte in Deutschland, Daten live aus OpenStreetMap über Overpass (Internet nötig); Branch `schneller-laden`: große Städte Niedersachsens aus dem Niedersachsen-Cache
- **Ladezeit ca. 20–25 s für alle drei Gruppen** bei 1:2.500 (vorher 1–2 min)
- Erst Layer einschalten, dann „Daten für diesen Ausschnitt laden“ – geladen wird nur, was eingeschaltet ist; später eingeschaltete Gruppen werden automatisch nachgeladen (**Branch `schneller-laden`:** es werden immer alle drei Gruppen geladen, siehe `ALLE_GRUPPEN_MITLADEN` oben)
- Neuer Ort/Ausschnitt → alte Daten werden verworfen; bei Fehlern „Fehlende Daten nachladen“
- Info-Fenster beim Anklicken: Kategorie, Name, Art, Adresse, Öffnungszeiten, Linien an Haltestellen, Link zu OSM; „vermutete“ Wohnhäuser sind gekennzeichnet

## Maßstab & PDF-Export
- Bildschirm: feste Stufen 1:500 / 1:1.000 / 1:2.000 / 1:2.500 / 1:5.000 (nur ungefähr, 96 dpi)
- PDF: A4–A1, hoch/quer, 1:500–1:5.000, Titel frei; roter Rahmen auf der Karte zeigt den Blattausschnitt
- Karte im exakten Maßstab (A4/A3 200 dpi, A2 150, A1 120); mit echten Daten getestet (A3 quer) ✓
- **Blatt im Swiss Style:** quer = Spalte rechts, hoch = Leiste unten
  - Kopf: „LOCUS.“ klein mit rotem Punkt, Titel groß, kräftige Linie
  - Legende klein, passt sich an, Gruppenüberschriften grau in Versalien, nie allein am Spaltenende
  - Plankopf: architektonisches Nordzeichen (Kreis mit Fadenkreuz, Balken nach Norden, „N“ nicht fett), schlichte Maßstabsleiste, „M 1 : x“ nicht fett auf Höhe des N; darunter FORMAT / STAND / QUELLE
- Dateiname: `LOCUS_<Titel>_<Format>_1-<Maßstab>.pdf`

## Layer (Version OHNE „Punkt 1“, bewusst so gewählt)
**Mobilität:** Buslinien #e3c46b (mit vollständigen Linieninfos) · Bushaltestellen #c9a43a · Fern-/Regionalbahn #9e3128 · S-Bahn #c4473a · U-Bahn #d26a55 · Straßenbahn #de9378 · Bahnhöfe/Haltestellen #7f2820 · Hauptverkehrsstraßen #6a8caf · Parkplätze #a9bfd6 · Radwege #cf7fb0 · Fußwege #efc6df
- Linien liegen nebeneinander wie in einem Netzplan

**Grün:** Spielplätze #bccb72 · Private Grünflächen #cbd8c2 · Öffentliche Grünflächen #94b98a · Aufenthaltsflächen #93c2ae (inkl. Bänke) · Bäume #557d4f

**Nutzungen (nur Gebäude werden eingefärbt):**
- Gesundheit: Krankenhäuser #a9383d · Zahnärzte #f5ccc6 · Fachärzte #ec9d93 · Allgemeinärzte #d9625f · Apotheken #c0517a
- Einkaufen: Supermärkte #4874a6 · Bäckereien #7ea3cf · Drogerien #4c9aa6 · Wochenmärkte #2f5b85 · Sonstige Läden #c4d8ee
- Freizeit: Gastronomie #e9c24f · Kultur #cf9532 · Sport #f3e2a2 (Sportplätze als Fläche mit Kontur #c8a94e) · Bars & Nachtleben #a8913f
- Bildung: Kitas #dcd0ec · Grundschulen #b49fdc · Weiterführende Schulen #8a6dc0 · Hochschulen #5c4795 · Bibliotheken #b083b8
- Wohnen #f2b37a: ausdrücklich als Wohnhaus eingetragen + Gebäude ohne Nutzung im Wohngebiet
- Regeln: Punkt im Gebäude → Gebäude; Punkt bis 20 m daneben → nächstes Gebäude; Fläche → alle Gebäude darauf; Gebäude ohne bekannte Nutzung bleiben grau

## Technik
- Eine HTML-Datei, per Doppelklick im Browser (getestet: Firefox/Windows, Safari/Mac)
- MapLibre GL 4.7.1; Grundkarte OpenFreeMap Positron (Notfall Esri Light Gray); Suche Nominatim, Ersatz Photon; jsPDF 2.5.1; d3 v7 + world-atlas für den Globus
- **Laden** (Stand `main`; Branch `schneller-laden` siehe oben): eine Abfrage für alle eingeschalteten Gruppen; „Wettlauf“ overpass-api.de gegen maps.mail.ru, erste Antwort gewinnt; abgewiesener Server nach 3 s (bei 429 nach 10 s) erneut, max. 5 Versuche; Zeitlimit 120 s pro Versuch, 180 s gesamt; danach private.coffee und kumi.systems je einmal
- Gebäudeumrisse ohne Merkmale („skel“) → weniger Daten
- Statusanzeige + Ladeprotokoll in der Seitenleiste

## Erkenntnisse aus den Ladetests (18.11.)
- Engpass sind Warteschlangen und Abweisungen der Server – nicht Datenmenge oder JavaScript
- Wirksamste Maßnahme: zwei Server im Wettlauf + schnelle Neuversuche (→ ca. 22 s)
- Aufteilen in Kacheln macht es langsamer
- Schlanke Buslinien sparen 96 % Daten, aber keine Zeit → volle Linieninfos bleiben

## Entscheidungen (Verlauf)
- CARTO-Karten brauchen bei lokalen Dateien einen API-Schlüssel → nicht nutzbar
- Bei Claude veröffentlichte Seiten können keine externen Kartendaten laden → HTML-Datei
- Schnelle Variante „Nutzungen aus der Grundkarte“ und Mischform verworfen → Overpass-Version bleibt
- „Punkt 1“ verworfen → Version ohne Punkt 1
- PMTiles, ohsome, Google Places, städtische Open Data verworfen
- Globus-Übergang: Variante „Globus zoomt, Karte blendet ein“ statt MapLibre-5-Globus (geringeres Risiko)
- Standort-Figur: eigene rote Maßstabsfigur (kein Nachbau des Street-View-Männchens), Zoom auf 1:5.000
- Demo: eigene Datei, „selbst machen mit Hilfe“, Daten live

## Fahrplan
1. ✅ Kartengerüst: Karte, Suche, Maßstab
2. ✅ Layer-Menü + Legende
3. ✅ Grün
4. ✅ Mobilität
5. ✅ Nutzungen
6. ✅ Info beim Anklicken
7. ✅ PDF-Export im Maßstab (getestet)
8. 🔧 Feinschliff: ✅ Ladeumbau · ✅ Legenden-Knopf · ✅ Name LOCUS · ✅ Swiss Style · ✅ Startseite mit Globus · ✅ PDF-Layout/Nordzeichen · ✅ Globus-Zoom-Übergang · ✅ Standort-Figur · ✅ Demo-Version (Test mit echten Daten offen) · offen: Tablet-Test, Fußzeile/Einleitungstext
9. (optional) Online stellen über GitHub Pages / Daten über GitHub Actions

## Arbeitsweise
Schrittweise, erst fragen, erst planen und testen, dann einbauen; nach jedem Schritt Pause für Feedback.
