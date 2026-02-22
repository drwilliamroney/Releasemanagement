# PI2

## Target release metadata
- Target release date: TBD
- Target release version tag: TBD

## Summary
- Build `WITPAE_Watcher`, an application that monitors the WITPAE game save directory.
- When a game turn is detected as ended, invoke `WITPAE_Monitor` to extract turn data.
- Primary dependency repository: `WITPAE_Monitor`.
- PI2 application repository: `WITPAE_Watcher`.

## Repository references
- `WITPAE_Watcher`: https://github.com/drwilliamroney/WITPAE_Watcher
- `WITPAE_Monitor`: https://github.com/drwilliamroney/WITPAE_Monitor

## Scaffolding issue tracker
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/1
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/2
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/3
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/4
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/5
- https://github.com/drwilliamroney/WITPAE_Watcher/issues/6

## Implementation progress
- Local scaffold initialized for `WITPAE_Watcher` in `external/WITPAE_Watcher`.
- Starter modules added: config, watcher service, turn detector, monitor runner, state store, and CLI entrypoint.
- Targeted detector tests pass locally (`2 passed`).

## Turn-end detection planning details
- Treat `wpae002.pws` as the start-of-turn-processing signal.
- Treat `wpae000.pws` as the end-of-turn-processing signal and extraction trigger (after stable-write checks).
- Use a stable-write window before invocation to avoid partial-write processing.

## Runtime planning details
- `WITPAE_Watcher` will run on `Python 3`.
- Final minimum supported Python 3 minor version is `TBD` until environment validation is complete.

## Deployment layout planning details
- `WITPAE_Watcher` and `WITPAE_Monitor` will be deployed in the same directory.
- Required DLLs for monitor execution are co-located in that same directory.
- Watcher invocation uses this shared directory as the working directory to avoid separate DLL path setup.

## Buildout workflow checklist
- [x] Review currently referenced GitHub repositories used by the solution.
- [x] If PI2 introduces a new application, add a new repository reference for it.
- [x] Update PI2 planning details with application/function/service scope.
- [x] Update root `README.md` PI2 section and architecture diagram.
- [x] Update root repository index table with any new repository entry.
- [x] Create scaffolding issues in relevant repositories with title prefix `For PI2,`.

