# Nuzlocke Tracker — Projektgedächtnis

> **SCHLANKHEITSREGEL (verbindlich):** Diese Datei bleibt dauerhaft unter ca. 40.000 Zeichen.
> Hier steht nur, WAS aktuell gilt — nicht die Geschichte, wie es dazu kam. Ausführliche
> Herleitungen/Begründungen zu einer neuen Änderung gehören in `CHANGELOG_HTML` (die
> App-Changelog-Konstante in `nuzlocke-v2-editionen.html`) bzw. bei größeren Audits in
> eine Datei unter `docs/archiv/`. Wird ein früherer Fehler korrigiert: neuen, kurzen
> Eintrag hier ergänzen, alte Einträge nicht umschreiben. Vor dem Schreiben eines neuen
> Abschnitts hier immer fragen: "gehört das als dauerhafte Regel hierher, oder ist das nur
> die Begründung EINER Änderung?" — Letzteres gehört ins Changelog/Archiv.
>
> Volltext der kompletten Projekthistorie bis v1.9.96 (jede Änderungsrunde mit voller
> Begründung, Zitaten, Präzedenzfällen): **`docs/archiv/CLAUDE-historie-bis-v1.9.96.md`**.
> Bei Unsicherheit über das WARUM einer bestehenden Regel dort nachschlagen, nicht raten.

Diese Datei existiert, damit eine neue/abgestürzte Claude-Sitzung den Kontext nicht erst
mühsam neu rekonstruieren muss. Regel seit einer frühen, irreversibel abgestürzten Sitzung:
**alles Wichtige landet als committete Datei im Repo, nicht nur im Chat-Kontext.**

## Projektzweck

Ein Nuzlocke-Run-Tracker für Pokémon-Randomizer-Runs, als einzelne selbstständige HTML-Datei
(Vanilla JS, kein Build-Schritt, kein Framework) gebaut, veröffentlicht als Claude-Artifact
und zusätzlich als installierbare Offline-PWA über Netlify. Ziel-Meilenstein **"Version 2.0"**
ist erreicht, sobald **alle Editionen vollständig vorhanden sind** (aktuell: Schwert/Schild-DLC
und einzelne, im Changelog dokumentierte Datenlücken fehlen noch, siehe "Offener Backlog" unten).

Repo: `github.com/RadoSantar/Nuzlocke-Tracker`, Branch `claude/magical-cray-d6vvlx`
(= auch GitHub-Standard-Branch). Live-Artifact: `https://claude.ai/artifact/DuhLSvkBi5S43eBS8pnGF7`.

## Dateiübersicht

- **`CLAUDE.md`** — dieses Projektgedächtnis (Schlankheitsregel s.o.).
- **`README.md`** — Wiederherstellungs-Anleitung für eingefrorene Checkpoints (`git show`-Befehle
  je Checkpoint) + kurzer Netlify-/PWA-Setup-Überblick.
- **`BACKLOG.md`** — die EINZIGE Backlog-Quelle (Rechercheaudit, UX/QoL, Karten-
  Kalibrierungsstand je Region, Todesursache-Ideen), gegliedert mit Quellenverweisen. Erledigte
  Punkte werden durchgestrichen mit Version markiert, nicht gelöscht. **Bei jedem Commit
  mitpflegen** (siehe Workflow-Pflichtschritte unten) — `CLAUDE.md` selbst führt keine eigene
  Backlog-Liste mehr, um Dopplung/Drift zwischen zwei Quellen zu vermeiden.
- **`docs/archiv/CLAUDE-historie-bis-v1.9.96.md`** — vollständiger, unveränderter Volltext der
  bisherigen `CLAUDE.md`-Fassungen; jede einzelne Änderungsrunde mit voller Begründung/Lehre.
  Künftige große Rechercheaudit-Berichte oder weitere Archiv-Abschnitte kommen ebenfalls unter
  `docs/archiv/` (eigene Datei pro Thema/Zeitraum), nicht in `CLAUDE.md` selbst.
- **`nuzlocke-v2-editionen.html`** — die aktiv weiterentwickelte, "lebende" App-Datei. Alle
  Code-/Datenänderungen passieren hier.
- **`nuzlocke-v1-baseline.html`**, **`nuzlocke-v2-standard.html`** — eingefrorene
  Wiederherstellungspunkte, werden nie mehr verändert.
