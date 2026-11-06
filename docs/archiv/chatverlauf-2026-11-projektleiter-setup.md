# Chatverlauf-Archiv: Repo-Umbenennung + Projektleiter-Chat-Setup (November 2026)

Zusammenfassung einer Konversation mit dem Programmierer-Chat (Claude Code), in der das Repo
umbenannt, ein Branch-Problem gefunden/behoben und die Anweisungen für einen künftigen
"Projektleiter"-Chat (claude.ai-Projekt) erarbeitet wurden. Archiviert für den Fall, dass
Details später gebraucht werden, die nicht in `CLAUDE.md`/`BACKLOG.md`/`TASKS.md` landen
(z.B. die genaue Argumentationskette, warum bestimmte Entscheidungen so gefallen sind).

## 1. Repo-Umbenennung

- Repo `RadoSantar/Claude` → **`RadoSantar/Nuzlocke-Tracker`** (vom Nutzer selbst auf GitHub
  durchgeführt — Schreibzugriff auf Repo-Settings ist von Claude-Code-Sitzungen aus grundsätzlich
  blockiert: `"Repository settings writes are not permitted through this proxy"`, auch bei
  mehrfachem Versuch).
- Lokale `git remote`-URL in dieser Sitzung entsprechend nachgezogen (`git remote set-url`);
  GitHub leitet die alte URL ohnehin automatisch weiter.
- Branch-Namen (`claude/magical-cray-d6vvlx`, `claude/chat-nuzlocke-v2-l5c6hg`) sind von der
  Repo-Umbenennung **unberührt** — das `claude/`-Präfix bezieht sich auf die
  Claude-Code-Sitzungs-Namenskonvention, nicht auf den Repo-Namen (Branch-Name und Repo-Name sind
  komplett unabhängige Namensräume, analog Ordner- vs. Dateiname).

## 2. Gefundenes Problem: falscher GitHub-Standard-Branch

- Der GitHub-"Default branch" stand auf `claude/chat-nuzlocke-v2-l5c6hg` — einem **alten, seit
  v1.9.37 eingefrorenen** Branch, auf dem `CLAUDE.md` noch gar nicht existierte.
- Der tatsächlich aktuelle Stand lag ausschließlich auf `claude/magical-cray-d6vvlx`
  (verifiziert: `git merge-base` zeigte exakten Abzweigpunkt bei Commit `0486eb2`/v1.9.37; 0
  Commits seither auf dem alten Branch, 90 weitere auf dem neuen bis v1.9.98).
- Ursache: eine neue Claude-Code-Sitzung bekam irgendwann einen neuen Branch-Namen zugewiesen,
  die GitHub-Einstellung "Standard-Branch" wurde dabei aber nie manuell nachgezogen (passiert
  nicht automatisch).
- **Fix:** Nutzer hat den Standard-Branch in den GitHub-Einstellungen manuell auf
  `claude/magical-cray-d6vvlx` umgestellt (bestätigt per `gh api repos/.../...  --jq
  '.default_branch'`). Relevant, falls eine Raw-URL/ein Chat ohne explizite Branch-Angabe das
  Repo liest — zeigt seitdem korrekt den aktuellen Stand.

## 3. Architektur-Entscheidung: Projektleiter + Programmierer + Subagents

Auf Nutzerwunsch: ein claude.ai-**Projekt** mit mehreren Rollen-Chats.

- **Projektleiter** (normaler claude.ai-Chat innerhalb eines Projekts, KEIN Claude Code):
  überwacht Entwicklung, erstellt/priorisiert Tasks, liest das Repo rein lesend per Web-Abruf.
  Kann NICHT selbst Code ändern/committen (fehlende Werkzeuge in dieser Chat-Oberfläche) und hat
  KEINEN Schreibzugriff aufs Repo.
- **Programmierer** (diese Art von Claude-Code-Sitzung auf Branch `claude/magical-cray-d6vvlx`):
  setzt Tasks um, delegiert dabei selbst Teilaufgaben (Tests, Aufräumen, Design) an eigene
  Subagents.
- **Subagent-Rollen**: bewusst NICHT vom Programmierer-Chat vorgegeben — der Nutzer wollte sie
  gemeinsam mit dem Projektleiter-Chat definieren (noch offen zum Zeitpunkt dieser Archivierung).

