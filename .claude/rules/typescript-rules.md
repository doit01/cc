# TypeScript Rules

- No `any` type — use `unknown` + type guard or a proper interface
- All function parameters and return types must be explicitly typed
- Use `readonly` for immutable data (DTOs, config objects)
- Prefer `interface` over `type` for object shapes
- Use `enum` only for stable sets of values, otherwise use union types
- Never use non-null assertion `!` — use optional chaining and defaults
