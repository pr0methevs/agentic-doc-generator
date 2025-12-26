# 1. Architecture

## 1.1 System Overview & Diagrams
**Context:** High-level design and system boundaries.

- **Pattern:** [e.g., Microservice, Monolith, Event-Driven]
- **Description:** [3-5 sentences describing the system's purpose and high-level architecture.]

**Diagrams:**
- **External:** [Link to Visio/SharePoint C4 Context/Container Diagram]
- **Agent Generated:**
```mermaid
%% Insert Mermaid C4 or Flowchart here
```

## 1.2 Component Deep Dives
**Context:** Detailed explanation of core subsystems.

### [Component Name]
- **Responsibility:** [What does this component do?]
- **Tech Stack:** [Languages/Frameworks]
- **Key Interactions:** [Upstream/Downstream dependencies]

## 1.3 Data Models & Flows
**Context:** Core entities and critical business processes.

- **ERD:**
    - **External:** [Link to Visio/SharePoint ERD]
    - **Agent Generated:**
    ```mermaid
    erDiagram
        %% Insert Mermaid ERD here
    ```
- **Critical Flows:**
    - **[Flow Name]:**
        - [Link to Visio/SharePoint Sequence Diagram]
        - ```mermaid
          sequenceDiagram
              %% Insert Mermaid Sequence Diagram here
          ```

## 1.4 Non-Functional Requirements
**Context:** Performance, security, and scalability targets.

| Category | Requirement | Target |
| -- | -- | -- |
| **Performance** | API Response Time (95th) | `< 200ms` |
| **Scalability** | Concurrent Users | `1000+` |
| **Availability** | Uptime SLA | `99.9%` |

## 1.5 Stakeholder Contacts & SLAs
**Context:** Who owns what.

| Role | Name | Contact |
| -- | -- | -- |
| **Product Manager** | [Name] | [Email/Slack] |
| **Architect** | [Name] | [Email/Slack] |
| **Support Team(s)** | [Team Name] | [Channel] |
