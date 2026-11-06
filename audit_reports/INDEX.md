# audit_reports/ — Übersicht

Diese Datei listet jeden Bericht in diesem Ordner mit Generation, Thema und Umsetzungsstatus.
Angelegt als Task T3 (Projektleiter, 2026-11-06). Bei neuen Berichten hier ergänzen (nicht in
`CLAUDE.md` — Schlankheitsregel).

| Datei | Generation(en) | Thema | Status |
|---|---|---|---|
| `gen5.md` | Gen 5 (Einall: Schwarz/Weiß, Schwarz2/Weiß2) | Rechercheaudit Runde 2 (Standorte/Bosse/Level) | ✅ **umgesetzt in v1.9.38** (6 Funde) |
| `gen6.md` | Gen 6 (Kalos: X/Y) | Rechercheaudit Runde 2 (Standorte/Bosse/Level) | ✅ **umgesetzt in v1.9.39/v1.9.40** (9 Bosskarten + mehrere Korrekturen) |
| `order-gen1-3.md` | Gen 1-3 (Kanto/Johto/Hoenn, alle 10 Editionen) | Standort-**Reihenfolge**-Verifikation | ✅ **umgesetzt in v1.9.50** (15 Korrekturen) |
| `gen5-sprites.md` | Gen 5 (Einall) | Sprite-Konsistenz-Audit, Teil 1 | ✅ **umgesetzt in v1.9.42** (15 von 16 ersetzt) |
| `gen4-sprites.md` | Gen 4 (Sinnoh) | Sprite-Konsistenz-Audit, Teil 2 | ✅ **umgesetzt in v1.9.43** (1 von 4 ersetzt: Barry) |
| `gen3-sprites.md` | Gen 3 (Hoenn) | Sprite-Konsistenz-Audit, Teil 3 | ✅ **umgesetzt in v1.9.44** (7 von 26 ersetzt, via PWT-Gastauftritte) |
| `gen1-2-sprites.md` | Gen 1-2 (Kanto/Johto) | Sprite-Konsistenz-Audit, Teil 4 (Abschluss) | ✅ **abgeschlossen in v1.9.45** — 0 von 7 ersetzbar, reine Recherche ohne Code-/Datenänderung |

Sprite-Audit-Gesamtbilanz (v1.9.42–v1.9.45, über alle vier Teile): 23 von 44 geprüften statischen
Sprites auf animierte Quellen umgestellt, 14 bleiben mangels Quelle oder wegen Outfit-Konflikts
bewusst statisch, 3 weitere (Juan, Tate&Liza in zwei Editionen) zurückgestellt.

## Korrigierte Status-Köpfe (T3, 2026-11-06)

`gen5.md`, `gen6.md` und `order-gen1-3.md` trugen bis zu diesem Task noch die ursprüngliche
Recherche-Kopfzeile "Stand: recherchiert, noch **nicht** ... umgesetzt" — obwohl alle drei
Berichte längst umgesetzt waren (siehe Versionsangaben oben, per Changelog-Cross-Check
verifiziert). Köpfe wurden entsprechend korrigiert.

## Fehlende Berichte

- **Alola (Sonne/Mond/USUM)** und **Galar (Schwert/Schild)**: komplette Neu-Recherche steht noch
  aus. Die ursprünglichen Detailberichte `gen7.md`/`gen8.md` gingen mit einer abgestürzten Sitzung
  verloren, bevor sie je committet wurden — nur eine Kurzfassung überlebte im Changelog. `gen6.md`
  (Kalos) war vom selben Verlust betroffen, wurde aber bereits komplett neu recherchiert (siehe
  oben). Siehe `BACKLOG.md` Abschnitt 1 für den offenen Punkt.
- Kein eigener Bericht existiert für die Gen-1-3/Gen-4-Vollaudits (Standorte/Bosse/Level, nicht nur
  Reihenfolge oder Sprites) — deren Funde wurden direkt umgesetzt (u.a. v1.9.35 für Sinnoh), ohne
  dass ein Detailbericht im Repo abgelegt wurde. Da bereits umgesetzt, kein offener Handlungsbedarf,
  nur eine Archiv-Lücke.
