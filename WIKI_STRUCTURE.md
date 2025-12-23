# Wiki Structure

Use this page tree as the mandatory wiki skeleton
- Each top‑level page is **Required** (1-x)
- Sub‑headings are added per project complexity (1.1 - 1.x)

```
Home (wiki root)
├── 1. Architecture
│   ├── 1.1 System Overview & Diagrams
│   ├── 1.2 Component Deep Dives
│   ├── 1.3 Data Models & Flows
│   ├── 1.4 Non-Functional Requirements
│   └── 1.5 Stakeholder Contacts & SLAs
├── 2. Configuration
│   ├── 2.1 Envirnonment Variables
│   ├── 2.2 Configuration Files
│   ├── 2.3 Feature Flags
├── 3. Testing 
│   ├── 3.1 Isolation / Ephemeral
│   ├── 3.2 Solution / Solution Integration
│   └── 3.3 Manual Test Scenarios
├── 4. CICD
│   ├── 4.1 Github Actions
│   ├── 4.2 Azure Key Vaults
│   ├── 4.3 Azure Keyvault Secrets
│   ├── 4.4 Repository Variables
│   ├── 4.5 Deployment Procedures
│   ├── 4.6 Jenkins
├── 5. Infrastructure
│   └── 5.1 Foundations / Servers
├── 6. Dependencies - Integration - API 
│   ├── 6.1 Related Repositories - Upstream / Downstream services Integration Points
│   ├── 6.2 Endpoints 
│   └── 6.3 JMS
├── 7. Monitoring & Observability
│   ├── 7.1 Application Performance
│   └── 7.2 Logging - Monitoring - Alerts
│   └── 7.3 Usefule Queries - Splunk / DynaTrace
├── 8. Troubleshooting
|   ├── 8.1 Common Issues
|   └── 8.2 Debugging
└── 9. Guides & How‑tos
    ├── 9.1 Documentatiomn
    ├── 9.1 Advanced Usage Recipes
    ├── 9.2 Performance Tuning
    ├── 9.3 Troubleshooting / Known Issues
    └── 9.4 FAQ (engineer & business)
```

## Wiki Page Spec Requirements

**Every wiki page must include:**

- **Title** matching the tree above.
- **Audience** tag (Engineer, Business, All).
- **Table of contents** if page >2 sections.
- **Related pages** links at bottom for navigation.
    

**Page content types:**

- **Concept** – Explain “what” and “why” (e.g., architecture overviews).
- **Task** – Step‑by‑step “how‑to” (e.g., deployment runbook).
- **Reference** – Lookup tables, API details, config matrices.
    

## Wiki Spec Compliance Checklist

- [ ] All top‑level pages exist and are linked from wiki sidebar.
- [ ] No page duplicates README content; README links to wiki for detail.
- [ ] Runbooks include prerequisites, steps, expected output, and rollback plan.
- [ ] Business‑facing pages (6.x) avoid deep technical jargon.