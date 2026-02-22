# PI2

## Target release metadata
- Target release date: TBD
- Target release version tag: TBD

## Summary
- Build `WITPAE_Watcher`, an application that monitors the WITPAE game save directory.
- When a game turn is detected as ended, invoke `WITPAE_Monitor` to extract turn data.
- Primary dependency repository: `WITPAE_Monitor`.

## Buildout workflow checklist
- [ ] Review currently referenced GitHub repositories used by the solution.
- [ ] If PI2 introduces a new application, add a new repository reference for it.
- [ ] Update PI2 planning details with application/function/service scope.
- [ ] Update root `README.md` PI2 section and architecture diagram.
- [ ] Update root repository index table with any new repository entry.
- [ ] Create scaffolding issues in relevant repositories with title prefix `For PI2,`.
