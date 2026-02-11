# Methodology & Process: Spec-Driven Rigor

This document defines the development lifecycle and the rigorous tracking system used to ensure high-fidelity software delivery, especially when augmented by AI.

## 1. Initial Architecture Pass

Before implementation begins, we perform a standardized **Initial Architecture Pass** to ensure the stack matches the project's requirements.

### 🖼️ At-a-Glance Process
1.  **Requirement Analysis:** Identify sub-domains (e.g., Public UI, Admin Tool, Core Engine).
2.  **Visual Selection:** Use the decision trees in `STACK.md` to map technologies to sub-domains.
3.  **Form Completion:** Fill out the `ARCH_SELECTION_FORM.md` template.
    *   *Default-First:* Start with the recommended "Gold Standard" selections.
    *   *Override with Care:* Only change selections if the domain specifically demands it.
4.  **ADR Creation:** For any non-standard or "Hybrid" architectural choices, record an Architectural Decision Record (ADR).

---

## 2. User Story Catalog: The Master Proof

To ensure every requirement is met and verified, we maintain a permanent **User Story Catalog** (using [USER_STORY_CATALOG_TEMPLATE.md](./templates/USER_STORY_CATALOG_TEMPLATE.md)).

*   **Dual-Layer Verification:** Every story must be proven twice:
    1.  **Backend Logic:** Verified via Table-Driven Tests (TDT).
    2.  **User Experience:** Verified via Playwright UI flows.
*   **Centralized Traceability:** The catalog links the User Story to its Technical Spec, its code implementation, and its multiple test artifacts.
*   **Auditability:** This document proves that the application does exactly what it was specified to do, with no untested edge cases.

---

## 3. Spec-Driven Development (SDD)

We never implement logic without a specification. The **Spec** is the "Prompt" for the AI and the "Source of Truth" for the developer.

### ⛓️ The Chain of Truth

1.  **User Story:** Defines the user need (`tracking/user_stories.md`).
2.  **Technical Spec:** Defines the interface, logic, and edge cases (`docs/specs/`).
3.  **Table-Driven Test:** Translates the spec's scenarios into executable code.
4.  **Implementation:** The code that makes the test pass.

---

## 2. Hyper-Linked Traceability (The "Ref" System)

To avoid "Document Rot," every artifact must link to its neighbors.

*   **Story Ref:** Use `[US-XXX]` in Specs and Trackers.
*   **Spec Ref:** Every task in a Tracker must have a link to a `.md` spec file.
*   **Test Ref:** Every task in a Tracker should point to its corresponding `_test.go` file.
*   **Code Refs:** Use comments to link complex logic back to specific Spec sections.

---

## 3. Planning & Tracking Hierarchy

We manage projects across three levels of zoom:

| Level | Document | Frequency | Audience |
| :--- | :--- | :--- | :--- |
| **Strategy** | `MASTER_PLAN.md` | Monthly | Stakeholders |
| **Tactics** | `phaseX_plan.md` | Bi-Weekly | Architects |
| **Execution** | `phaseX_tracker.md` | Daily | Developers / AI |

### Git Discipline: Commit & Push 🚀
Every Phase Plan must include explicit checkpoints for commits.
*   *Rule:* Commit whenever a Spec is approved.
*   *Rule:* Commit whenever a TDT goes "Green."
*   *Benefit:* Small, atomic commits make rollbacks trivial and provide a perfect training set for future AI agents.

---

## 4. Documentation as Code (MermaidJS)

We treat diagrams as first-class citizens. If it's not in Mermaid, it doesn't exist.

*   **Gantt:** Use in `MASTER_TRACKER.md` to visualize phase overlaps.
*   **Sequence:** Use in `Specs` to clarify interactions between agents.
*   **State:** Use in `Design Docs` to show state transitions (e.g., `Draft -> Refined -> Published`).
*   **Mindmap:** Use for brainstorming new features or "Kit" outlines.

---

## 5. ADRs (Architectural Decision Records)

When a significant technical choice is made (e.g., "Why we chose IndexedDB over LocalStorage"), it must be recorded as an ADR in `docs/design/adr/`.

*   **Format:** Context -> Options -> Decision -> Consequences.
*   **Persistence:** ADRs provide the "Why" long after the original developer has moved on.
