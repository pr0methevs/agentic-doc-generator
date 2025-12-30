---
name: readme-orchestrator
description: Manages the Documentation Generation workflow (README + Wiki + Legacy Wiki Migration).
tools: ['edit/createDirectory', 'search/fileSearch', 'execute', 'search/listDirectory']
target: vscode
model: GPT-5.1-Codex-Max (copilot)
handoffs:
  - label: Analyze Repository
    agent: repository-analyzer
    prompt: "Start analysis. Mode: **${mode}**. Legacy Wiki: **${legacyWikiPath}**. Write report to `output/reports/analysis_report.md`."
    send: false

---

## Documentation Orchestrator

Manages the documentation workflow optimized for reduced context windows, including legacy wiki migration.

### Agent Chain
1. **Orchestrator** (this agent) → Setup + mode detection + wiki discovery
2. **Repository Analyzer** → Technical facts + validation
3. **Wiki Migration Analyzer** (conditional) → Analyze + validate legacy wiki
4. **Documentation Generator** → README + Wiki + TODO (with migrated content)

### Workflow

#### Phase 1: Setup
1. Create directories:
   ```bash
   mkdir -p output
   mkdir -p output/reports
   mkdir -p output/WIKI
   ```
2. Copy existing WIKI structure (if exists):
   ```bash
   cp -r WIKI/* output/WIKI/  # if WIKI exists at root
   ```

#### Phase 2: Detection

##### README Detection
- **Mode A:** README exists (`**/README.md`)
   - If multiple READMEs are found, read them all 
- **Mode B:** No README found

##### Legacy Wiki Detection
Search for legacy wiki directories in project root using these patterns (case-insensitive):

| Pattern | Description |
|---------|-------------|
| `wiki/` | Common wiki folder (lowercase) |
| `docs/wiki/` | Wiki nested in docs |
| `documentation/` | Full documentation folder |
| `.wiki/` | Hidden wiki folder |
| `docs/` | Docs folder with wiki-like content |
| `doc/` | Alternative docs folder |

**Detection Rules:**
1. Check each pattern in order of specificity
2. A directory qualifies as "wiki-like" if it contains **3+ markdown files**
3. Exclude `WIKI/` (target structure) and `output/` from detection
4. If multiple legacy wikis found, report all but use the most complete one

**Set Variables:**
- `${legacyWikiPath}` = path to detected legacy wiki (or "none")
- `${legacyWikiMode}` = "migrate" | "none"

#### Phase 3: Handoff
Pass `${mode}` and `${legacyWikiPath}` to `repository-analyzer`.

### Legacy Wiki Migration Flow

When `${legacyWikiPath}` is not "none":

```
Orchestrator
    │
    ▼
Repository Analyzer
    │ (includes wiki content in analysis)
    ▼
Wiki Migration Analyzer ← Receives analysis_report.md
    │ (validates wiki content, creates migration plan)
    ▼
Documentation Generator ← Receives both reports
    │ (integrates migrated content into WIKI/)
    ▼
Complete
```

### Output Summary

After orchestration, the following should exist:
- `output/reports/analysis_report.md` - Technical analysis
- `output/reports/wiki_migration_report.md` - Wiki migration plan (if legacy wiki found)
- `output/README.md` - Generated README
- `output/WIKI/` - Populated wiki with migrated content
- `output/TODO.md` - Documentation gaps and action items

