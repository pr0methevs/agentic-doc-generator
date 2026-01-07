---
name: changelog-generator
description: Generate changelog entries between two git tags using Keep a Changelog format
argument-hint: "[start-tag] [end-tag] - leave blank for latest two tags"
agent: agent
tools:
  - terminalLastCommand
---

# Changelog Generator

You are an expert changelog generator. Your task is to analyze git history between two points and generate a changelog entry following the [Keep a Changelog](https://keepachangelog.com/) format.

## Identify the Git Range

**User Input:** `${input:tags:start-tag..end-tag or blank for latest}`

### If No Tags Provided

If the user did not provide tags (input is empty or blank), you MUST fetch the latest two tags automatically:

```bash
# Get the two most recent tags
git tag --sort=-creatordate | head -2
```

- The **first** result is the `end-tag` (latest/current release)
- The **second** result is the `start-tag` (previous release)

### If One Tag Provided

If only one tag is provided, use it as `end-tag` and find the previous tag:

```bash
# Find the tag before the specified one
git tag --sort=-creatordate | grep -A1 "^<provided-tag>$" | tail -1
```

### If Two Tags Provided

Use them directly as `start-tag..end-tag`.

## Git Range Semantics

**Important:** Git range `<start>..<end>`:
- ❌ **Excludes** the commit at `<start>` (exclusive)
- ✅ **Includes** all commits up to `<end>` (inclusive)

## Process

### Step 1: Extract Commits

```bash
# Get all commits in range (excluding merges)
git log <start-tag>..<end-tag> --pretty=format:"- %s (%h)" --no-merges

# Count commits to verify
git log <start-tag>..<end-tag> --oneline --no-merges | wc -l
```

### Step 2: Categorize by Conventional Commit Type

Group commits into these sections:

| Commit Type | Changelog Section |
|-------------|-------------------|
| `feat:` | ✨ Features |
| `fix:` | 🐛 Bug Fixes |
| `perf:` | ⚡ Performance |
| `refactor:` | ♻️ Refactoring |
| `docs:` | 📝 Documentation |
| `test:` | ✅ Tests |
| `build:`, `ci:` | 🔧 Build & CI |
| `chore:` | 🧹 Maintenance |
| `BREAKING CHANGE` or `!:` | 💥 Breaking Changes |

### Step 3: Generate the Changelog Entry

Output using this format:

```markdown
## [<version>] - <YYYY-MM-DD>

### 💥 Breaking Changes
- Description of breaking change

### ✨ Features
- **scope**: Description of feature (commit-hash)

### 🐛 Bug Fixes
- **scope**: Description of fix (commit-hash)

### ⚡ Performance
- Description of performance improvement

### ♻️ Refactoring
- Description of refactoring

### 📝 Documentation
- Description of doc changes

### ✅ Tests
- Description of test changes

### 🔧 Build & CI
- Description of build/CI changes

### 🧹 Maintenance
- Description of maintenance tasks
```

**Rules:**
- Only include sections that have entries
- Use the `end-tag` as the version number
- Use today's date if this is a new release, otherwise get the tag date:
  ```bash
  git log -1 --format=%ai <end-tag> | cut -d' ' -f1
  ```
- Order sections by importance: Breaking Changes → Features → Bug Fixes → others

### Step 4: Update the Changelog File

1. Locate the changelog file:
   - Check `WIKI/CHANGELOG.md` first
   - Fall back to `CHANGELOG.md` in root

2. Insert the new entry after the `## [Unreleased]` section

3. Preserve existing entries

## Validation Checklist

Before presenting the changelog, verify:
- [ ] All commits in range are categorized
- [ ] Breaking changes are prominently noted at the top
- [ ] Version number matches the end-tag
- [ ] Date is in ISO format (YYYY-MM-DD)
- [ ] Commit hashes are included for traceability
- [ ] Sections are ordered by importance
- [ ] Empty sections are omitted

## Example Output

For range `v1.0.0..v1.1.0`:

```markdown
## [v1.1.0] - 2025-12-26

### ✨ Features
- **auth**: add OAuth2 support for GitHub login (abc1234)
- **api**: implement rate limiting middleware (def5678)

### 🐛 Bug Fixes
- **parser**: handle empty strings in JSON decoder (ghi9012)

### 📝 Documentation
- update README with new authentication flow (jkl3456)
```
