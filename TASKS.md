# Nuzlocke Tracker — Tasks

Übergabe-Datei zwischen Projektleiter-Chat (plant, formuliert Tasks) und Programmierer-Chat
(diese Claude-Code-Sitzung, setzt sie um).

**Wichtig — Schreibzugriff:** Der Projektleiter-Chat hat nur lesenden Web-Zugriff aufs Repo,
kein Schreibrecht. Er kann Tasks also NICHT selbst hier eintragen. Ablauf:
1. Projektleiter formuliert einen Task (kurzer Titel + 2-4 Sätze Kontext, siehe Format unten).
2. Nutzer trägt ihn hier ein — entweder per Nachricht an den Programmierer-Chat ("trag diesen
   Task ein: ...") oder direkt über die GitHub-Weboberfläche.
3. Programmierer prüft `TASKS.md` zu Beginn der Arbeit (oder wenn der Nutzer explizit darauf
   verweist), arbeitet offene Einträge ab.
4. Nach Abschluss: Eintrag zu "Erledigte Tasks" verschieben, mit Version markieren — NICHT
   löschen (gleiches Prinzip wie `BACKLOG.md`: der Projektleiter soll den Fortschritt
   nachvollziehen können, auch ohne Git-Historie zu durchsuchen).

**Format pro Task:**
```
- [ ] <Kurztitel> — <Kontext: was soll sich ändern, warum, Bezug zu CLAUDE.md/BACKLOG.md-Stelle
  falls vorhanden> (vorgeschlagen: Projektleiter, YYYY-MM-DD)
```

## Offene Tasks

_(noch keine eingetragen)_

## Erledigte Tasks

_(noch keine abgeschlossen)_
