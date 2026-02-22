# PI2 - Decisions Needed Before Proceeding

This document tracks key decisions required to move forward with WITPAE_Watcher implementation.

## Step 2: Create WITPAE_Watcher Repository

### Decision 1: Programming Language/Runtime Selection

**Question:** What programming language and runtime should WITPAE_Watcher use?

**Options:**

| Language | Pros | Cons | File Watching Support |
|----------|------|------|----------------------|
| **Python** | • Easy to learn/maintain<br>• Excellent libraries (watchdog)<br>• Quick development<br>• Cross-platform<br>• Strong subprocess support | • Requires Python runtime<br>• Potentially slower execution<br>• Distribution requires bundling | `watchdog` library (excellent) |
| **C# (.NET)** | • Native Windows support<br>• FileSystemWatcher built-in<br>• Can compile to standalone exe<br>• Strong typing<br>• Excellent performance | • Requires .NET runtime (or self-contained)<br>• More verbose than Python<br>• Primarily Windows-focused | `FileSystemWatcher` (native, robust) |
| **Node.js** | • JavaScript/TypeScript<br>• Good libraries (chokidar)<br>• Easy JSON handling<br>• Cross-platform | • Requires Node.js runtime<br>• Less common for system tools<br>• Async complexity | `chokidar` library (good) |
| **Go** | • Single binary output<br>• Fast execution<br>• Good stdlib support<br>• Cross-platform | • Steeper learning curve<br>• Less common in Windows tooling | `fsnotify` library (good) |
| **C++** | • Native performance<br>• Matches WITPAE_Monitor<br>• No runtime needed | • Complex development<br>• Longer dev time<br>• More error-prone | Windows API directly (complex) |

**Recommendation:** **Python** or **C# (.NET)**

- **Python** if priority is rapid development, easy maintenance, and simpler code
- **C# (.NET)** if priority is native Windows integration, performance, and single-exe distribution

**Current Assessment:**
Given that:
- WITPAE_Monitor is C++ and Windows-only
- File watching needs to be reliable on Windows
- Simple subprocess invocation is needed
- Configuration parsing will be required
- Logging is essential

**→ Leaning toward C# (.NET)** for native Windows integration and FileSystemWatcher reliability

---

### Decision 2: Repository Structure

**Question:** What should the initial folder structure be?

**Option A: .NET Project Structure**
```
WITPAE_Watcher/
├── src/
│   └── WITPAE_Watcher/
│       ├── Program.cs
│       ├── FileWatcher.cs
│       ├── Configuration.cs
│       └── WITPAE_Watcher.csproj
├── tests/
│   └── WITPAE_Watcher.Tests/
├── docs/
│   └── ARCHITECTURE.md
├── config/
│   └── config.example.json
├── .gitignore
├── LICENSE
├── README.md
├── CONTRIBUTING.md
└── WITPAE_Watcher.sln
```

**Option B: Python Project Structure**
```
WITPAE_Watcher/
├── witpae_watcher/
│   ├── __init__.py
│   ├── main.py
│   ├── watcher.py
│   ├── config.py
│   └── monitor_invoker.py
├── tests/
│   └── test_watcher.py
├── docs/
│   └── ARCHITECTURE.md
├── config/
│   └── config.example.yaml
├── .gitignore
├── LICENSE
├── README.md
├── CONTRIBUTING.md
├── requirements.txt
└── setup.py
```

**Depends on:** Language choice (Decision 1)

---

### Decision 3: Initial Feature Scope

**Question:** What features should v1.0 include?

**Minimum Viable Product (MVP):**
- [x] Monitor single directory for .pws file changes
- [x] Invoke WITPAE_Monitor when file changes detected
- [x] Basic console logging
- [x] Simple configuration (hardcoded or single config file)

**Enhanced v1.0:**
- [ ] Configuration file support (JSON/YAML)
- [ ] Structured logging with levels
- [ ] Turn number tracking (avoid duplicate processing)
- [ ] Error handling and retry logic
- [ ] Status reporting

**Future versions:**
- [ ] Multiple directory monitoring
- [ ] Service/daemon mode
- [ ] Web dashboard
- [ ] Notification system
- [ ] Database integration

**Recommendation:** Start with **Enhanced v1.0** - configuration and logging are essential

---

### Decision 4: Distribution Method

**Question:** How should WITPAE_Watcher be distributed?

**Options:**

1. **Standalone Executable** (if C#)
   - Self-contained .NET app
   - No runtime installation needed
   - Larger file size (~50-100MB)
   - Simplest for end users

2. **Framework-Dependent** (if C#)
   - Requires .NET runtime installed
   - Smaller download (~1-5MB)
   - User must install .NET separately

3. **Python Package** (if Python)
   - PyPI package (`pip install witpae-watcher`)
   - Requires Python installation
   - Easy updates

4. **Python Bundled Executable** (if Python)
   - PyInstaller or similar
   - Single exe, large size
   - No Python needed

**Recommendation:** If C#, use **standalone executable** for ease of use

---

### Decision 5: Configuration Format

**Question:** What format should the configuration file use?

**Options:**
- **JSON:** Standard, built-in parsing, type-safe
- **YAML:** More readable, comments supported, requires library
- **TOML:** Modern, readability, requires library
- **INI:** Simple, legacy format

**Recommendation:** **JSON** (native support in both Python and C#, good for structured data)

**Example Configuration Structure:**
```json
{
  "watchDirectory": "C:\\Matrix Games\\War in the Pacific Admiral's Edition\\SAVE",
  "monitorExecutable": "C:\\path\\to\\witpae_monitor.exe",
  "polling": {
    "enabled": true,
    "intervalSeconds": 5
  },
  "logging": {
    "level": "INFO",
    "file": "witpae_watcher.log",
    "console": true
  },
  "processing": {
    "trackProcessedTurns": true,
    "stateFile": "processed_turns.json"
  }
}
```

---

## Actions Required

1. **User Decision:** Select programming language (Python vs C# recommended)
2. **User Decision:** Confirm repository structure based on language choice
3. **User Decision:** Approve initial feature scope (Enhanced v1.0 recommended)
4. **User Decision:** Approve distribution method
5. **User Decision:** Confirm configuration format (JSON recommended)

Once these decisions are made, Step 2 can proceed with repository creation.

---

## Recommendations Summary

| Decision | Recommendation | Rationale |
|----------|---------------|-----------|
| Language | C# (.NET) | Native Windows support, FileSystemWatcher reliability, standalone exe option |
| Structure | .NET Standard | Follows C# conventions, clear separation of concerns |
| Scope | Enhanced v1.0 | Config and logging essential for real-world use |
| Distribution | Standalone exe | No dependencies, easiest for end users |
| Config Format | JSON | Native support, structured, widely understood |
