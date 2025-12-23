# 6. Dependencies - Integration - API

## 6.1 Related Repositories - Upstream / Downstream services Integration Points
**Context:** Upstream producers and downstream consumers.

- **Upstream:** `[Repo A]` (Provides X)
- **Downstream:** `[Repo B]` (Consumes Y)

## 6.2 Endpoints
**Context:** Exposed API surface.

| Method | Component | Path | Purpose |
| -- | -- | -- | -- |
| `GET` | `[Service]` | `/api/v1/[resource]` | [Description] |
| `POST` | `[Service]` | `/api/v1/[resource]` | [Description] |

## 6.3 JMS
**Context:** Async constraints.

| Resource | Type | Producer | Consumer | Purpose |
| -------- | ---- | -------- | -------- | ------- |
| `[Topic]` | `[Topic/Queue]` | `[Service A]` | `[Service B]` | [Event Description] |
