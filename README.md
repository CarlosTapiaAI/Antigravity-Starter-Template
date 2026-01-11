# 🚀 Antigravity Development Playbook: Feature-Pod Edition

This repository is optimized for **Google Antigravity** orchestration. It utilizes a 3-Layer Agent Architecture to separate probabilistic AI reasoning from deterministic application execution.

---

## 🏗 Project Architecture

We use a **Feature-Pod** structure to maximize parallel agent efficiency and minimize context bleed between Web, Mobile, and Backend layers.

### Directory Structure
- **`/apps/web`**: Next.js (App Router) - The web interface.
- **`/apps/mobile`**: Expo (React Native) - The mobile interface.
- **`/features/[name]`**: The "Pod." Contains feature-specific UI components, API hooks, and TypeScript definitions shared between apps.
- **`/supabase`**: Database migrations, RLS policies, and Edge Functions (The Backend).
- **`.antigravity/directives`**: SOPs that guide agent behavior.
- **`execution/`**: Deterministic scripts for automated tasks (e.g., migrations, scraping).

---

## 🤖 The 3-Layer Agent Framework

To ensure 100% reliability, all Antigravity agents must operate within these three layers:

1. **Layer 1: Directive (The SOPs)**
   - Markdown files in `.antigravity/directives/` that define "What" to do.
   - Includes inputs, goals, and expected outputs.
2. **Layer 2: Orchestration (The Brain)**
   - The Antigravity Agent itself.
   - It reads directives, calls tools, and updates documentation based on findings.
3. **Layer 3: Execution (The Tools)**
   - Deterministic scripts (Python/TypeScript) in `execution/` or Supabase CLI commands.
   - Environment variables are stored securely in `.env`.

---

## 📝 Prompting Templates

Use these templates in the **Antigravity Manager View** to initialize parallel work streams.

### 🌐 Web Application Feature Prompt
> "Using the **Feature-Pod Architecture**, implement the `[Feature Name]` for the **Web app**. 
> 1. Read the directive at `.antigravity/directives/[feature].md`.
> 2. Create the pod in `/features/[feature-name]`.
> 3. Build the UI in `/apps/web` using Shadcn/UI.
> 4. Ensure API interactions are isolated in `/features/[feature-name]/api.ts`."

**Example:** "Build the TCG Collection View. Ensure the grid is responsive and fetches data from the `inventory` table via Supabase."

### 📱 Mobile Application Feature Prompt
> "Using the **Feature-Pod Architecture**, implement the `[Feature Name]` for the **Mobile app** in `/apps/mobile`.
> 1. Reuse the logic and types from `/features/[feature-name]`.
> 2. Use NativeWind for styling to maintain design parity with Web.
> 3. Create a **Browser Recording** artifact showing the mobile navigation flow."

**Example:** "Build the Card Scanner interface. Integrate with the Expo Camera and trigger the `process-card` Edge Function."

---

## 🛠 Operating Principles

- **Check for tools first**: Before generating new logic, check the `execution/` directory for existing scripts.
- **Self-Annealing**: If an agent hits an error (e.g., Supabase RLS failure), it must fix the script, update the migration, and document the learning in the directive.
- **Artifact-First**: No code is merged without an **Implementation Plan** and a **Validation Artifact** (Screenshot/Video).
- **Cloud Deliverables**: Local files in `.tmp/` are for processing; all final data must be synced to the database or cloud storage.

---

## 🛤 Feature Roadmap (Parallel Execution)

| Agent Role | Primary Directory | Responsibility |
| :--- | :--- | :--- |
| **Architect** | `/supabase` | Database Schema, RLS, & Edge Functions. |
| **Web Dev** | `/apps/web` | Next.js Page layouts & Component wiring. |
| **Mobile Dev** | `/apps/mobile` | Expo screens & Native hardware integration. |
| **QA/Validator**| `.tmp/` | Browser recordings & Unit test execution. |