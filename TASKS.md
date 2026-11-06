# Nuzlocke Tracker — Tasks

Übergabe-Datei zwischen Projektleiter-Chat (plant, formuliert Tasks) und Programmierer-Chat
(diese Claude-Code-Sitzung, setzt sie um).

**Schreibzugriff (seit 2026-11-06):** Der Projektleiter-Chat hat per fine-grained GitHub-Token
(nur dieses Repo, nur *Contents*) Schreibrecht und trägt Tasks selbst hier ein. Regeln:
1. Der Projektleiter schreibt AUSSCHLIESSLICH in `TASKS.md` — Code, Daten, `CLAUDE.md`,
   `BACKLOG.md`, `audit_reports/` usw. bleiben Sache des Programmierer-Chats.
2. Projektleiter-Commits sind klein und mit `TASKS:` präfixiert (z. B. "TASKS: T3 eingetragen").
3. Programmierer macht zu Beginn jeder Arbeit `git pull`, damit er neue Einträge sieht und keine
   Push-Konflikte entstehen, und prüft dann `TASKS.md` auf offene Einträge.
4. Nach Abschluss: Eintrag zu "Erledigte Tasks" verschieben, abhaken und mit Version markieren —
   NICHT löschen (gleiches Prinzip wie `BACKLOG.md`: der Projektleiter soll den Fortschritt
   nachvollziehen können, auch ohne Git-Historie zu durchsuchen).
5. Status-Zwischenstände ("in Arbeit", Rückfragen) darf der Programmierer direkt am Eintrag ergänzen.

**Format pro Task:**
```
- [ ] <Kurztitel> — <Kontext: was soll sich ändern, warum, Bezug zu CLAUDE.md/BACKLOG.md-Stelle
  falls vorhanden> (vorgeschlagen: Projektleiter, YYYY-MM-DD)
```

## Offene Tasks

- [ ] **T4 — Drei Lücken in `BACKLOG.md` nachtragen** — Beim Abgleich CLAUDE.md ↔ BACKLOG.md
  fielen drei fehlende Punkte auf: (1) Das Schwert/Schild-DLC (Isle of Armor, Crown Tundra) ist laut
  CLAUDE.md "Projektzweck" ausdrückliches v2.0-Kriterium, steht aber nicht als eigener Punkt in
  BACKLOG.md Abschnitt 1. (2) Die beim Sinnoh-Karten-Rollout (v1.9.94, Archiv) vorgemerkte Prüfung,
  ob die Exklusivstandorte Zerrwelt/Eisenruinen (Platin) und Untergrundhöhlen/Hamanasu-Park (BDSP)
  korrekt zugeordnet sind, fehlt. (3) Für Karmesin/Purpur (Gen 9) gibt es weder Audit-Bericht noch
  Backlog-Punkt; auch dessen DLCs zählen zum v2.0-Kriterium "alle Editionen vollständig" — bitte
  als offenen Punkt (Status unbekannt, Audit nötig) aufnehmen und in `audit_reports/INDEX.md` unter
  "Fehlende Berichte" ergänzen. (vorgeschlagen: Projektleiter, 2026-11-06)
