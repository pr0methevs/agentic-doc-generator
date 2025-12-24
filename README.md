# Agentic Documentation Generation Process

## Executive Summary

This project implements an **Agentic Documentation Swarm**—a coordinated team of specialized AI agents designed to treat documentation as code. By automating the extraction, validation, and generation of technical documentation, we ensure that your `README.md` and Wiki remain "living documents" that accurately reflect the current state of your codebase.

**Value Proposition for IT Leaders:**
*   **Consistency:** Removes human error and stylistic variance from technical docs.
*   **Speed:** Generates comprehensive documentation suites in minutes, not days.
*   **Separation of Concerns:** Distinct agents handle fact-gathering (Forensics) versus presentation (DX), ensuring technical accuracy without sacrificing readability.
*   **Standardization:** Enforces strict templates (Conventional Commits, standardized READMEs) automatically.

---

## 2. High-Level Workflow

The process is orchestrated by a central manager agent that dispatches specialized workers in a strict linear pipeline. This ensures that downstream agents always have validated context from upstream analysis.

```mermaid
    graph TD
    %% Theme Definitions - Nordic Slate
    classDef manager fill:#2c323a,stroke:#62aeb7,stroke-width:3px,color:#f4f7f6
    classDef worker fill:#395671,stroke:#f4f7f6,stroke-width:2px,color:#f4f7f6
    classDef artifact fill:#f4f7f6,stroke:#748590,stroke-width:2px,stroke-dasharray: 5 5,color:#2c323a
    classDef user fill:#62aeb7,stroke:#fff,stroke-width:2px,color:#fff
    linkStyle default stroke:#748590,stroke-width:2px

    User((User)) -->|Triggers| Orch["**Readme Orchestrator**<br/>(Manager)"]
    
    subgraph "Phase 1: Context & Fact Finding"
        direction TB
        Orch -->|Handoff| Forensics["**Forensics Engineer**<br/>(Analyst)"]
        Forensics -->|Generates| Brief[Technical Brief]
    end

    subgraph "Phase 2: Validation"
        direction TB
        Brief --> QA["**Quality Analyst**<br/>(Auditor)"]
        QA -->|Generates| Report[Validation Report]
    end

    subgraph "Phase 3: Execution & Generation"
        direction TB
        Report --> DX["**DX Architect**<br/>(Writer)"]
        DX -->|Generates| README[output/README.md]
        DX -->|Generates| TODO[output/TODO.md]
        
        README --> WikiExp["**Wiki Content Expander**<br/>(Tech Writer)"]
        Brief --> WikiExp
        WikiExp -->|Populates| Wiki[output/WIKI/*.md]
    end

    %% Apply Styles
    class Orch manager
    class Forensics,QA,DX,WikiExp worker
    class Brief,Report,README,TODO,Wiki artifact
    class User user
    
    %% Global Styling
    linkStyle default stroke:#7e8590,stroke-width:1px
```

### Initial Prompt
```
@readme-orchestrator Initialize the documentation generation workflow. 
1. Create the `output/` directories.
2. Analyze the repository to determine if we are in "Greenfield" (New) or "Brownfield" (Migration) mode.
3. Hand off the technical analysis to the @readme-forensics-engineer.
```

---

## 3. The Agent Squad

Each agent in this pipeline mimics a specific real-world role within a software development team.

### 1. `readme-orchestrator` (The Project Manager)
*   **Role:** Workflow orchestration and state management.
*   **Responsibility:**
    *   Initializes the `output/` workspaces.
    *   Determines if the project is in "Greenfield" (Generation) or "Brownfield" (Migration) mode.
    *   Manages handoffs between agents to prevent context loss.

### 2. `readme-forensics-engineer` (The Systems Analyst)
*   **Role:** Deep code analysis and fact extraction.
*   **Responsibility:**
    *   Scans the entire repository to understand the tech stack, implementation details, and hidden logic.
    *   **Output:** `output/reports/technical_brief.md` (Raw, unstructured technical facts).
    *   *Note: This agent does not write user-facing text; it only extracts truth.*

### 3. `readme-quality-analyst` (The Auditor)
*   **Role:** Verification and gap analysis.
*   **Responsibility:**
    *   Reviews the `technical_brief.md` against the codebase to ensure no hallucinations.
    *   Identifies missing sections or ambitious claims.
    *   **Output:** `output/reports/validation_report.md` (A "pass/fail" report for the brief).

### 4. `readme-dx-architect` (The Technical Writer co. "DevRel")
*   **Role:** Synthesis and user-facing documentation.
*   **Responsibility:**
    *   Consumes the validated facts.
    *   Applies the `README_TEMPLATE.md` to ensure consistent formatting.
    *   Writes the "Selling Pitch" and "Getting Started" guides.
    *   **Output:** `output/README.md` and `output/TODO.md`.

### 5. `wiki-content-expander` (The Operations Specialist)
*   **Role:** Detailed operational documentation.
*   **Responsibility:**
    *   Takes the high-level concepts from the README.
    *   Expands them into deep-dive articles in the `WIKI/` directory.
    *   Fills in structure templates with specific configuration, API details, and deployment steps.
    *   **Output:** Fully populated `output/WIKI/` directory (e.g., `1.1-System-Overview.md`, `output/WIKI/4.1-API-Endpoints.md`).

---

## 4. Data Flow Architecture

The system relies on a **"Context Waterfall"** approach where information is refined at each step.

```mermaid
sequenceDiagram
    %% Nordic Slate Theme Config
    %%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#395671', 'primaryTextColor': '#f4f7f6', 'edgeLabelBackground':'#2c323a', 'actorBorder': '#62aeb7', 'actorBkg': '#2c323a', 'signalColor': '#748590', 'signalTextColor': '#f4f7f6', 'textColor': '#f4f7f6', 'mainBkg': '#2c323a', 'sequenceNumberColor': '#62aeb7', 'activationBorderColor': '#62aeb7'}}}%%
    
    participant Repo as Codebase
    participant Forensics as Forensics Agent
    participant Context as output/reports/
    participant DX as DX Architect Agent
    participant Docs as Final Docs

    Note over Forensics: Phase 1: Exploration
    Forensics->>Repo: Read Files & Structure
    Forensics->>Context: Write technical_brief.md
    
    Note over DX: Phase 2: Synthesis
    DX->>Context: Read technical_brief.md
    DX->>Context: Read validation_report.md
    DX->>Docs: Generate README.md
    
    Note over DX, Docs: Phase 3: Expansion
    DX->>Docs: Read README.md (Source of Truth)
    DX->>Docs: Populate WIKI/ templates
```

---

## 5. Technical Implementation Details

*   **Context Storage:** detailed reports are stored in `output/reports/`. This allow agents to "pass the baton" without needing massive context windows to remember the entire conversation history.
*   **Idempotency:** The Wiki Expander is designed to be safe to run multiple times; it looks for placeholders to fill rather than overwriting custom changes.
*   **Templates:**
    *   `README_TEMPLATE.md`: Enforces structure for the main entry point.
    *   `WIKI_TEMPLATE.md`: Defines the schema for the detailed documentation.
