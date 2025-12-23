---
created_dt: 2025-12-21
tags:
links:
external sources:
cssclasses:
---
Use the README as the single-page “front door” to the repo (overview + quickstart), and use the wiki for deeper, evolving documentation such as architecture, runbooks, and business/process context.

## Core split: README vs wiki

- README
    - Purpose: Help someone quickly understand what this repo is, whether it’s relevant, and how to start using or contributing to it.
    - Scope: Short, opinionated, and task‑oriented (install, run, basic usage, contribution entry points).
- Wiki
    - Purpose: Act as a structured knowledge base/manual for the system: detailed docs, decisions, and processes that don’t fit cleanly in a single page.
    - Scope: Longer-form, navigable documentation (multiple pages, cross‑linking), suitable for onboarding and ongoing reference.
        

## What goes in the README

Aim for a single, well-structured markdown page that is readable by both engineers and business stakeholders at the top, and more technical further down.

Recommended sections:
- Project name and one‑line tagline
    - Clear, concise statement of what this repo is and who it’s for.
	
- High‑level overview (for all audiences, incl. business)
    - 2–4 sentences or a few bullets describing: what the system does, the main value it provides, and key users or use cases.
	
- Status and links
    - Repo status (active/maintenance/deprecated), primary contact or owning team, and links to: wiki home, issue tracker, production environment, and monitoring dashboards as needed.
        
- Getting started (for engineers)
    - Prerequisites and system requirements (languages, runtimes, services).
    - How to set up a local dev environment (clone, install dependencies, configure env vars, run migrations, start services).
    - How to run the test suite and basic tooling commands (lint, format, build).
        
- Basic usage examples
    - Minimal examples: API endpoints, CLI commands, or UI flows that prove the system works locally or in a sandbox

- Contribution & governance pointers
    - Short contribution blurb with links to: CONTRIBUTING.md, CODE_OF_CONDUCT, release process, branching strategy (details live in wiki or docs/ when longer).
        
- License and credits
    - License identifier and link to LICENSE file; optional brief acknowledgments or key third‑party dependencies.
        

Anything that starts to make the README long or scroll-heavy (e.g., lots of screenshots, edge‑case docs, big API tables) should be summarized and moved to the wiki.

## What goes in the wiki

Use the wiki as the “documentation site” attached to the repo, organized into multiple pages with a clear navigation.

Typical content:

- Architecture and design
    - System architecture diagrams, data flows, key components and their responsibilities, integration points, and external dependencies.
    - Design rationales (ADR-style pages), trade‑offs, and non‑functional requirements.
        
- Detailed technical docs
    - API reference pages, configuration matrices, deployment topologies, environment-specific differences, and feature flags.
    - Performance characteristics, scaling limits, security considerations, and compliance notes.
        
- Runbooks and operations
    - Incident response guides, common failure modes, troubleshooting steps, and known issues.
    - Operational checklists: deployments, rollbacks, data migrations, DR procedures.
	
- Onboarding and workflows (good for both engineers and business)
    - “How this system fits in the wider product,” domain glossary, and business processes supported by this repo.
    - Team workflows: how to create features, how to request changes, release calendar, and stakeholder contacts.
        
- Extended guides and FAQs
    - Advanced usage, integration how‑tos, example configurations, and “recipes” that would clutter the README.
    - FAQ aimed at support/business (common questions, limitations, SLAs).
        

## Quick decision guide

Use this as a policy statement you can share with the team:
- Put it in the README if:
    - Someone new must read it in the first 5–10 minutes to understand or run the project.
    - It is short, essential, and directly tied to cloning, building, running, or lightly evaluating the repo.
- Put it in the wiki if:
    - It needs more than a few paragraphs or a dedicated page (architecture, runbooks, business process docs).
    - It is reference material that people will revisit, maintain over time, or navigate via a table of contents.
	
### External Sources
- [Github README Best Practices](https://www.hatica.io/blog/best-practices-for-github-readme/)​