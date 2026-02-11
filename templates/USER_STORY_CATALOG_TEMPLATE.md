# User Story Catalog: [Project Name]

This catalog serves as the **Master Proof of Correctness** for the application. It tracks every user requirement from its definition through its technical specification to its final verification in both logic and UI.

**Status Legend:** ⚪ Todo | 🟡 In Progress | ✅ Implemented | 🧪 Backend Test Green | 🖥️ UI Test Verified | 🏁 Done

## 📚 The Catalog

| ID | User Story | Spec Ref | Backend Test | UI Test | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **US-101** | As a [persona], I want to [action] so that [value]. | [Spec](./docs/specs/101.md) | [TDT](./path/to_test.go) | [Playwright](./path/to_test.spec.ts) | ⚪ |
| **US-102** | As a [persona], I want to [action] so that [value]. | [Spec](./docs/specs/102.md) | [TDT](./path/to_test.go) | [Playwright](./path/to_test.spec.ts) | ⚪ |

---

## 📈 Coverage Dashboard

- **Total Stories:** 0
- **Implemented:** 0%
- **Logic Verified (Backend):** 0%
- **UI Verified (Playwright):** 0%

## 📝 Catalog Notes
*   *Rule:* A story is not "Done" (🏁) until both the Backend Test and the UI Test are verified against the Spec scenarios.
*   *Traceability:* Ensure all Spec Refs link to the corresponding file in `docs/specs/`.
