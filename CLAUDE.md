# Project Instructions for AI Agents

This file provides instructions and context for AI coding agents working on this project.

## Beads Issue Tracker

This project uses **bd (beads)** for issue tracking. Run `bd prime` to see full workflow context and commands.

### Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --claim  # Claim work
bd close <id>         # Complete work
```

### Rules

- Use `bd` for ALL task tracking — do NOT use TodoWrite, TaskCreate, or markdown TODO lists
- Run `bd prime` for detailed command reference and session close protocol
- Use `bd remember` for persistent knowledge — do NOT use MEMORY.md files

## Session Completion

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd dolt push
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds

## Projekttyp: Dokumentation / Referenzmuster

Dieses Repo enthält **kein eigenständiges Plugin**. Es dokumentiert das verteilte Toolbar-Muster aller Telis-QGIS-Plugins.

### Prinzip: Geteilte TelisToolbar

Die Telis-Werkzeugleiste existiert nicht als eigenes Plugin. Stattdessen trägt **jedes Telis-Plugin** die Toolbar selbst ein:

```python
TOOLBAR_OBJECT_NAME = "TelisToolbar"
TOOLBAR_NAME = "Telis"

# 1. Prüfen ob Toolbar schon existiert (anderes Plugin hat sie angelegt)
existing = self.iface.mainWindow().findChild(QToolBar, self.TOOLBAR_OBJECT_NAME)

# 2. Falls nicht: neu anlegen
toolbar = self.iface.addToolBar(self.TOOLBAR_NAME)
toolbar.setObjectName(self.TOOLBAR_OBJECT_NAME)
```

- Welches Telis-Plugin zuerst startet, erstellt die Toolbar
- Alle anderen finden sie per `findChild(QToolBar, "TelisToolbar")` und hängen sich dran
- Beim Entladen des letzten Plugins wird sie aufgeräumt

### Betroffene Plugins

- `telis_projekte_eigentuemer` (Referenzimplementierung: telis_projekte_eigentuemer.py:153–157)
- `qgis_telis_flst_finder`
- `mastr_matcher_plugin`
- `saturn_planer_plugin`
- `Flurstuecksuche_de`

### Aktive Agenten

- `~/.claude/agents/telis-db.md` – PostgreSQL/PostGIS-Konventionen (bei Bedarf laden)


<!-- BEGIN BEADS INTEGRATION v:1 profile:minimal hash:ca08a54f -->
## Beads Issue Tracker

This project uses **bd (beads)** for issue tracking. Run `bd prime` to see full workflow context and commands.

### Quick Reference

```bash
bd ready              # Find available work
bd show <id>          # View issue details
bd update <id> --claim  # Claim work
bd close <id>         # Complete work
```

### Rules

- Use `bd` for ALL task tracking — do NOT use TodoWrite, TaskCreate, or markdown TODO lists
- Run `bd prime` for detailed command reference and session close protocol
- Use `bd remember` for persistent knowledge — do NOT use MEMORY.md files

## Session Completion

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git pull --rebase
   bd dolt push
   git push
   git status  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes, prune remote branches
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Work is NOT complete until `git push` succeeds
- NEVER stop before pushing - that leaves work stranded locally
- NEVER say "ready to push when you are" - YOU must push
- If push fails, resolve and retry until it succeeds
<!-- END BEADS INTEGRATION -->