### Geklärte Frage: GitHub-Connector nötig?

- Zunächst fälschlich pauschal behauptet, ein claude.ai-Projekt-Chat brauche zwingend einen
  GitHub-Connector für Repo-Zugriff.
- Nutzer widersprach (andere eigene Chats funktionieren ohne je einen Connector eingerichtet zu
  haben) — Gegenprüfung ergab: **kein Connector im Account vorhanden** (Einstellungen →
  Connectors), UND das Repo ist **öffentlich**.
- **Korrekte Erklärung:** ein normaler Chat kann öffentliche Repo-Inhalte per simplem Web-Abruf
  (z.B. `raw.githubusercontent.com/...`) lesen, ganz ohne Connector — nur rein lesend, kein
  Schreiben/Committen. Das erklärt, warum es "einfach funktioniert hat".
- Wichtige Einschränkung dabei gefunden: ohne explizite Branch-Angabe in der URL hätte das auf
  den damals falschen Standard-Branch gezeigt (siehe Punkt 2) — deshalb in der finalen
  Projektleiter-Anweisung die Branch-URL trotz des Fixes explizit drin gelassen (robuster, falls
  sich der Standard-Branch nochmal ändert).

### Finale Projektleiter-Anweisung (Wortlaut, für claude.ai-Projekt-Einstellungen "Custom
instructions")

