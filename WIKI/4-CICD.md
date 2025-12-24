# 4. CICD

## 4.1 Github Actions
**Context:** Workflow automation.

| Workflow | Status | File | Purpose | Parameters |
| -------- | ------ | ---- | ------- | ---------- |
| [Name] | [available / in-progress / not-available] | `.github/workflows/[file].yml` | [Description] | `[inputs.name]` |

## 4.2 Azure Key Vaults
**Context:** Vaults accessed during the build process.

- **Dev Vault:** [Link]
- **Prod Vault:** [Link]

## 4.3 Azure Keyvault Secrets
**Context:** Secrets management mapping.

| Secret Name | Key Vault | Usage & Purpose |
| ----------- | --------- | --------------- |
| `[secret-name]` | `[vault-name]` | **Purpose:** ... <br> **Rotation:** [Auto/Manual] |

## 4.4 Repository Variables
**Context:** CICD and Repo-level secrets/vars.

| Variable Name | Scope | Purpose |
| ------------- | ----- | ------- |
| `[VAR_NAME]` | `[Repo/Env]` | [Description] |

## 4.5 Deployment Procedures
**Context:** How to ship code.

1. **L2 (Dev):** [Automatic/Manual trigger]
2. **L4 (Stage):** [Promotion process]
3. **PROD:** [Approval gates & execution]

## 4.6 Jenkins
**Context:** Legacy or current build pipelines.

| Pipeline | Purpose | Triggers | Parameters |
| -------- | ------- | -------- | ---------- |
| [Job Name] | [Description] | [Commit/Schedule] | `[Param: Value]` |
