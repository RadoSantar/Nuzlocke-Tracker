# Nuzlocke Tracker — Tasks

Übergabe-Datei zwischen Projektleiter-Chat (plant, formuliert Tasks) und Programmierer-Chat
(diese Claude-Code-Sitzung, setzt sie um).

**Schreibzugriff (seit 2026-11-06):** Der Projektleiter-Chat hat per fine-grained GitHub-Token
(nur dieses Repo, nur *Contents*) Schreibrecht und trägt Tasks selbst hier ein. Regeln:
1. Der Projektleiter schreibt standardmäßig nur in `TASKS.md`. Doku-Dateien (`CLAUDE.md`,
   `BACKLOG.md`, `IDEEN.md`, `audit_reports/INDEX.md`) nur, wenn der Nutzer ihm einen Task
   ausdrücklich direkt zuweist. App-Code, Daten und `tools/` bleiben immer beim Programmierer-Chat.
2. Projektleiter-Commits sind klein und mit `TASKS:` (bzw. `DOKU:`) präfixiert (z. B. "TASKS: T3 eingetragen").
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

- [ ] **T6 — Galar-Rechercheaudit inkl. DLC (Rechercheur + Übersetzer), nach T5** — Erster Schritt
  Richtung v2.0: Für Schwert/Schild existiert kein Bericht mehr (`gen8.md` verloren, siehe
  `audit_reports/INDEX.md`), und das DLC ist ausdrückliches v2.0-Kriterium. Der Rechercheur
  erstellt `audit_reports/gen8.md` nach Muster `gen6.md`: Hauptspiel plus Isle of Armor und Crown
  Tundra, Existenz- UND Reihenfolge-Prüfung der Standorte, Bosse/Level/Ass, Präzedenzfall
  Vorstands-Bosskarten (`cls:"Vorstand"`) beachten. Der Übersetzer prüft alle deutschen Namen im
  Bericht. Bericht sofort committen und dem Nutzer zum Gegenchecken vorlegen — noch KEINE Änderung
  am App-Code. (vorgeschlagen: Projektleiter, 2026-11-06)

## Erledigte Tasks

- [x] **T4 — Drei Lücken in `BACKLOG.md` nachgetragen** (erledigt vom Projektleiter auf direkte
  Zuweisung des Nutzers, 2026-11-06, reine Doku → kein `APP_VERSION`-Bump). BACKLOG.md Abschnitt 1
  um Schwert/Schild-DLC, Sinnoh-Exklusivstandorte und Karmesin/Purpur (Gen 9) inkl. DLC ergänzt;
  `audit_reports/INDEX.md` "Fehlende Berichte" um Gen 9 ergänzt.
- [x] **T5 — Subagent-Rollen in CLAUDE.md verankert + `IDEEN.md` angelegt** (erledigt vom
  Projektleiter auf direkte Zuweisung des Nutzers, 2026-11-06, reine Doku → kein
  `APP_VERSION`-Bump). Neuer Abschnitt "Subagent-Rollen" (8 Rollen), `IDEEN.md` mit Ablauf/Format,
  Dateiübersicht ergänzt. Schreibregel des Projektleiters in CLAUDE.md und hier angepasst: Doku-
  Dateien nur bei ausdrücklicher Nutzer-Zuweisung, App-Code/Daten/`tools/` nie.
- [x] **T3 — `audit_reports/INDEX.md` angelegt und Status-Köpfe korrigiert** (erledigt,
  2026-11-06, kein App-Code/-Daten betroffen → kein `APP_VERSION`-Bump). `audit_reports/INDEX.md`
  neu angelegt: listet alle 7 Berichte mit Generation, Thema, Status (per Changelog-Cross-Check
  gegen `nuzlocke-v2-editionen.html` verifiziert, nicht nur README). Dabei drei fälschlich auf
  "noch nicht umgesetzt" stehende Status-Köpfe korrigiert (`gen5.md`→v1.9.38, `gen6.md`→
  v1.9.39/40, `order-gen1-3.md`→v1.9.50 — alle drei waren längst umgesetzt). `BACKLOG.md`
  Abschnitt 1 verweist jetzt auf die neue `INDEX.md` und nennt explizit, dass Alola/Galar
  (Gen 7/8) als einzige Generationen noch gar keinen Bericht in `audit_reports/` haben.
  (vorgeschlagen: Projektleiter, 2026-11-06)
