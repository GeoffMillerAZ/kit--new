# Configuration Management: Cuelang-First

This document outlines our strategy for managing application configuration and semantic state using Cuelang (`cue`).

## 1. The "No Viper" Philosophy

We explicitly avoid "magic" configuration libraries like Viper.

*   **Explicit Wiring:** Configuration should be loaded at the entry point and passed down via dependency injection.
*   **No Global State:** We do not allow a global `config.Get()` function.
*   **Compile-Time Verification:** Whenever possible, we use generated Go structs that mirror our Cuelang schemas to ensure type safety.

---

## 2. Why Cuelang?

Cuelang is more than a data format; it is a **Constraint Language**.

| Feature | JSON / YAML | Cuelang |
| :--- | :--- | :--- |
| **Types** | Primitive only | Types are values |
| **Validation** | External (JSON Schema) | Native / Built-in |
| **Templates** | No | Robust interpolation |
| **Unification** | Overwriting | Logical merging (Unification) |

---

## 3. Configuration Patterns

### Schema-First Design
Every project must define its configuration schema in `configs/schema/config.cue`.

```cue
// Example Schema
#AppConfig: {
    server: {
        port: int & > 1024 | *8080 // Default to 8080
        host: string | *"localhost"
    }
    database: {
        url: string
        timeout: duration | *"30s"
    }
}
```

### Composition over Inheritance
Use Cue's unification to build environment-specific configs without repeating the base schema.

```cue
// base.cue
#Config: { ... }

// prod.cue
#Config & {
    server: host: "api.production.com"
}
```

---

## 4. Runtime Validation

One of the greatest benefits of Cuelang is ensuring the application never starts with an invalid state.

1.  **Load:** Read the `.cue` or `.json` file.
2.  **Unify:** Merge with the internal schema.
3.  **Validate:** The `cue` runtime checks constraints (e.g., is `port` actually an `int`? Is it `> 1024`?).
4.  **Unmarshal:** If valid, map to a Go struct. If invalid, the app exits with a clear error message.

---

## 5. Semantic State as Code

Beyond configuration, we use Cuelang to define the **Semantic State** (the intermediate representation) of our agentic workflows.

*   **Schema as Contract:** Ingestor agents must produce output that unifies with the state schema.
*   **Refinement:** Users "edit" the state by providing Cue snippets that unify with the existing state, ensuring they can't break the document's structure.
