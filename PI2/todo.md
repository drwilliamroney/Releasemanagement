# PI2 Todo

- [ ] Define turn-end detection criteria from WITPAE save artifacts (file names, timestamps, markers).
- [ ] Decide runtime/platform for watcher app and document command contract to call `WITPAE_Monitor`.
- [ ] Scaffold `WITPAE_Watcher` repository/app structure (config, logging, run script, README).
- [ ] Implement directory watcher for the game save folder with debounce/retry handling.
- [ ] Implement turn-end detector and guard against duplicate processing of the same turn.
- [ ] Invoke `WITPAE_Monitor` on detected turn end and capture output/error telemetry.
- [ ] Persist processing state (last processed turn/checksum) for restart safety.
- [ ] Add targeted tests for detection logic and monitor-invocation flow.
- [ ] Update PI2 planning/docs and root solution diagram/index to include `WITPAE_Watcher`.
- [ ] Create scaffolding issues in relevant repos with title prefix `For PI2, ...`.