- [ ] **T5 — Subagent-Rollen in CLAUDE.md verankern + `IDEEN.md` anlegen** — Mit dem Nutzer
  abgestimmte Rollenaufteilung als kurzer Abschnitt "Subagent-Rollen" in CLAUDE.md aufnehmen
  (Schlankheitsregel beachten). Grundregel: nur die Hauptsitzung committet (Ausnahme: ein
  Audit-Bericht wird sofort nach Rückgabe committet). Rollen:
  **Orchestrator** (Hauptsitzung: liest TASKS.md, setzt Code/Daten selbst um, delegiert, committet);
  **Rechercheur** (Audits nach Muster `gen5.md`/`gen6.md`, Existenz- und Reihenfolge-Prüfung getrennt,
  Asset-URLs per `curl` prüfen, ändert keinen App-Code);
  **Übersetzer** (prüft, ob englische Begriffe korrekt mit dem OFFIZIELLEN deutschen Namen übersetzt
  sind statt 1:1 — z. B. "Rock Climb" = Kraxler; gilt für Pokémon, Attacken/VMs, Items, Orte,
  Trainer, Orden und UI-Texte; Quelle PokéWiki/offizielle deutsche Spieltexte; prüft auch jeden
  neuen Audit-Bericht vor der Umsetzung; meldet Funde, ändert selbst nichts);
  **Verifizierer** (`validate-editions.js`, `node --check`, Playwright auf tatsächlichen
  Zielzustand, Shapely-Überlappungscheck bei Kalibrierungsdaten; meldet nur, repariert nichts);
  **UI-Polish** (CSS/Hell-Dunkel/Editionsfarben/Antipp-Größen, keine Logik/Daten, Ergebnis immer
  zum Verifizierer); **Aufräumer** (toter Code/verwaiste Handler/Dopplungen ohne
  Verhaltensänderung, Ergebnis immer zum Verifizierer); **Release & Doku** (Versionsbump, Changelog,
  CLAUDE.md inkl. 40k-Grenze, BACKLOG.md, TASKS.md, Artifact- und Netlify-Build, kein Code);
  **Innovator** (bringt neue Ideen ein — Features, QoL, bessere Technologien, neue Werkzeuge,
  Sonstiges — und schreibt sie AUSSCHLIESSLICH in eine neue Datei `IDEEN.md` (Titel, Nutzen,
  grober Aufwand, Risiken, Bezug zu BACKLOG.md falls vorhanden); setzt nie selbst um. Der
  Projektleiter liest `IDEEN.md`, legt die Ideen dem Nutzer vor und erstellt NUR mit dessen
  Genehmigung Tasks daraus). `IDEEN.md` in die Dateiübersicht von CLAUDE.md aufnehmen.
  (vorgeschlagen: Projektleiter, 2026-11-06)
- [ ] **T6 — Galar-Rechercheaudit inkl. DLC (Rechercheur + Übersetzer), nach T5** — Erster Schritt
  Richtung v2.0: Für Schwert/Schild existiert kein Bericht mehr (`gen8.md` verloren, siehe
  `audit_reports/INDEX.md`), und das DLC ist ausdrückliches v2.0-Kriterium. Der Rechercheur
  erstellt `audit_reports/gen8.md` nach Muster `gen6.md`: Hauptspiel plus Isle of Armor und Crown
  Tundra, Existenz- UND Reihenfolge-Prüfung der Standorte, Bosse/Level/Ass, Präzedenzfall
  Vorstands-Bosskarten (`cls:"Vorstand"`) beachten. Der Übersetzer prüft alle deutschen Namen im
  Bericht. Bericht sofort committen und dem Nutzer zum Gegenchecken vorlegen — noch KEINE Änderung
  am App-Code. (vorgeschlagen: Projektleiter, 2026-11-06)

## Erledigte Tasks

- [x] **T3 — `audit_reports/INDEX.md` angelegt und Status-Köpfe korrigiert** (erledigt,
  2026-11-06, kein App-Code/-Daten betroffen → kein `APP_VERSION`-Bump). `audit_reports/INDEX.md`
  neu angelegt: listet alle 7 Berichte mit Generation, Thema, Status (per Changelog-Cross-Check
  gegen `nuzlocke-v2-editionen.html` verifiziert, nicht nur README). Dabei drei fälschlich auf
  "noch nicht umgesetzt" stehende Status-Köpfe korrigiert (`gen5.md`→v1.9.38, `gen6.md`→
  v1.9.39/40, `order-gen1-3.md`→v1.9.50 — alle drei waren längst umgesetzt). `BACKLOG.md`
  Abschnitt 1 verweist jetzt auf die neue `INDEX.md` und nennt explizit, dass Alola/Galar
  (Gen 7/8) als einzige Generationen noch gar keinen Bericht in `audit_reports/` haben.
  (vorgeschlagen: Projektleiter, 2026-11-06)