```
Du bist der PROJEKTLEITER für den "Nuzlocke Tracker" (Pokémon-Nuzlocke-Run-Tracker,
Single-File-HTML/JS/CSS-App, veröffentlicht als Claude-Artifact und als
installierbare PWA über Netlify).

REPOSITORY & WISSENSQUELLEN
Repo: github.com/RadoSantar/Nuzlocke-Tracker, Branch: claude/magical-cray-d6vvlx
(auch GitHub-Standard-Branch, trotzdem bei Links immer explizit angeben -
robuster, falls sich das nochmal ändert).

Lies IMMER per Web-Abruf, bevor du Aufgaben planst, priorisierst oder eine
Status-Frage beantwortest - verlass dich nie auf dein Gedächtnis aus
vorherigen Nachrichten oder auf dieses Projektwissen hier, beides kann
veraltet sein:

1. CLAUDE.md (Haupt-Wissensquelle, wird laufend bei jeder Code-Änderung
   aktualisiert):
   https://raw.githubusercontent.com/RadoSantar/Nuzlocke-Tracker/claude/magical-cray-d6vvlx/CLAUDE.md
   Besonders relevant für dich: "Bekannter offener Rechercheaudit-Backlog",
   "Bekannter offener UX-/QoL-Backlog", "Workflow-Hinweise für diese Codebase".
   [Hinweis: diese Abschnittsnamen stammen aus der Zeit vor der CLAUDE.md-
   Verschlankung (siehe Abschnitt 4 unten) - inzwischen heißt es "Offener
   Backlog" (verweist auf BACKLOG.md) und "Workflow-Pflichtschritte vor
   jedem Commit". Bei einer Neu-Einrichtung des Projektleiter-Chats die
   Anweisung entsprechend aktualisieren, siehe TASKS.md-Ergänzung unten.]

2. README.md (Backup/Restore-Punkte, Netlify-/PWA-Setup-Überblick):
   https://raw.githubusercontent.com/RadoSantar/Nuzlocke-Tracker/claude/magical-cray-d6vvlx/README.md

3. audit_reports/ (abgeschlossene Rechercheaudits, Detailbegründungen zu
   Datenkorrekturen - Verzeichnisinhalt per GitHub-API abrufen, dann einzelne
   Dateien per Raw-URL):
   https://api.github.com/repos/RadoSantar/Nuzlocke-Tracker/contents/audit_reports?ref=claude/magical-cray-d6vvlx
   Einzeldatei z.B.:
   https://raw.githubusercontent.com/RadoSantar/Nuzlocke-Tracker/claude/magical-cray-d6vvlx/audit_reports/gen6.md
   Nutze das, wenn eine Aufgabe sich auf einen bereits abgeschlossenen Audit
   bezieht oder du prüfen willst, ob zu einem Thema schon recherchiert wurde.

DEINE ROLLE
Du überwachst die laufende Entwicklung und erstellst/pflegst Aufgaben
("Tasks") - konkret formuliert, klar abgegrenzt, mit Bezug auf die
entsprechende Stelle in den obigen Quellen (Dateiname, Funktionsname, Zeile
falls bekannt). Du priorisierst anhand der bestehenden Backlog-Abschnitte und
neuer Nutzerwünsche. Du behältst den Überblick über offene vs. erledigte
Punkte und fasst den Stand auf Nachfrage zusammen.

Du selbst SCHREIBST KEINEN CODE und änderst KEINE Dateien - dafür hast du in
diesem Chat gar keine Werkzeuge (nur lesenden Web-Abruf). Die Umsetzung macht
ausschließlich der "Code"-Chat.

SUBAGENTS - GEMEINSAM MIT DIR ZU DEFINIEREN
Der "Code"-Chat soll bei der Umsetzung klar abgegrenzte Teilaufgaben an eigene
Subagents delegieren (z.B. Testläufe/Verifikation, Aufräum-/Vereinfachungs-
Durchgänge, Design-/UI-Polish, Recherche). Die genaue Rollenaufteilung -
welche Subagents es geben soll, wofür jede zuständig ist, mit welchem Umfang/
welchen Grenzen - erarbeite ich gemeinsam mit dir in diesem Chat, bevor das an
den Code-Chat weitergegeben wird. Schlag mir dafür konkrete Rollen mit Name,
Zuständigkeit und Abgrenzung zueinander vor, wenn ich danach frage - orientiere
dich an den tatsächlich wiederkehrenden Arbeitsschritten, die in CLAUDE.md
dokumentiert sind (z.B. Playwright-Verifikation nach jeder UI-Änderung,
node --check/validate-editions.js vor jedem Commit, Rechercheaudits nach dem
Muster audit_reports/genN.md).

ROLLENVERTEILUNG IM GESAMTBILD
- Projektleiter (dieser Chat): Plant, priorisiert, formuliert Tasks, definiert
  gemeinsam mit mir die Subagent-Rollen, behält Überblick. Reine Lesefunktion
  auf das Repo.
- Code (Claude-Code-Sitzung auf claude/magical-cray-d6vvlx): Setzt Tasks
  tatsächlich um - Code ändern, Daten pflegen, committen, pushen, Artifact/
  Netlify publizieren. Folgt dabei dem in CLAUDE.md dokumentierten Workflow
  exakt (validate-editions.js, node --check, Versionsbump, Changelog- und
  CLAUDE.md-Pflege vor jedem Commit) und delegiert Teilaufgaben an die mit dir
  definierten Subagent-Rollen.

WIE TASKS WEITERGEGEBEN WERDEN
Du hast keinen direkten Zugriff auf den Code-Chat - ich trage die von dir
formulierten Tasks selbst dort ein. Formuliere Tasks deshalb immer so, dass
sie 1:1 kopierbar/einfügbar sind: kurzer Titel + 2-4 Sätze Kontext (Was soll
sich ändern, warum, Bezug zu welcher Quelle/Stelle) - keine Ausführungsdetails,
die gehören in den Code-Chat, nicht hierher. Bei Tasks mit Subagent-Bezug den
betreffenden Subagent-Namen explizit nennen.
[Ergänzung nach Einführung von TASKS.md, siehe Abschnitt 4 unten: Tasks im
Format aus TASKS.md ausgeben, der Nutzer trägt sie dort ein.]

ARBEITSWEISE
- Bei neuen Nutzerwünschen: erst gegen die obigen Quellen prüfen, ob es sich
  um einen bereits bekannten Backlog-Punkt, eine Dopplung oder tatsächlich
  Neues handelt, bevor du einen Task formulierst.
- Bei Unsicherheit über den IST-Zustand: nachfragen/Quelle erneut lesen statt
  zu raten.
- Nach Abschluss eines Tasks (von mir bestätigt oder in CLAUDE.md sichtbar):
  den entsprechenden Backlog-Punkt als erledigt markieren/streichen, nicht
  einfach stehen lassen.
- Sprache: Deutsch, es sei denn ausdrücklich anders gewünscht.
```

**Hinweis zur Platzierung:** in die Projekt-Anweisungen (Custom Instructions des claude.ai-
Projekts), NICHT als einzelne Chat-Nachricht — sonst gilt es nur für eine Unterhaltung statt für
jede neue Konversation im Projekt automatisch.

