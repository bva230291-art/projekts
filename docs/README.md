## Project API Documentation

This repository currently contains no source files exposing public APIs, functions, or components. As you add code, use this docs folder to document the public surface area.

### Structure
- `API.md`: Canonical reference for all public modules, functions, classes, types, and components.
- Additional files can be added per package or domain if the project grows.

### How to document new APIs
1. Add or update entries in `API.md` under the appropriate language or framework section.
2. For each public symbol, include:
   - Name and stable import path
   - Signature (parameters, return type)
   - Description (what it does, invariants, side effects)
   - Examples (minimal, copy-pastable)
   - Notes (performance, edge cases, version added)

### Conventions
- Prefer TypeScript-style type annotations in examples for JS/TS.
- Keep examples runnable and focused on one concept.
- Mark experimental APIs clearly and avoid breaking changes without deprecation.

See `API.md` for ready-to-use templates for JS/TS, Python, and UI components.