# Agent OS

A local-first, self-running framework for creating isolated agent workspaces for businesses.

Each organization gets its own context, prompts, workflow config, integration references, memory, logs, and access rules. SQLite is the source of truth for identity and workspace paths; the file system holds each org's workspace under `/orgs`.

## Architecture

```
/context      global knowledge, policies, playbooks, default rules
/harness      agent execution, workflows, queues, guards, event handling
/model        prompts, agents, schemas, routing, model configs
/runtime      healthcheck, heartbeat, supervisor, retry, recovery
/orgs         isolated business workspaces
/vault        local Obsidian-style markdown knowledge base
/tools        executable agent tools
/integrations provider adapters (GHL, Composio, Mail, Google, Obsidian)
/database     SQLite identity, organization, session, run metadata
/auth         local auth, JWT, password hashing, org access
/scripts      CLI operations
/lib          shared utilities
/types        shared TypeScript types
/docs         documentation
/logs         system logs
/archive      uncertain or deprecated files
```

## What Lives Where

- **Database (SQLite)** — users, authentication, sessions, organizations, memberships, agent run metadata.
- **File system (`/orgs`)** — per-org workspace: context, prompts, workflow config, integration config refs, memory (JSONL), logs.

## Principles

1. Preserve existing working code.
2. Do not delete useful files.
3. Archive uncertain files instead of deleting them.
4. Never use raw org input as a file path.
5. SQLite is the source of truth for organization identity and workspace path.
6. Every organization workspace stays inside `/orgs`.
7. `client-template` is not a real organization.
8. Use JSONL for conversation memory.
9. Redact sensitive data before logs.
10. Do not store secrets in configs.
11. Use `credentialRef` for integration configs.
12. Dev no-auth is only allowed in development.
13. Placeholder responses must not invent pricing, booking, payment, or tool success.
14. Tool permissions must be enforced before tool execution.
15. The MVP must be smoke-testable with one command.

## Build Plan

Agent OS is being built in 30 daily steps. Each day focuses on a single, scoped prompt. The previous `BuildPhase` directory project has been moved to `/archive`.
