# WITPAE Tools
This "enterprise" is build around WITPAE.

## PI1

### Summary
- Added the initial portfolio for `PI1`.
- Portfolio repository: `WITPAE_Monitor`.

### Solution diagram (as it now looks)
```mermaid
flowchart TD
	A[Solution]
	A --> F[[WITPAE_Monitor - external repo]]
	click F "#repo-witpae-monitor" "Go to repository index entry"
```

## PI2

### Summary
- Initialized `PI2` release planning artifacts.
- Target release metadata set to `TBD` in `PI2/README.md`.
- Turn-boundary rule defined: `wpae002.pws` marks start of turn processing, and `wpae000.pws` marks end of turn processing (invoke extraction after stable-write checks).
- Added external repository `WITPAE_Watcher` for PI2 watcher application delivery.
- Opened PI2 scaffolding issue set in `WITPAE_Watcher` (`#1` through `#6`).

### Solution diagram (as it now looks)
```mermaid
flowchart TD
	A[Solution]
	A --> G[[WITPAE_Watcher - external repo]]
	G --> F[[WITPAE_Monitor - external repo]]
	click G "#repo-witpae-watcher" "Go to repository index entry"
	click F "#repo-witpae-monitor" "Go to repository index entry"
```

## Referenced repositories

| Repository name | Summary | README link |
| --- | --- | --- |
| <a id="repo-witpae-watcher"></a>WITPAE_Watcher | File-system watcher service for WITPAE save data that detects completed turns, applies stability checks, and invokes monitor extraction with restart-safe state handling. | [README](https://github.com/drwilliamroney/WITPAE_Watcher/blob/main/README.md) |
| <a id="repo-witpae-monitor"></a>WITPAE_Monitor | Command-line parser for War in the Pacific Admiral's Edition `.pws` scenario files that uses `pwsdll.dll` and emits structured JSON game/state entities for automation and integration workflows. | [README](https://github.com/drwilliamroney/WITPAE_Monitor/blob/main/README.md) |

