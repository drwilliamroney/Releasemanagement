# PI2 Implementation TODO

## Overview
Build WITPAE_Watcher application to monitor game save directory and invoke WITPAE_Monitor when turns complete.

---

## Phase 1: Planning & Documentation

### 1. Review existing repository dependencies
**Dependencies:** None  
**Description:** Review WITPAE_Monitor repository to understand its API, input/output formats, and integration points.

**Tasks:**
- [x] Read WITPAE_Monitor README and documentation
- [x] Identify WITPAE_Monitor entry points and invocation methods
- [x] Document WITPAE_Monitor's expected input format
- [x] Document WITPAE_Monitor's output structure
- [x] Identify game save file format and turn completion indicators

**Findings:**

#### Entry Points & Invocation
- **Executable:** `witpae_monitor.exe` (command-line tool)
- **Usage:** `witpae_monitor "path/to/file.pws"`
- **Single argument:** Full path to a `.pws` save file
- **Platform:** Windows x86 (32-bit) only
- **Dependencies:** Requires `pwsdll.dll` and `pwsdll7.dll` in PATH

#### Input Format
- **File type:** `.pws` (binary scenario save files)
- **Location:** Game SAVE directory (e.g., `C:\Matrix Games\War in the Pacific Admiral's Edition\SAVE\`)
- **Naming pattern:** `wpae###.pws` where ### is a sequential number
- **Parser:** Uses pwsdll.dll to read binary format

#### Output Structure (JSON)
WITPAE_Monitor outputs structured JSON to stdout containing:
- **gameturn:** Current turn number (integer)
- **gameinfo:** Scenario comment/timestamp
- **airgroups:** Array of air units with status
- **taskgroups:** Array of naval task forces
- **minefields:** Array of minefield positions
- **leaders:** Array of commanders
- **ships:** Array of individual ships with damage, cargo, location
- **shipclasses:** Array of ship class definitions
- **pilots:** Array of pilot roster
- **planes:** Array of aircraft types
- **devices:** Array of equipment types
- **locations:** Array of bases with facilities, units, supplies
- **Done:** Completion flag (value: 1)

#### Turn Completion Detection Strategy
- Monitor `.pws` files in SAVE directory for modifications
- File modification indicates potential turn processing
- Parse JSON output to extract `gameturn` field
- Track last processed turn number to detect new turns
- File naming increments (wpae001.pws, wpae002.pws, etc.) may indicate save progression

---

### 2. Create WITPAE_Watcher repository
**Dependencies:** Step 1  
**Description:** Create a new GitHub repository for the WITPAE_Watcher application.

**📋 See [DECISIONS_NEEDED.md](DECISIONS_NEEDED.md) for detailed decision analysis and recommendations**

**Questions to Answer:**
1. **Programming Language/Runtime:** What language/platform should WITPAE_Watcher use?
   - Options: C# (.NET), Python, Node.js, Go, Rust, C++
   - Considerations:
     - Must run on Windows (same as WITPAE_Monitor)
     - Should support file system watching natively
     - Must be able to invoke subprocess (WITPAE_Monitor)
     - Ease of development and maintenance
     - Community support and libraries available
   - **Recommendation:** Python or C# (.NET) - both have excellent file watching libraries and subprocess support

2. **Repository Structure:** What folders/files should be in the initial setup?
   - Source code directory name: `src/`, `lib/`, `WITPAE_Watcher/`?
   - Configuration examples location
   - Documentation structure
   - Test organization

3. **License:** What license should be used?
   - **Recommendation:** MIT License (matches WITPAE_Monitor for consistency)

4. **Initial Features Scope:** What should be included in v1.0?
   - Basic file watching only?
   - Configuration file support from start?
   - Logging from start?
   - Service/daemon mode or console app only?

5. **Build/Packaging:** How will the application be distributed?
   - Standalone executable?
   - Requires runtime installation?
   - Installer or manual deployment?

**Tasks:**
- [ ] **Decision:** Choose programming language/runtime (document rationale)
- [ ] **Decision:** Define initial repository structure
- [ ] Create new repository: `drwilliamroney/WITPAE_Watcher`
- [ ] Initialize with README (include purpose, requirements, quick start placeholder)
- [ ] Add LICENSE file (MIT recommended)
- [ ] Add appropriate .gitignore for chosen language
- [ ] Add repository description: "File system watcher for WITPAE game saves that triggers turn data extraction"
- [ ] Set repository topics/tags: `witpae`, `file-watcher`, `game-automation`, `turn-based`
- [ ] Create initial folder structure:
  - [ ] Source code directory
  - [ ] `docs/` directory
  - [ ] `tests/` directory
  - [ ] `config/` directory for example configurations
- [ ] Add CONTRIBUTING.md with contribution guidelines
- [ ] Add initial README.md sections:
  - [ ] Project description
  - [ ] Prerequisites/requirements
  - [ ] Installation (placeholder)
  - [ ] Configuration (placeholder)
  - [ ] Usage (placeholder)
  - [ ] License reference
- [ ] **Optional:** Set up branch protection for main branch
- [ ] **Optional:** Create initial project board for issue tracking

---

### 3. Update PI2 planning documentation
**Dependencies:** Step 2  
**Description:** Update PI2/README.md with detailed scope, architecture, and deliverables.

**Tasks:**
- [ ] Add WITPAE_Watcher application details to PI2/README.md
- [ ] Document watcher configuration requirements (file paths, polling intervals)
- [ ] Document integration flow between Watcher and Monitor
- [ ] Add technical architecture section
- [ ] Define success criteria and acceptance tests
- [ ] Update target release date and version tag (if known)

---

### 4. Update root README.md
**Dependencies:** Step 3  
**Description:** Update the root repository's README.md with PI2 solution diagram and repository index.

**Tasks:**
- [ ] Update PI2 solution diagram to include WITPAE_Watcher node
- [ ] Add clickable link from WITPAE_Watcher node to repository index
- [ ] Add WITPAE_Watcher entry to Referenced Repositories table
- [ ] Create stable anchor ID for WITPAE_Watcher table entry
- [ ] Update PI2 summary with watcher application details

---

## Phase 2: Repository Setup & Issue Creation

### 5. Create scaffolding issues in WITPAE_Watcher
**Dependencies:** Step 2  
**Description:** Create GitHub issues for initial scaffolding work in the WITPAE_Watcher repository.

**Tasks:**
- [ ] Issue: "For PI2, Set up project structure and build configuration"
- [ ] Issue: "For PI2, Implement file system watcher for game save directory"
- [ ] Issue: "For PI2, Implement turn completion detection logic"
- [ ] Issue: "For PI2, Implement WITPAE_Monitor invocation mechanism"
- [ ] Issue: "For PI2, Add configuration file support (paths, settings)"
- [ ] Issue: "For PI2, Add logging and error handling"
- [ ] Issue: "For PI2, Create unit tests for core functionality"
- [ ] Issue: "For PI2, Create integration tests with WITPAE_Monitor"
- [ ] Issue: "For PI2, Write user documentation and setup guide"

---

### 6. Define technical requirements
**Dependencies:** Step 1, Step 3  
**Description:** Document detailed technical requirements and design decisions.

**Tasks:**
- [ ] Choose programming language/framework for WITPAE_Watcher
- [ ] Define file system monitoring approach (polling vs. events)
- [ ] Define turn completion detection algorithm
- [ ] Specify configuration file format (JSON, YAML, etc.)
- [ ] Define logging strategy and log levels
- [ ] Specify error handling and retry logic
- [ ] Define performance requirements (latency, resource usage)

---

## Phase 3: Core Implementation

### 7. Set up WITPAE_Watcher project structure
**Dependencies:** Step 6  
**Description:** Initialize the project with build system, dependencies, and folder structure.

**Tasks:**
- [ ] Create build configuration (package.json, requirements.txt, etc.)
- [ ] Set up dependency management
- [ ] Create src/ folder structure
- [ ] Create tests/ folder structure
- [ ] Set up linting and code formatting
- [ ] Configure CI/CD pipeline (GitHub Actions)

---

### 8. Implement configuration system
**Dependencies:** Step 7  
**Description:** Build configuration loading and validation.

**Tasks:**
- [ ] Create configuration file schema
- [ ] Implement configuration file parser
- [ ] Add validation for required fields
- [ ] Add default value handling
- [ ] Document configuration options
- [ ] Create example configuration file

---

### 9. Implement file system watcher
**Dependencies:** Step 7, Step 8  
**Description:** Build the core file monitoring capability.

**Tasks:**
- [ ] Implement directory monitoring logic
- [ ] Add file change detection
- [ ] Filter for relevant file types (save files)
- [ ] Implement debouncing/throttling to avoid duplicate triggers
- [ ] Add startup directory scan for existing files
- [ ] Handle watcher errors and restart logic

---

### 10. Implement turn completion detection
**Dependencies:** Step 9  
**Description:** Build logic to identify when a game turn has completed.

**Tasks:**
- [ ] Define turn completion criteria (file patterns, contents, timestamps)
- [ ] Implement file parsing/inspection logic
- [ ] Add state tracking to avoid processing same turn multiple times
- [ ] Implement persistence for processed turn tracking
- [ ] Add logging for detected turns

---

### 11. Implement WITPAE_Monitor integration
**Dependencies:** Step 10  
**Description:** Build the mechanism to invoke WITPAE_Monitor when turns complete.

**Tasks:**
- [ ] Implement subprocess/process invocation
- [ ] Build command-line argument construction
- [ ] Add output capture and parsing
- [ ] Implement error handling for Monitor failures
- [ ] Add retry logic with exponential backoff
- [ ] Log Monitor execution results

---

### 12. Implement logging system
**Dependencies:** Step 7  
**Description:** Set up comprehensive logging throughout the application.

**Tasks:**
- [ ] Configure logging framework
- [ ] Add log levels (DEBUG, INFO, WARNING, ERROR)
- [ ] Implement log rotation
- [ ] Add structured logging for key events
- [ ] Create log output configuration (file, console)
- [ ] Add performance metrics logging

---

## Phase 4: Testing & Quality Assurance

### 13. Create unit tests
**Dependencies:** Steps 8-12  
**Description:** Build comprehensive unit test suite.

**Tasks:**
- [ ] Test configuration loading and validation
- [ ] Test file system watcher logic
- [ ] Test turn completion detection
- [ ] Test Monitor invocation mechanism
- [ ] Test error handling scenarios
- [ ] Achieve >80% code coverage

---

### 14. Create integration tests
**Dependencies:** Step 13  
**Description:** Build end-to-end integration tests.

**Tasks:**
- [ ] Test full workflow: file change → turn detection → Monitor invocation
- [ ] Test configuration loading from file
- [ ] Test with mock file system changes
- [ ] Test with actual WITPAE save files (if available)
- [ ] Test error recovery scenarios
- [ ] Test long-running stability

---

### 15. Manual testing and validation
**Dependencies:** Step 14  
**Description:** Perform manual testing in realistic scenarios.

**Tasks:**
- [ ] Test with actual WITPAE game installation
- [ ] Verify turn detection accuracy
- [ ] Validate Monitor integration produces expected output
- [ ] Test configuration changes while running
- [ ] Verify logging output quality
- [ ] Test resource usage (CPU, memory, disk I/O)

---

## Phase 5: Documentation & Deployment

### 16. Create user documentation
**Dependencies:** Step 15  
**Description:** Write comprehensive documentation for end users.

**Tasks:**
- [ ] Write README with overview and quick start
- [ ] Document installation process
- [ ] Document configuration options with examples
- [ ] Create troubleshooting guide
- [ ] Add FAQ section
- [ ] Document system requirements

---

### 17. Create developer documentation
**Dependencies:** Step 15  
**Description:** Document architecture and development processes.

**Tasks:**
- [ ] Document code architecture and design decisions
- [ ] Create API/interface documentation
- [ ] Document build and test procedures
- [ ] Add contributing guidelines
- [ ] Document release process

---

### 18. Prepare for release
**Dependencies:** Steps 16, 17  
**Description:** Finalize release artifacts and versioning.

**Tasks:**
- [ ] Set version number
- [ ] Create CHANGELOG
- [ ] Tag release in git
- [ ] Build release artifacts (executables, packages)
- [ ] Test release artifacts on clean system
- [ ] Update PI2/README.md with actual release date and version

---

### 19. Update solution documentation
**Dependencies:** Step 18  
**Description:** Finalize all documentation in the Releasemanagement repository.

**Tasks:**
- [ ] Update root README.md PI2 section with completion summary
- [ ] Update solution diagram to reflect final architecture
- [ ] Verify all repository links are functional
- [ ] Complete PI2 buildout workflow checklist
- [ ] Add "as it now looks" diagram showing completed state

---

### 20. Close PI2 and merge PR
**Dependencies:** Step 19  
**Description:** Final review and merge of PI2 branch.

**Tasks:**
- [ ] Review all changes in PI2 branch
- [ ] Verify all checklist items complete
- [ ] Convert draft PR to ready for review
- [ ] Merge PI2 pull request
- [ ] Create git tag for PI2 completion
- [ ] Archive PI2 planning materials

---

## Dependency Graph Summary

```
Phase 1: Planning & Documentation
1 → 2 → 3 → 4
     └→ 5

Phase 2: Repository Setup
1, 3 → 6
2 → 5

Phase 3: Implementation
6 → 7 → 8, 9, 12
9 → 10 → 11

Phase 4: Testing
8-12 → 13 → 14 → 15

Phase 5: Deployment
15 → 16, 17 → 18 → 19 → 20
```

## Critical Path
1 → 2 → 3 → 6 → 7 → 9 → 10 → 11 → 13 → 14 → 15 → 16 → 18 → 19 → 20

## Estimated Timeline
- Phase 1: 2-3 days
- Phase 2: 1-2 days  
- Phase 3: 1-2 weeks
- Phase 4: 3-5 days
- Phase 5: 2-3 days

**Total estimated duration: 3-4 weeks**
