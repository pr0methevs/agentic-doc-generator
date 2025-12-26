# Job Aid: Agentic Documentation Generator Workflow

Use this guide to set up and run the current 3-agent documentation workflow with the updated directory layout.

## 1. Prerequisites

### Copilot License
Ensure you have the necessary access by requesting a license.
> [GitHub Copilot License Request](https://myfedex.sharepoint.com/sites/EnterpriseApplicationArchitecture/SitePages/GitHub-Copilot.aspx)
- Follow "Getting Started - Request a License"

### IDE Setup
Ensure Visual Studio Code + Copilot
> [Download Visual Studio Code](https://code.visualstudio.com/download)

## 2. Application Setup

1. **Clone your target repository** locally.
   ```bash
   git clone <your-repo-url>
   cd <your-project-directory>
   ```

2. **Copy the agents folder** from `agentic-doc-generator/.github/agents/` into your repo's `.github/agents/` directory.
   - Create `.github/agents/` in your repo if it does not exist.
   - Copy all agent files (`.agent.md`) including the `archive/` subfolder.
   ```bash
   mkdir -p .github/agents
   cp -r <path-to-agentic-doc-generator>/.github/agents/* .github/agents/
   ```

3. **Copy the WIKI folder** from `agentic-doc-generator/WIKI/` to your project root.
   ```bash
   cp -r <path-to-agentic-doc-generator>/WIKI ./WIKI
   ```

4. **Copy the templates folder** from `agentic-doc-generator/templates/` to your project root.
   ```bash
   cp -r <path-to-agentic-doc-generator>/templates ./templates
   ```

5. Open your project in VS Code and confirm the following structure exists:
   ```
   <your-repo>/
   ├── .github/
   │   └── agents/
   │       ├── readme-orchestrator.agent.md
   │       ├── repository-analyzer.agent.md
   │       ├── documentation-generator.agent.md
   │       └── archive/
   ├── templates/
   │   ├── README_TEMPLATE.md
   │   ├── TODO_TEMPLATE.md
   │   └── WIKI_TEMPLATE.md
   └── WIKI/
       ├── Home.md
       ├── 1-Architecture.md
       └── ...
   ```

## 3. Layout Reference

| Path | Purpose |
|------|---------|
| `.github/agents/` | Core agents: `readme-orchestrator`, `repository-analyzer`, `documentation-generator` (archive of retired agents in `archive/`). |
| `templates/` | Strict templates: `README_TEMPLATE.md`, `TODO_TEMPLATE.md`, `WIKI_TEMPLATE.md`. |
| `WIKI/` | Starter wiki pages; `AGENTS.md` is for reference only. |
| `output/` | Created by the workflow: `reports/analysis_report.md`, `README.md`, `TODO.md`, `WIKI/`. |

## 4. Execution Workflow

Call the `readme-orchestrator` agent with this prompt:
```markdown
@readme-orchestrator Initialize the documentation generation workflow.
1. Create the output/ directories.
2. Analyze the repository to determine if we are in Mode A (README exists) or Mode B (no README).
3. Hand off the technical analysis to the @repository-analyzer.
```

## 5. Review Generated Content
- Validate `output/reports/analysis_report.md` for mode selection and captured facts.
- Review `output/README.md`, `output/TODO.md`, and `output/WIKI/*.md` against the templates.

## 6. Wiki Deployment
Publish the wiki content by copying everything from `output/WIKI/` (or the provided `WIKI/` starter set) into the repository's Wiki. Skip `WIKI/AGENTS.md`—it is informational only.

## 7. Cleanup
After you publish the generated docs, remove the `agentic-doc-generator` tooling if you do not plan to rerun it. Keep the final README and any wiki pages you deployed.
