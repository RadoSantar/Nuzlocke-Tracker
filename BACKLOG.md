# Nuzlocke Tracker — Backlog

**Stand: v1.9.98.** Diese Datei bei jedem Commit mitpflegen (siehe `CLAUDE.md` →
"Workflow-Pflichtschritte vor jedem Commit"). Erledigte Punkte werden mit Version
**durchgestrichen**, nicht gelöscht — so bleibt der Fortschritt für den Projektleiter-Chat
nachvollziehbar, auch ohne Git-Historie durchsuchen zu müssen. Quellenangaben verweisen auf
`docs/archiv/CLAUDE-historie-bis-v1.9.96.md` (Zeilenangaben dort, Datei wird nicht mehr
verändert) bzw. auf `audit_reports/*.md`.

## 1. Rechercheaudit-Backlog

- [ ] **Alola (Sonne/Mond/USUM), Galar (Schwert/Schild):** komplette Neu-Recherche nötig
  (frühere Detailberichte `gen7.md`/`gen8.md` verloren, nur Kurzfassung im Changelog erhalten),
  inkl. Reihenfolge-Verifikation. Stilvorlage: `audit_reports/gen5.md`/`gen6.md`. Präzedenzfall
  aus dem Kalos-Audit mitnehmen: Vorstands-/Admin-Mitglieder eines Bösewicht-Teams gehören als
  eigene `cls:"Vorstand"`-Bosskarten rein (z.B. Alola: Faba/Plumeria), nicht nur der Teamboss
  selbst.
  Quelle: Archiv Zeile 1420-1423, 1427-1431.
- [ ] **Einall (Schwarz2/Weiß2) — komplettes Postgame:** Rückkehr nach West-Einall (~15
  Standorte: Avenitia/Route 1-3/Gavina/Orion City/Septerna City/Wunderbrücke/P2-Labor/
  Route 17-18/Schwarzes Hochhaus-Weiße Baumhöhle) fehlt komplett.
  Quelle: Archiv Zeile 1424-1426.
- [ ] **Reihenfolge-Verifikation Sinnoh und Einall:** noch nicht begonnen (Methode: Bulbapedia
  "Connecting areas" PRO Einzelseite prüfen, nicht nur Fließtext-Zusammenfassung — siehe erledigte
  Gen-1-3-Runde als Vorlage).
  Quelle: Archiv Zeile 1472-1484; Vorlage `audit_reports/order-gen1-3.md`.
- [ ] **Johto-Namensverwechslung "Anemonia City"/"Oliviana City":** laut PokéWiki ist
  "Anemonia City" die deutsche Bezeichnung für Cianwood City und "Oliviana City" für Olivine
  City — die App bindet Jasmine (Stahlorden) aktuell an "Anemonia City", umgekehrt zum
  PokéWiki-Befund. Erst klären, DANACH Punkt direkt darunter angehen.
  Quelle: Archiv Zeile 1500-1504 (Ursprung `order-gen1-3.md` Abschnitt 4.3).
- [ ] **Boss "chuck" (Kampforden) falsch gebunden:** hängt an "Strudelinseln" statt einer
  Cianwood-Stadt — blockiert durch den Punkt direkt darüber, nicht vorher anfassen.
  Quelle: Archiv Zeile 1494-1499.
- [x] ~~Route 47/Route 48 (Johto) nur in HGSS, tauchen aber auch in GSC_LOCATIONS auf~~ —
  bewusst NICHT korrigiert (Existenz-, kein Reihenfolgefehler), kein weiterer Handlungsbedarf.
  Quelle: Archiv Zeile 1488-1493.
- [x] ~~Kalos (X/Y) Rechercheaudit~~ (erledigt v1.9.39) — `audit_reports/gen6.md`.
  Quelle: Archiv Zeile 1427-1431.
- [x] ~~Reihenfolge-Verifikation Gen 1-3 (Kanto/Johto/Hoenn)~~ (erledigt v1.9.50, 15 Standorte
  korrigiert) — `audit_reports/order-gen1-3.md`.
  Quelle: Archiv Zeile 1472-1479.
- [x] ~~Kanto — Safari-Zone fehlte als eigene Kachel~~ (behoben v1.9.73, zusätzlich Kartenpunkt
  v1.9.74 nachkalibriert).
  Quelle: Archiv Zeile 1432-1451.
- [x] ~~Hoenn — Urzeithöhle fehlte komplett~~ (behoben v1.9.65, zusätzlich Kartenpunkt v1.9.67
  nachkalibriert); „Geheiminsel" (ORAS) dabei gegengecheckt — bestätigt KEIN Fehler.
  Quelle: Archiv Zeile 1452-1471.
- [x] ~~Reihenfolge-Verifikation Kalos~~ (erledigt, siehe `audit_reports/gen6.md`).
  Quelle: Archiv Zeile 1472-1473.

## 2. UX-/QoL-Backlog

- [ ] **Onboarding-Tour kuratieren**, sobald v2.0/"das große Ganze" steht — bewusst
  zurückgestellt, bis der Funktionsumfang final ist (sonst müsste die Kuration bei jeder neuen
  Funktion wiederholt werden).
  Quelle: Archiv Zeile 1566-1580.
- [ ] **Barrierefreiheit:** nur 11 `aria-label`-Attribute im ganzen Code, deutlich mehr
  icon-only-Buttons ohne Beschriftung. Zusätzlich denkbar: eigene, von der System-Textgröße
  unabhängige Schriftgrößen-Einstellung.
  Quelle: Archiv Zeile 1582-1586.
