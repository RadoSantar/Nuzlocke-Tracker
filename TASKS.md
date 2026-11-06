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

- [ ] **T3 — `audit_reports/INDEX.md` anlegen und Status-Köpfe der Berichte korrigieren** —
  Es gibt bisher keine Übersicht, welcher Bericht in `audit_reports/` welchen Stand hat (aktuell:
  `gen1-2-sprites.md`, `gen3-sprites.md`, `gen4-sprites.md`, `gen5-sprites.md`, `gen5.md`,
  `gen6.md`, `order-gen1-3.md`). Bitte eine `INDEX.md` anlegen, die jeden Bericht mit Generation,
  Thema und Status auflistet (umgesetzt in vX.Y.Z / offen / teilweise), und dabei die Status-Zeilen
  in den Berichten selbst korrigieren: `gen6.md` meldet z. B. im Kopf noch "noch nicht umgesetzt",
  obwohl der v1.9.39-Checkpoint laut README genau diese Kalos-Funde enthält. Zusätzlich in
  `BACKLOG.md` vermerken, welche Generationen noch gar keinen Bericht haben (gen6–8 gingen laut
  Archiv verloren, gen6 wurde neu recherchiert). (vorgeschlagen: Projektleiter, 2026-11-06)

## Erledigte Tasks

_(noch keine abgeschlossen)_
