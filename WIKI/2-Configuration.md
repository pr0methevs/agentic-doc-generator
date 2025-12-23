# 2. Configuration

## 2.1 Envirnonment Variables
**Context:** App-level settings found in code/manifests.

| Variable | Description | Required | Default | Example |
| -------- | ----------- | -------- | ------- | ------- |
| `[VAR_NAME]` | `[Purpose]` | Yes/No | `[value]` | `[example]` |

## 2.2 Configuration Files
**Context:** External config maps or property files.

- **File:** `[path/to/config.yml]`
- **Purpose:** [What this dictates]
- **Differences:** [Dev vs Prod differences]

## 2.3 Feature Flags
**Context:** Toggles for feature management.

| Flag Name | Type | Purpose & Behavior | Context |
| --------- | ---- | ------------------ | ------- |
| `[flag_name]` | `[Boolean]` | **Purpose:** ... <br> **Behavior:** ... | `[Code Ref]` |
