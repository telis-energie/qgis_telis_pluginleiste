# PROJECT_LOG

## Zweck

Dieses Repo ist **kein eigenständiges QGIS-Plugin**, sondern das Referenzmuster für die geteilte `TelisToolbar`, die von allen Telis-QGIS-Plugins gemeinsam genutzt wird. Es dokumentiert, wie einzelne Plugins die Toolbar anlegen bzw. sich an eine bereits existierende anhängen.

## Persistenz-Architektur

- **bd (beads)** – ausschließlich Aufgabenverwaltung (Issues, Status, operative Planung), kein Wissensspeicher mehr.
- **Claude Memory** (`~/.claude/projects/.../memory/`) – projektspezifische Erinnerungen/Kontext, ersetzt `bd remember`.
- **PROJECT_LOG.md** (diese Datei) – lesbare Projektdokumentation: Verlauf, Entscheidungen, Erkenntnisse, aktueller Stand. Kein Todo-Ersatz.

## Verlauf

- `fddcd9e` bd init: Beads-Issue-Tracking initialisiert
- `6a4e2f0` Projekt-Claude-Kontext für qgis_telis_pluginleiste hinzugefügt
- `45385f1` config: QGIS-MCP erlaubt und mastr_matcher als zusätzliches Verzeichnis ergänzt
- `b452a41` chore: lokale Claude-Berechtigungen ergänzt (MCP, gh release)
- `4ecf8e5` chore: settings.local.json zu .gitignore hinzugefügt
- `d605903` bd init: Beads-Issue-Tracking erneut initialisiert (zweiter Init, vermutlich nach Neuaufsetzung der Datenbank)
- `d7a2b32` chore(beads): 3 Issues aus telis_db migriert
- `95ae3ce` docs: TelisToolbar-Muster dokumentiert – kein eigenständiges Plugin

## Entscheidungen & Erkenntnisse

- Keine bd-memories vorhanden (`bd memories` liefert keine Einträge) – Wissen steckte bisher nur in CLAUDE.md.
- Kernmuster (aus CLAUDE.md, Referenzimplementierung: `telis_projekte_eigentuemer.py:153–157`):

  ```python
  TOOLBAR_OBJECT_NAME = "TelisToolbar"
  TOOLBAR_NAME = "Telis"

  # 1. Prüfen ob Toolbar schon existiert (anderes Plugin hat sie angelegt)
  existing = self.iface.mainWindow().findChild(QToolBar, self.TOOLBAR_OBJECT_NAME)

  # 2. Falls nicht: neu anlegen
  toolbar = self.iface.addToolBar(self.TOOLBAR_NAME)
  toolbar.setObjectName(self.TOOLBAR_OBJECT_NAME)
  ```

  - Welches Telis-Plugin zuerst startet, erstellt die Toolbar per `objectName`.
  - Alle anderen Plugins finden sie per `findChild(QToolBar, "TelisToolbar")` und hängen ihre Aktionen an.
  - Beim Entladen des letzten Plugins wird die Toolbar aufgeräumt.
  - Betroffene Plugins: `telis_projekte_eigentuemer` (Referenz), `qgis_telis_flst_finder`, `mastr_matcher_plugin`, `saturn_planer_plugin`, `Flurstuecksuche_de`.
- Die 3 offenen bd-Issues wurden ursprünglich aus dem Projekt `telis_db` migriert (`d7a2b32`).

## Probleme & Risiken

- Keine bekannt.

## Aktueller Stand

- CLAUDE.md enthielt bis 2026-07-02 den "Beads Issue Tracker"-Block doppelt (einmal ohne, einmal mit `<!-- BEGIN/END BEADS INTEGRATION -->`-Markern) mit veralteten `bd remember`-Regeln. Beide Vorkommen wurden auf die neue Drei-Wege-Persistenz-Architektur umgestellt.
- Kein eigener Plugin-Code in diesem Repo, ausschließlich Dokumentation/Referenzmuster.

## Offene Punkte

- `qgis_telis_pluginleiste-mwg` (P2, offen): Filter-Plugin Fix ausrollen (v_eigentuemer Projektfilter)
- `qgis_telis_pluginleiste-jkx` (P3, offen): Processing Script "Flurstücke -> prj_pot" in Telis-Toolbar einbinden
- `qgis_telis_pluginleiste-tl3` (P3, offen): Tool zum Entfernen eines Flurstücks aus einem Projekt mit einem Klick
