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

## 3. Data Fixtures: The Cuelang Advantage

We avoid brittle, giant JSON files for test data. Instead, we use **Compositional Cuelang Fixtures**.

*   **#BaseData:** Define a standard entity.
*   **Mixins:** Define variations (e.g., `#BannedUser`, `#PremiumUser`).
*   **Unification:** In your test, unify the base with a mixin to create the exact state needed for a scenario.
*   **Dryness:** This ensures that if the schema changes, we update it in one place, and all test fixtures are automatically updated.

---

## 4. UI Testing Strategy

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
