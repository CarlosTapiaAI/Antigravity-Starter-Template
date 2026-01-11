# Antigravity Agent Instructions: Feature-Pod Architecture

> **Mirroring Note**: This file provides the operational framework for Antigravity Agents to ensure deterministic, parallel development across Web, Mobile, and Supabase layers.

## The 3-Layer Architecture (Antigravity Optimized)

To maximize reliability in an agent-first environment, all work must follow this separation:

### Layer 1: Directive (The "What" - SOPs)
- **Location**: `.antigravity/directives/`
- **Function**: Standard Operating Procedures (SOPs) for specific app features (e.g., `auth_setup.md`, `tcg_price_sync.md`).
- **Constraint**: Agents must read the corresponding directive before touching code. Directives define the "Vibe," UI standards, and edge cases.

### Layer 2: Orchestration (The "How" - Manager View)
- **Location**: Antigravity Manager / Agent Manager.
- **Function**: This is the AI's core role—routing tasks to specialized sub-agents. 
- **Workflow**: 
    1. Read Directive.
    2. Check for existing "Artifacts" (Design docs/Schemas).
    3. Spawn execution tasks in parallel (e.g., Agent A builds the DB Schema while Agent B scaffolds the UI).
    4. Validate using the **Browser Surface** artifact.

### Layer 3: Execution (The "Work" - Deterministic Tools)
- **Location**: `supabase/functions/`, `shared/scripts/`, and Supabase MCP.
- **Function**: Deterministic TypeScript/SQL/CLI operations.
- **Principle**: Minimize raw "probabilistic" code generation. Use the **Supabase MCP** for DB management and pre-defined component libraries (Shadcn) for UI to ensure consistency.

---

## Operating Principles

### 1. Parallel Feature Isolation
- Agents are assigned to a **Feature Pod** (e.g., `/features/inventory`).
- You are forbidden from modifying files in another pod unless it is a shared utility in `/shared`.
- Use **Cross-Agent Communication** only via the Manager View to sync on breaking changes (e.g., schema updates).

### 2. Artifact-First Development
- Every major change requires an **Implementation Artifact**.
- Use the **Browser Recording** feature to verify UI changes on both Web (Next.js) and Mobile (Expo) viewports before marking a task complete.

### 3. Self-Annealing & Tool Maintenance
- If a Supabase migration fails, read the log, fix the SQL in `supabase/migrations`, and update the `db_directive.md` with the learned constraint.
- If an API rate limit is hit (e.g., TCG market data), rewrite the logic into a **Supabase Edge Function** to handle retries and update the directive.

---

## Directory Structure & Routing

- `.antigravity/directives/` - Feature SOPs and AI instructions.
- `apps/web/` - Next.js frontend (Agent Alpha).
- `apps/mobile/` - Expo/React Native frontend (Agent Beta).
- `features/` - Shared logic, UI components, and API calls grouped by feature.
- `supabase/` - Database migrations and Edge Functions.
- `.tmp/` - Temporary logs and agent-generated dossiers (Git ignored).

---

## Parallel Execution Workflow
When building a new feature:
1. **Agent 1 (Architect)**: Updates `supabase/` schema and generates types via Supabase MCP.
2. **Agent 2 (Frontend)**: Reads types and builds UI in `apps/web` and `apps/mobile` simultaneously.
3. **Agent 3 (Logic)**: Develops the Supabase Edge Functions for complex middleware/API logic.
4. **Final Step**: Verification Agent runs a full-stack test and records a "Validation Artifact."