- **`nuzlocke-netlify-deploy.zip`** — NICHT committet (`.gitignore`), lokal per
  `tools/build-netlify-zip.js` gebautes Deploy-Artefakt. Ein im Repo liegender alter Stand wäre
  kein echter Hinweis auf den aktuellen Zustand, da er nicht Teil der Versionshistorie ist.
- **`audit_reports/*.md`** — abgeschlossene Rechercheaudit-Berichte je Generation/Thema (z.B.
  `gen5.md` = Einall, `order-gen1-3.md` = Standort-Reihenfolge-Verifikation Gen 1-3). Sofort nach
  Fertigstellung committen/pushen, nicht erst am Ende einer Sitzung sammeln — genau das Versäumnis,
  das die früheren `gen7.md`/`gen8.md` (Alola/Galar) verloren gehen ließ.
- **`pwa/`** — `manifest.json`, `sw.js`, vier Icon-Dateien für den Offline-Installations-Build.
- **`sprites/`** — 2027+ Sprite-/Kartenbilddateien (`legacy/`, `modern/`, `boss/`, `badges/`,
  `maps/`), ausgelagert aus den Base64-JS-Konstanten der App.
- **`tools/validate-editions.js`** — Datenvalidierung pro Edition (doppelte IDs, verwaiste Bosse,
  unbekannte `bossAfter`-Verweise/`ace`-Spezies). Vor jedem Commit mit Datenänderungen laufen
  lassen.
- **`tools/extract-sprites.js`** — extrahiert Base64-Sprite-Werte in echte Dateien unter
  `sprites/`, ersetzt sie im Code durch Pfad-Strings. Idempotent.
- **`tools/inline-sprites.js`** — Gegenstück, bettet `sprites/...`-Dateien für den
  Artifact-Publish-Build wieder als Base64 ein (Artifact erlaubt nur ≤255 Dateien).
- **`tools/make-artifact-bare.js`** — ruft zuerst `inline-sprites.js` auf, strippt dann
  doctype/html/head/body. **Immer** diese gestrippte Ausgabe publizieren, nie die Rohdatei.
- **`tools/build-netlify-zip.js`** — baut das Netlify-ZIP korrekt flach (nie manuell `zip -r`
  bauen) und patcht `sw.js`s `CACHE_NAME` automatisch auf die aktuelle `APP_VERSION`.
- **`.gitignore`** — schließt nur das generierte Netlify-ZIP aus.

## Kern-Datenmodellregeln (`nuzlocke-v2-editionen.html`)

- `GAMES` — Registry pro Edition: `regions`, `bosses`, `bossAfter` (Standort→Boss-IDs, steuert
  wann ein Bosskampf auf der Karte erscheint), `starters`, `theme`, `generation`.
- Boss-Einträge tracken nur das Ass (`ace`), nicht das komplette Gegner-Team — dafür gibt es das
  separate, optionale Freitextfeld (Hausregel-Schalter "Gegner-Team tracken").
- Multi-Battles/Verbündeten-Doppelkämpfe (Rivale kämpft MIT dir gegen Dritte) sind KEINE
  `cls:"Rivale"`-Bosskarte — sonst suggeriert die App fälschlich, man müsse ihn dort besiegen.
- **"Route-22-Falle":** wird ein Standort im Spielverlauf nur wegen `bossAfter`-Positionierung
  ein zweites Mal betreten, braucht dieser zweite Eintrag `noCatch:true` — sonst suggiert die
  App einen zweiten, unabhängigen Fangversuch, den es in einer Nuzlocke-Regel nicht gibt. Gilt
  genauso für Kartenpunkte/-flächen zweier Standorte am selben realen Ort (DOM-Reihenfolge
  entscheidet bei Überlappung, später gerenderte Elemente gewinnen den Klick).
  **Wichtig:** ein fehlender eigener Wiki-Artikel für ein Teilgebiet ist KEIN Beleg dafür, dass
  es mit der übergeordneten Stadt identisch ist — im Zweifel beim Nutzer nachfragen statt aus
  Artikelstruktur zu schließen (Nevaio-Moor-Fall, v1.9.98).
- `buildVersionGames()` erzeugt Versions-Trios (z.B. Rot/Blau/Gelb) aus einem gemeinsamen
  Basis-Datensatz mit punktuellen Overrides.
- Postgame-Standorte, die auf der Karte zeitlich zu früh erscheinen würden: als eigene, ans Ende
  angehängte Kachel führen, nicht am alten Standort-Eintrag bündeln (außer dieser steht selbst
  schon ganz am Anfang/Ende der Liste).
