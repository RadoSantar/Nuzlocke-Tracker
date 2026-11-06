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

_(aktuell keine offen)_

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
