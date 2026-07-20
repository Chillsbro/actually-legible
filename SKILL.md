---
name: actually-legible
description: Architectural taste for TypeScript and React coding agents. Minimize conceptual surface area, preserve clear dependency direction, and produce code humans can navigate, review, and evolve. Use when implementing, refactoring, reviewing, scaffolding, or organizing TypeScript and React code, including modules, imports, exports, folders, files, functions, components, hooks, naming, and comments.
---

# Actually Legible

Apply these rules to authored or modified code. Preserve externally imposed interfaces and established repository conventions when changing them would break compatibility or create unrelated churn.

## Design

1. Minimize total conceptual surface area: files, folders, exports, abstractions, dependency hops, and code. Add a seam only when it improves cohesion, navigation, reuse, testability, or dependency direction.
2. Keep declarations together when they change for the same reason. Split a file when the result has a clearer interface or dependency direction, not solely because of its length or number of exports.
3. Treat 100 lines as a prompt to inspect cohesion, never as a mechanical limit.
4. Keep private helpers beside their sole caller when extraction would add navigation without independent meaning or reuse.
5. Use short, descriptive names. Avoid opaque placeholders such as `s`, `e`, `n`, and `obj` outside conventional tiny scopes where their meaning is unmistakable.
6. Prefer names and structure over explanatory comments. Comment only necessary constraints, non-obvious reasons, externally imposed behavior, or deliberate tradeoffs.
7. Implement the smallest complete solution that remains readable. Avoid speculative abstractions, wrappers, configuration, and fallback paths.

## Modules and Imports

1. Prefer direct imports between files inside an application or module. Make the actual dependency visible.
2. Add a barrel only when it is a deliberate consumer-facing entry point. A folder does not need an `index` file merely because it exists.
3. Never import a module's barrel from within that module's own implementation. Import the owning file directly to avoid hidden cycles and inflated dependency graphs.
4. Export names explicitly from public entry points. Avoid `export *` when it obscures ownership or unintentionally expands the supported interface.
5. For published packages, define supported entry points with `package.json` `exports`; do not rely on folder barrels to enforce encapsulation.
6. Use `import type` and `export type` for type-only dependencies.
7. Match `module` and `moduleResolution` to the real runtime or bundler. Prefer `module: "preserve"` with `moduleResolution: "bundler"` for Bun and modern bundler-owned applications unless the host requires another mode.
8. Do not introduce TypeScript `paths` aliases as a style preference. They do not rewrite runtime imports. Use runtime-supported package imports or workspace packages only when repeated deep imports create a demonstrated navigation problem.
9. Consider `verbatimModuleSyntax` when the project benefits from explicit type/value import behavior, and `noUncheckedSideEffectImports` when it uses side-effect imports.

## Structure

1. Organize source by functional area or domain before generic technical category.
2. Extend the area that owns a behavior before creating an overlapping `utils`, `helpers`, `common`, or `misc` module.
3. Create a folder only when it groups a meaningful area or multiple cohesive files. Do not create a folder solely to wrap one file.
4. Name implementation files after their main concept, operation, hook, component, or type.
5. Keep a type beside its sole consumer. Move shared domain types to the narrowest common owner rather than a global type bucket.
6. Follow framework naming and placement conventions when they improve recognition or tooling support.
7. Follow the repository's existing test layout unless changing it is part of the task.

## Workflow

1. Inspect nearby code, compiler settings, package metadata, and established import patterns.
2. Identify the functional area that owns the behavior and the smallest compatible change.
3. Trace dependency direction before adding a file, export, barrel, alias, or abstraction.
4. Reuse existing code when doing so preserves cohesion; do not reuse merely to avoid a small local implementation.
5. Implement the shortest clear solution.
6. Update a public entry point only when the change intentionally alters its supported consumer interface.
7. Remove redundant branches, comments, types, wrappers, files, and exports introduced by the change.
8. Verify with the smallest relevant typecheck, test, lint, or build command.
9. Recheck cohesion, dependency direction, public surface area, naming, and avoidable indirection.

## Exceptions

- Do not edit generated, vendored, or third-party files solely to satisfy this style.
- Preserve framework-mandated file shapes, overloads, declaration layouts, and public interfaces.
- Keep cohesive declarative structures such as schemas, lookup tables, reducers, and related operations intact when splitting them would reduce clarity.
- Prefer correctness and compatibility over these heuristics, then minimize conceptual surface area.