- Neue Edition ergänzen: Anleitung als Kommentar direkt über `KALOS_LOCATIONS` in der Datei.
  Standort-Reihenfolge aktiv verifizieren — pro Standort die "Connecting areas"-Angabe seiner
  eigenen Bulbapedia-Seite prüfen, eine reine Walkthrough-Fließtext-Zusammenfassung übersieht
  Fälle (siehe `audit_reports/order-gen1-3.md`).
- `REGION_MAPS[edition].points[name]`: Array `[x,y]` (Punkt) ODER `{quad:[[x,y],...]}`
  (Fläche/Route, beliebig viele Ecken). Flächen werden in `artworkMapHtml()` IMMER vor Punkten
  gerendert, sonst fängt eine Fläche fälschlich Klicks auf überlappenden Punkten ab.
  Kalibrierung ausschließlich über den eingebauten "Punkte selbst kalibrieren"-Modus (liefert
  reale, vom Nutzer abgetippte Koordinaten) — nie Koordinaten raten/interpolieren.
- Einklapp-Mechanik: zwei Sammel-Gruppen PRO REGION — grau/`expandedRegions` für automatisch
  eingeklappte ERLEDIGTE Standorte, gold/`expandedStashRegions` für manuell zurückgestellte OFFENE
  Standorte (`state.manualCollapsedLocs`, funktioniert für Standort- UND Boss-Kacheln).

## Feste Lehren (Kurzfassung — volle Herleitung je im Archiv)

- Fehlender eigener Wiki-Artikel für ein Teilgebiet beweist NICHT reale Ortsidentität mit der
  übergeordneten Stadt (s.o., v1.9.98).
- WebFetch-Zusammenfassungen können eine URL "exakt" zitieren, die trotzdem ein 404 ist — jede
  Asset-URL (Bilder u.ä.), die wirklich heruntergeladen werden soll, per direktem `curl`
  gegenprüfen, nicht auf die Zusammenfassung allein verlassen.
- Ähnlich klingende deutsche Pokémon-Namen können andere Spezies sein (z.B. "Klikk"=Klink≠
  Joltik, "Zwirrfinst"≠Banette-Familie, "Flunkifer"=Mawile≠Accelgor/Hydragil) — gegenprüfen.
- KI-Zusammenfassungen von Serebii-/Bulbapedia-Seiten (über Suche statt direktem Fetch) können
  Kampf-Reihenfolgen/Level durcheinanderbringen — Trainer-Tabelle im Zweifel direkt fetchen.
- `validate-editions.js` prüft nur bis zum `injectEditionThemeCSS();`-Marker — Änderungen danach
  zusätzlich mit `node --check` auf den extrahierten `<script>`-Inhalt prüfen.
- Ein Kachel-Objekt, das mehrere `kind`-Varianten über gemeinsamen Code verarbeitet, braucht bei
  JEDER neuen Variante dieselben Pflichtfelder (fehlendes `id`-Feld bei Boss-Kacheln, v1.9.69) —
  das fällt beim Draufschauen nicht auf, nur beim Prüfen des tatsächlichen Zielzustands.
- Bei `scrollIntoView({behavior:"smooth"})` nie eine geratene feste Wartezeit vor einer
  nachfolgenden Positionsmessung einbauen — das `scrollend`-Event abwarten (mit Timeout-Fallback
  für ältere Safari-Versionen). Eine "Position seit N Frames unverändert"-Heuristik ist KEIN
  verlässlicher Ersatz dafür.
- Ein UI-Element, das sich an anderen, potenziell wachsenden UI-Stapeln orientiert (z.B.
  FAB-Reihen), sollte seine Position live per `getBoundingClientRect()` ableiten, nicht aus einer
  zum Implementierungszeitpunkt passenden, aber stillschweigend alternden Konstante.
- Service-Worker `CACHE_NAME` muss bei jedem Build mit `APP_VERSION` mitziehen (automatisiert in
  `build-netlify-zip.js`) — sonst zeigt eine installierte PWA unbemerkt einen veralteten Stand.
- "Vergrößert" kann zwei verschiedene Dinge bedeuten: mehr Abstand zwischen Elementen ≠ größere
  Antipp-Ziele der Elemente selbst — bei fixgrößigen Overlays auf skalierter Fläche beides
  einzeln prüfen.