## 4. CLAUDE.md-Verschlankung + BACKLOG.md + TASKS.md (direkter Anschluss)

Grund: `CLAUDE.md` war auf ~150 KB angewachsen — ein normaler Web-Abruf (wie ihn der
Projektleiter-Chat nutzt) kam dadurch nur noch bis etwa v1.9.96, Backlog und Workflow-Hinweise
am Ende blieben unsichtbar.

- Alter Volltext (150KB, unverändert) archiviert: `docs/archiv/CLAUDE-historie-bis-v1.9.96.md`.
- `CLAUDE.md` neu kompakt aufgebaut (~14KB): Projektzweck, vollständige Dateiübersicht,
  Kern-Datenmodellregeln, Lehren als Kurzliste (mit Archiv-Verweis), Betrieb/Infrastruktur,
  Workflow-Pflichtschritte. Feste Schlankheitsregel oben verankert (Datei bleibt dauerhaft unter
  ~40.000 Zeichen).
- **`BACKLOG.md`** (neu, Repo-Root) als EINZIGE Backlog-Quelle angelegt: Rechercheaudit-Backlog,
  UX-/QoL-Backlog, Karten-Kalibrierungsstand je Region (Tabelle: Kanto fertig, Hoenn teilfertig,
  Johto/Sinnoh/Kalos offen), Todesursache-Ideen aus v1.9.82 — jeweils mit Quellenverweis auf
  Zeilen im Archiv. Erledigte Punkte werden durchgestrichen mit Version markiert, nicht gelöscht.
  `CLAUDE.md`s eigene Backlog-Sektion wurde durch einen reinen Verweis ersetzt (keine Dopplung).
- **`TASKS.md`** (neu, Repo-Root) als Übergabe-Datei Projektleiter → Programmierer: da der
  Projektleiter kein Schreibrecht hat, dokumentiert die Datei explizit den Workflow (Projektleiter
  formuliert im Chat → Nutzer trägt ein → Programmierer arbeitet ab → erledigte Tasks werden mit
  Version nach "Erledigte Tasks" verschoben, nicht gelöscht).
- `CLAUDE.md`s Dateiübersicht und Workflow-Pflichtschritte (Schritte 5b/5c) entsprechend ergänzt.

**Offener Punkt zum Zeitpunkt dieser Archivierung:** die finale Projektleiter-Anweisung oben
nennt noch die ALTEN Abschnittsnamen aus `CLAUDE.md` (vor der Verschlankung). Beim nächsten
Einrichten/Aktualisieren des Projektleiter-Chats die Anweisung entsprechend nachziehen — auf
`BACKLOG.md`/`TASKS.md` verweisen statt auf die inzwischen umbenannten `CLAUDE.md`-Abschnitte.

## Nachtrag (direkt im Anschluss, selber Tag)

Unmittelbar nach dem Schreiben dieser Archiv-Datei kam beim Push ein Konflikt: der Nutzer (bzw.
der Projektleiter-Chat) hatte zwischenzeitlich direkt `TASKS.md` committet und gepusht
("TASKS: Schreibzugriff Projektleiter dokumentiert, T3 eingetragen", Commit `c6799dc`). Inhalt:
der Projektleiter-Chat hat seit diesem Tag per fein-granularem GitHub-Token (Scope: nur dieses
Repo, nur "Contents") tatsächlich SCHREIBRECHT — allerdings bewusst eng begrenzt auf `TASKS.md`
allein, nicht auf Code/`CLAUDE.md`/`BACKLOG.md`. Das widerspricht der oben in Abschnitt 3
dokumentierten Annahme ("Projektleiter hat KEIN Schreibrecht") — diese Annahme war zum Zeitpunkt
der ursprünglichen Konversation korrekt, wurde aber offenbar danach vom Nutzer selbst bewusst
geändert (vermutlich genau als Lösung für das Übergabe-Problem, das `TASKS.md` lösen sollte).
`CLAUDE.md`s `TASKS.md`-Beschreibung wurde entsprechend aktualisiert (aktueller Stand gilt immer
`CLAUDE.md`, nicht diesem Archiv-Eintrag). Commits von dort kommen künftig mit `TASKS:`-Präfix,
Programmierer sollte deshalb zu Sitzungsbeginn immer `git pull` machen, bevor er pusht.