- [ ] **Gefühlte Performance:** Shimmer/Pulse-Skeleton statt reinem "?"-Platzhalter beim ersten
  Sprite-Laden; ggf. Ergebnis-Begrenzung/"mehr laden" bei sehr langen Editionen (kein konkreter
  Ruckel-Fall bekannt, nur vorsorglich notiert).
  Quelle: Archiv Zeile 1587-1591.
- [ ] **Auffindbarkeit neuer Funktionen:** "Neu"-Badge auf Einstellungs-Kapiteln mit Update seit
  letztem Öffnen (aus dem Changelog ableitbar) — löst dasselbe Grundproblem wie der
  Soul-Link-Discoverability-Fund.
  Quelle: Archiv Zeile 1592-1595.
- [ ] **Datensicherheit:** automatisches, rollierendes LOKALES Backup (z.B. letzte 3
  Speicherstände in eigenem `localStorage`-Fach), unabhängig von Cloud-Sync, als zusätzliches
  Sicherheitsnetz.
  Quelle: Archiv Zeile 1596-1600.
- [ ] **Auswertung/Motivation:** teilbare Bild-Karte des Run-Rückblicks (Editions-Logo, Orden,
  Team, Todesursachen) zum Teilen/Sichern — Recap-Text existiert schon, nur nicht als Bild.
  Quelle: Archiv Zeile 1601-1606 (siehe auch Abschnitt 4 unten, Nemesis-Idee).
- [x] ~~`pwa/manifest.json`-Beschreibung veraltet~~ (erledigt bei einem Cleanup-Durchgang, kein
  `APP_VERSION`-Bezug da `manifest.json` nicht Teil der App-Datei ist) — auf "23 Editionen
  (Gen 1-9)" aktualisiert.
  Quelle: Archiv Zeile 1607-1614.

## 3. Karten-Kalibrierungsstand je Region

| Region(en) | Punkte | Routen/Flächen | Status |
|---|---|---|---|
| Kanto (Rot/Blau/Gelb/FeuerRot/BlattGrün) | ✅ kalibriert | ✅ kalibriert | **fertig** — zuletzt komplette Neukalibrierung aller 50 Standorte v1.9.88 |
| Hoenn (Rubin/Saphir/Smaragd/ORAS/Omega Rubin/Alpha Saphir) | ✅ kalibriert (v1.9.63) | ⬜ offen | Routen bewusst noch nicht auf Flächen-Format umgestellt |
| Johto (Gold/Silber/Kristall/HGSS) | ⬜ offen | ⬜ offen | reines 8×8-Platzhalter-Raster, noch nie kalibriert |
| Sinnoh (Diamant/Perl/Platin/BDSP) | ⬜ offen | ⬜ offen | reines 9×10-Platzhalter-Raster, noch nie kalibriert |
| Kalos (X/Y) | ⬜ offen | ⬜ offen | reines 8×7-Platzhalter-Raster, noch nie kalibriert |
| Einall, Alola, Galar, Karmesin/Purpur | — | — | keine Regionskarte implementiert (Feature nicht ausgeweitet) |

Quelle: Archiv Zeile 390-457 (Kanto), 434-471 (Hoenn), 681 (Hoenn-Routen offen), 681-828
(Johto/Sinnoh/Kalos-Rollouts mit Platzhaster-Rastern).

**Offene Aufgaben daraus:**
- [ ] Hoenn-Routen auf Flächen-Format (`{quad:[...]}`) umkalibrieren.
- [ ] Johto komplett kalibrieren (Punkte + ggf. Flächen).
- [ ] Sinnoh komplett kalibrieren (Punkte + ggf. Flächen).
- [ ] Kalos komplett kalibrieren (Punkte + ggf. Flächen).
- [ ] Einall/Alola/Galar/Karmesin-Purpur: Regionskarten-Feature ggf. ausweiten (bisher nicht
  angefragt, kein fester Plan).

## 4. Todesursache-Ideen (aus v1.9.82, technisch vorbereitet durch `deathBossId`)

- [ ] **Nemesis-Pokémon-Statistik:** welche Gegner-Spezies hat insgesamt die meisten eigenen
  Team-Mitglieder getötet — Auszählung von `deathCause`, mit `deathBossId` zusätzlich nach
  Bosskampf aufschlüsselbar.
- [ ] **"Gefährlichster Trainer"-Detailaufschlüsselung:** bestehender "Härtester Gegner"-Insight
  in `runRecapInsights()` um eine Aufschlüsselung erweitern ("hat X mit {Spezies A}, Y mit
  {Spezies B} besiegt") — jetzt dank `deathBossId` möglich.
- [ ] **Achievement "Erzfeind":** für besonders viele Team-Verluste gegen dieselbe Gegner-Spezies
  oder denselben Bosskampf — neuer `ACHIEVEMENTS`-Eintrag, Check-Funktion analog zu bestehenden
  `bossLossIds`-basierten Erfolgen.
- [ ] **Ausführlichere Recap-Erzählung:** Insight wie "Dein größter Feind war {Species}, hat {N}
  deiner Pokémon besiegt" ergänzen, analog zum "Härtester Gegner"-Insight, aber
  pokémon- statt bosszentriert.

Quelle: Archiv Zeile 970-988.