- Eine Funktion, die erst nach einer Bedingung im DOM erscheint (z.B. Soul-Link-Modus erst nach
  Partner-Verknüpfung), braucht einen Hinweis/Guard VOR dieser Bedingung — sonst faktisch
  unauffindbar, egal wie gut dokumentiert.
- `justify-content:center`/`align-items:center` per Flex/Grid bei potenziell überlaufendem
  scrollbaren Inhalt vermeiden (Überlauf wird einseitig unerreichbar) — `margin:auto` auf dem
  Kind in normalem Block-Fluss bevorzugen.
- Existenzlücken (komplett fehlender Standort, z.B. Urzeithöhle/Safari-Zone) werden von einer
  Reihenfolge-Verifikation NICHT mitgefunden — das ist eine andere Prüfungsart, beide bei Audits
  explizit einzeln einplanen.

## Betrieb/Infrastruktur

- **Supabase (Cloud-Sync-Backend, nicht im Repo):** Projekt-ID `cyaanqljqxzsqlzeaaev`. Tabellen
  `nuzlocke_saves`, `nuzlocke_pairing_pins` — RLS aktiv OHNE Policies (Absicht), Zugriff
  ausschließlich über 4 SECURITY-DEFINER-RPCs (`nuzlocke_get_save`/`put_save`/
  `create_pairing_pin`/`resolve_pairing_pin`). Schema-Änderungen per `apply_migration`, danach
  `get_advisors(type:"security")` — nur ein NEUER, andersartiger Hinweis ist ein echtes Warnsignal.
  Test-Zeilen nach Live-Tests wieder löschen, nie echte Nutzer-Zeilen anfassen.
- **Netlify hat KEIN Auto-Deploy** — nach jeder Änderung `tools/build-netlify-zip.js` neu bauen
  und das komplette ZIP manuell auf `app.netlify.com/drop` ziehen.
- **Artifact-Publish:** immer die per `tools/make-artifact-bare.js` gebaute Datei publizieren,
  nie `nuzlocke-v2-editionen.html` direkt. Vor dem ersten Publish einer Sitzung die Live-Version
  per `Artifact(action:"read")` lesen (sonst wird der Publish abgelehnt).

## Offener Backlog

Vollständig in **`BACKLOG.md`** (Repo-Root) — gegliedert nach Rechercheaudit-Backlog,
UX-/QoL-Backlog, Karten-Kalibrierungsstand je Region und Todesursache-Ideen, jeweils mit
Quellenverweis. Dort auch nachsehen, bevor ein neuer Task zu einem dieser Themen formuliert
wird (Dopplungen vermeiden).

## Workflow-Pflichtschritte vor jedem Commit

1. Datenänderungen (Bosse/Standorte): `node tools/validate-editions.js` — bei Fehlern NICHT
   committen.
2. Code-Änderungen jenseits des `injectEditionThemeCSS();`-Markers: zusätzlich `node --check`
   auf dem extrahierten `<script>`-Inhalt.
3. UI-/Verhaltensänderungen: per Playwright das TATSÄCHLICHE Zielverhalten verifizieren, nicht
   nur "kein Fehler ausgelöst".
4. `APP_VERSION` hochzählen; neuen `<div class="entry">` ganz oben in `CHANGELOG_HTML` einfügen;
   "Versionsstände"-Stat-Kachel und Footer-Versionsnummer mitziehen.
5. `CLAUDE.md` pflegen: neue dauerhafte Regeln/Lehren knapp ergänzen (Schlankheitsregel!); bei
   Korrektur eines früheren Fehlers neuen Eintrag ergänzen, nichts umschreiben.
5b. `BACKLOG.md` pflegen: neu entstandene offene Punkte ergänzen, erledigte Punkte
   DURCHSTREICHEN mit Version (nicht löschen), Quellenverweis aktuell halten.
6. Vor jedem Artifact-Publish: `node tools/make-artifact-bare.js`, dann die gestrippte Ausgabe
   publizieren.
7. Für die PWA: `node tools/build-netlify-zip.js`, ZIP komplett auf `app.netlify.com/drop`
   ziehen.
8. Committen (Branch `claude/magical-cray-d6vvlx`) und pushen.
9. Größere Rechercherunden (Audits) zusätzlich: Bericht in `audit_reports/` SOFORT committen,
   dann dem Nutzer zum Gegenchecken vorlegen, bevor App-Code geändert wird.
