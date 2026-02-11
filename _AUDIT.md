# 🔍 Project Audit & Alignment Guide (The "Gold Standard" Gap Analysis)

This guide is designed for **existing projects** that wish to evaluate their current architectural and procedural health against the "Gold Standard" engineering kit. 

The goal of this audit is not to force immediate refactoring, but to identify high-leverage opportunities to increase quality, speed, and AI-readiness.

## 📋 The Audit Workflow

For each major area below, create an **Evaluation Document** (e.g., `docs/audit/eval-hexagonal-arch.md`) that follows this structure:
1.  **Current State:** How do we do this today?
2.  **Reward:** What would we gain by adopting the kit's standard? (e.g., "Reduce bug regressions by 30%")
3.  **Cost/Risk:** What is the effort required to migrate or implement?
4.  **Recommendation:** [Adopt Now | Adopt Incrementally | Do Not Adopt]

---

## 1. Architectural Integrity
*Reference: [ARCHITECTURE.md](./ARCHITECTURE.md)*

- [ ] **Hexagonal Boundary Check:** Does domain logic leak into UI components or database queries?
- [ ] **Dependency Injection:** Are we using global state or `init()` functions instead of explicit wiring?
- [ ] **Port Standards:** Do we have clearly defined interfaces for all infrastructure (Adapters)?

---

## 2. Process & Traceability
*Reference: [METHODOLOGY.md](./METHODOLOGY.md)*

- [ ] **User Story Catalog:** Do we have a master list tracking the implementation and dual-layer verification (Backend + UI) of every story?
- [ ] **Planning & Prioritization:** Are user stories prioritized and mapped to strategic development phases?
- [ ] **Spec-Driven Gap:** Do we have features implemented without corresponding Technical Specs?
- [ ] **Traceability Audit:** Can we link a line of code back to a User Story or Spec?
- [ ] **ADR Presence:** Are our major architectural decisions documented, or are they tribal knowledge?

---

## 3. Configuration & State
*Reference: [CONFIG.md](./CONFIG.md)*

- [ ] **Validation Rigor:** Does the app validate its configuration schema at startup?
- [ ] **Cuelang Migration:** Would moving from JSON/YAML to Cuelang eliminate "magic" strings and configuration errors?
- [ ] **Semantic State:** Is our application state well-defined and constrained, or is it a loose collection of types?

---

## 4. Quality & Testing
*Reference: [QUALITY.md](./QUALITY.md)*

- [ ] **TDT Adoption:** Are we using Table-Driven Tests for complex business logic?
- [ ] **Fixture Composability:** Are our test fixtures flat and repetitive, or are they hierarchical and patched?
- [ ] **User Story Catalog:** Do we have a verified catalog of UI flows that proves the app works?

---

## 5. Developer Experience (DX)
*Reference: [STACK.md](./STACK.md)*

- [ ] **Local Dev/Demo Mode:** Does it take more than 5 minutes to get a seeded, working environment running for a specific role?
- [ ] **SQLite Standard:** Could we replace a heavy local Postgres dependency with a seeded SQLite instance for faster iteration?
- [ ] **Task Automation:** Is our `Taskfile.yml` (or Makefile) comprehensive, or are commands "hidden" in developer history?

---

## 📊 The Recommendation Report

After completing the individual evaluations, synthesize them into a **Master Audit Report** for stakeholders:

| Concept | Impact | Effort | Recommendation |
| :--- | :--- | :--- | :--- |
| **Hexagonal Arch** | High | High | Adopt for new modules only |
| **Cuelang Config** | Med | Low | **Immediate Adoption** |
| **Demo Mode** | High | Med | **Target for Phase 2** |

---

**Next Step:** Create your first evaluation document for the area with the highest perceived technical debt.
