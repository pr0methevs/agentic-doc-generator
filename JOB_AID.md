# Job Aid: Agentic Documentation Generator Workflow

This job aid outlines the steps to set up and execute the agentic documentation generation workflow for your application.

## 1. Request GitHub Copilot License

Ensure you have the necessary access by requesting a license.

[GitHub Copilot License Request]()

## 2. Application Setup

1.  **Clone the Repository**: Clone your target application repository locally.
    ```bash
    git clone <your-repo-url>
    ```
2.  **Navigate directly**: Change into the project directory.
    ```bash
    cd <your-project-directory>
    ```
3.  **Add Tooling**: Add the `agentic-doc-generator` folder to the root of your project.

## 3. Agent Configuration

1.  Locate the `agents` directory within the `agentic-doc-generator` folder.
2.  Move or copy the `agents` directory into your project's `.github` folder.
    *   *Path check*: `.github/agents/`

## 4. Execution Workflow

To initiate the agentic swarm workflow, use the following prompt and reference the `readme-orchestrator` agent.

### Initial Prompt
Call the `readme-orchestrator` agent with the following prompt:

```markdown
@readme-orchestrator Initialize the documentation generation workflow. 
1. Create the `output/` directories.
2. Analyze the repository to determine if we are in "Greenfield" (New) or "Brownfield" (Migration) mode.
3. Hand off the technical analysis to the @[agents/readme-forensics-engineer.agent.md] 
```

## 5. Review Generated Content
Once the documentation generation is complete, check the `TODO.md` at a high level. Then, review the generated content within the `/output` directory to validate for correctness.

## 6. Wiki Deployment
Take **ALL** the contents of the `/WIKI` directory and place them in the corresponding repository's Wiki.
- Except the `AGENTS.md` file.

## 7. Cleanup
Remove **everything** that came with this workflow (the `agentic-doc-generator` tooling), leaving only the generated `README.md`.

