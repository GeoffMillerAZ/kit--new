# Quality Assurance: The "Gold Standard"

This document defines our rigorous standards for testing and verification, ensuring that our software is correct, maintainable, and resilient.

## 1. Test-Driven Development (TDD)

We follow the classic **Red-Green-Refactor** loop, strictly enforced by the SDD process.

1.  **Red:** Write a Table-Driven Test (TDT) that implements the scenarios defined in the Spec. It must fail.
2.  **Green:** Write the minimal implementation to satisfy the test.
3.  **Refactor:** Clean up the implementation while keeping the tests passing.

---

## 2. Table-Driven Tests (TDT)

TDT is our standard for all backend logic. It allows us to test complex permutations with minimal code duplication.

### Example Pattern:
```go
func TestService_Action(t *testing.T) {
    tests := []struct {
        name    string
        input   Input
        want    Output
        wantErr bool
    }{
        {"Success Case", validIn, validOut, false},
        {"Error Case", invalidIn, nil, true},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := service.Action(tt.input)
            // Assertions...
        })
    }
}
```

---

## 3. Data Fixtures: Hierarchical & Composable

We avoid brittle, flat JSON blobs. Instead, we use a **Hierarchical Fixture Catalog** powered by Cuelang.

*   **Compositional Logic:** Start with a `#BaseData` (Happy Path) fixture. Create specific scenarios by **patching** the base with variations (e.g., `#BaseData & { status: "expired" }`).
*   **Hierarchical Organization:** Fixtures are organized by domain and scenario, allowing developers to import and extend existing states for complex tests.
*   **Source of Truth:** These fixtures are the "Gold Standard" state for both automated tests and local seeding.

---

## 4. User Story Catalog & UI Verification

To prove the application works, we maintain a **User Story Catalog** as the central artifact for quality.

*   **Dual-Layer Proof:** Every user story must have:
    1.  **Backend Tests (TDT):** Proving the domain logic is correct.
    2.  **UI Tests (Playwright):** Proving the user flow is functional in the browser.
*   **High-Fidelity Documentation:** The catalog serves as executable documentation, proving that the application handles every defined state correctly.
*   **Consistency:** The same hierarchical fixtures used for unit tests must be used for UI verification to ensure the "Chain of Truth" remains unbroken.

---

## 5. UI Testing Strategy

We separate UI testing into two distinct layers:

1.  **Component Logic (Vitest):** Tests React hooks, state management, and utility functions in isolation.
2.  **User Flows (Playwright):** End-to-end (E2E) tests that simulate a real user interacting with the browser. These ensure that the "Glue" between components is working.

---

## 5. Local Prototyping & Mocking

To maintain high development velocity, we use **Memory Adapters** and **Mocks**.

*   **Mock Early:** If the database or AI API is not ready, implement a `MemoryAdapter` that satisfies the Port interface.
*   **Mock Often:** Unit tests for Core Services should *always* use mocks for their dependencies (Adapters) to ensure isolation and speed.
*   **Dependency Injection:** This is only possible because we strictly follow Hexagonal Architecture and never use global state.

---

## 6. Performance Standards

Quality includes performance. For public-facing web applications, we adhere to strict performance budgets.

*   **Lighthouse Score:** Target **99/100** for Performance on static content (blogs, marketing pages).
*   **Core Web Vitals:** Must pass all Core Web Vitals (LCP, FID, CLS).
*   **Bundle Analysis:** Use `@next/bundle-analyzer` to ensure no accidental bloat.

---

## 7. Automated Quality Gates (CI)

We do not rely on "Good Intentions." Standards are enforced via the CI pipeline.

*   **Zero-Failure Linting:** `golangci-lint` and `eslint` must pass on every PR.
*   **Coverage Thresholds:** Automated tests must maintain a minimum coverage (e.g., 80%) on new code.
*   **E2E Mandatory:** Playwright flows for every story in the catalog must pass before merging.
*   **The "Two-Key" Rule:** A PR cannot be merged without:
    1.  **Spec Approval:** An architect confirms the implementation matches the `docs/specs/`.
    2.  **Test Proof:** The `User Story Catalog` shows green for both Backend and UI tests.

---

## 8. Visual Regression & Snapshots

To prevent "silent" UI breakage (CSS leaks, layout shifts), we use **Visual Snapshot Testing**.

*   **Golden Snapshots:** Playwright takes snapshots of critical UI components seeded with the **Hierarchical Fixture Catalog**.
*   **Regression Detection:** Any pixel-level deviation triggers a failure, requiring a deliberate "Snapshot Update" or a fix.
*   **State-Driven:** We test visual states for every scenario (e.g., Error State, Loading State, Success State) defined in the Spec.
