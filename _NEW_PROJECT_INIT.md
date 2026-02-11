# 🚀 New Project Initialization Guide (The "Gold Standard" Startup)

Welcome to the start of your new project. This guide is the **Master Entry Point** for applying the "Gold Standard" engineering principles. Following this ensures your project is structured for high-fidelity implementation, AI-augmented speed, and long-term maintainability.

## 🧭 The Path to Implementation

1.  **[Stage 1: Design Clarification](#stage-1-design-clarification)**
2.  **[Stage 2: Architecture & Stack Selection](#stage-2-architecture-and-stack-selection)**
3.  **[Stage 3: Strategic Planning](#stage-3-strategic-planning)**
4.  **[Stage 4: Execution & Tracking](#stage-4-execution-and-tracking)**

---

## Stage 1: Design Clarification
*Reference: [METHODOLOGY.md](./METHODOLOGY.md) (Spec-Driven Development)*

Before a single line of code is written, we must define the **Intent**.

- [ ] **Initialize User Story Catalog:** Copy [USER_STORY_CATALOG_TEMPLATE.md](./templates/USER_STORY_CATALOG_TEMPLATE.md) to `docs/tracking/user_story_catalog.md`.
- [ ] **Define User Stories:** Identify the core personas and their primary goals.
- [ ] **Draft Technical Specs:** For every major feature, create a spec using the [SPEC_TEMPLATE.md](./templates/SPEC_TEMPLATE.md).
    - *Rigor Check:* Does the spec include the "happy path" and edge cases?
    - *Reference:* See [ARCHITECTURE.md](./ARCHITECTURE.md) for how to define Ports as contracts within these specs.

---

## Stage 2: Architecture and Stack Selection
*Reference: [STACK.md](./STACK.md) & [CONFIG.md](./CONFIG.md)*

We use a visual, at-a-glance process to select the "Best of Breed" tools for your specific domain.

- [ ] **Initialize the Selection Form:** Copy [ARCH_SELECTION_FORM.md](./templates/ARCH_SELECTION_FORM.md) to your project root.
- [ ] **Analyze Sub-Domains:** Use the **Decision Trees** in [STACK.md](./STACK.md) to pick:
    - **Frontend:** Next.js (SEO), Datastar (Real-time), or Vite (Local)?
    - **Backend:** Standard CRUD or Event Sourcing/CQRS?
- [ ] **Define Semantic State:** Use Cuelang to define your initial data schemas in `configs/schema/`.
- [ ] **Standardize the Environment:** Set up your `Taskfile.yml` and `docker-compose.yml` to mirror the [STACK.md](./STACK.md) requirements.

---

## Stage 3: Strategic Planning
*Reference: [METHODOLOGY.md](./METHODOLOGY.md) (Planning Hierarchy)*

Transition from "What" to "How" and "When".

- [ ] **Create the Master Plan:** Use the [PLAN_TEMPLATE.md](./templates/PLAN_TEMPLATE.md) to define the strategic phases of the project.
- [ ] **Establish Traceability:** Every phase must link back to a User Story and forward to a Technical Spec.
- [ ] **Define Verification Standards:** Reference [QUALITY.md](./QUALITY.md) to plan your testing strategy (Table-Driven Tests + Playwright flows).

---

## Stage 4: Execution and Tracking
*Reference: [QUALITY.md](./QUALITY.md) & [OUTLINE.md](./OUTLINE.md)*

Maintain rigor during the build phase.

- [ ] **Initialize Phase Trackers:** For the current phase, create a tracker using the [TRACKER_TEMPLATE.md](./templates/TRACKER_TEMPLATE.md).
- [ ] **The "Red-Green-Refactor" Loop:**
    1.  **Red:** Write a Table-Driven Test (TDT) based on the spec.
    2.  **Green:** Implement logic to satisfy the test.
    3.  **Refactor:** Clean up while maintaining green status.
- [ ] **Build the Fixture Catalog:** Create hierarchical, composable fixtures in Cuelang as defined in [QUALITY.md](./QUALITY.md).
- [ ] **Verify in Demo Mode:** Ensure the app functions in `demo` mode with Role Selection and SQLite seeding as described in [STACK.md](./STACK.md).

---

## 🛠️ Essential Tools Reminder
*   **Design Inspiration:** Always check the **TailwindPlus MCP Server** first.
*   **Diagramming:** Use MermaidJS within your docs (see [METHODOLOGY.md](./METHODOLOGY.md) for patterns).
*   **Decisions:** Record any deviations from these standards in `docs/design/adr/` using the [ADR_TEMPLATE.md](./templates/ADR_TEMPLATE.md).

---

**Next Step:** Copy this guide to your new repository and check off the first item in **Stage 1**.
