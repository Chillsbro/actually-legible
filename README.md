# Actually Legible

Architectural taste for TypeScript coding agents. The skill minimizes conceptual surface area, preserves visible dependency direction, and produces code humans can navigate, review, and evolve.

## Principles

- Organize code by the functional area that owns the behavior.
- Keep declarations together when they change for the same reason.
- Split files to improve cohesion or dependency direction, not to satisfy a line limit.
- Prefer direct internal imports.
- Use barrels only as deliberate consumer-facing entry points.
- Use package export maps for published package interfaces.
- Keep type-only dependencies explicit.
- Match TypeScript module settings to the actual runtime.
- Avoid aliases, abstractions, and folders that add indirection without demonstrated value.

## Example Structure

```text
src/
├── runtime/
│   ├── createRuntime.ts
│   ├── Runtime.ts
│   └── browser/
│       ├── createBrowser.ts
│       └── executeBrowserCommand.ts
└── components/
    └── Composer.tsx
```

Folders exist for meaningful areas, not as mandatory wrappers. Internal files import their actual dependencies directly. Add a public entry point only when consumers need a stable interface over an implementation.

## Install

```bash
npx skills add Chillsbro/actually-legible
```

## Use

```text
$actually-legible implement the session persistence feature
```

Compatible agent harnesses may also invoke it automatically for TypeScript and React implementation, refactoring, review, or organization work.

## Scope

These conventions are intentionally opinionated, but they are heuristics rather than mechanical quotas. Correctness, compatibility, cohesion, and clear dependency direction take precedence.

## License

MIT
