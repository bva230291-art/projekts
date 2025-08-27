## API Reference

At the time of writing, no public APIs, functions, or components were detected in the repository. This file serves as the canonical reference and provides templates to document new APIs as the codebase evolves.

### Current API Surface
- None detected

---

### Templates and Examples

#### JavaScript/TypeScript Functions

##### Example: `formatDate`

Signature
```ts
function formatDate(input: Date | string, options?: { locale?: string; pattern?: string }): string
```

Description
- Converts a `Date` or ISO8601 string to a localized string using an optional pattern.

Usage
```ts
import { formatDate } from "@project/utils/date";

const s1 = formatDate(new Date("2024-12-01T09:30:00Z"));
const s2 = formatDate("2024-12-01", { locale: "en-GB", pattern: "dd/MM/yyyy" });
```

Notes
- Accepts both `Date` and ISO8601 strings.
- Throws on invalid date inputs.

Documentation Block Template
```md
#### <FunctionName>

Signature
```ts
<signature>
```

Description
- <what it does and why>

Parameters
- **paramName**: <type> - <description>

Returns
- <type> - <description>

Usage
```ts
import { <FunctionName> } from "<package-or-path>";

const result = <FunctionName>(<args>);
```

Notes
- <edge cases, performance, version added>
```

---

#### TypeScript Types and Interfaces

Example
```ts
export interface HttpRequestOptions {
  method: "GET" | "POST" | "PUT" | "DELETE";
  headers?: Record<string, string>;
  body?: unknown;
  timeoutMs?: number;
}
```

Usage
```ts
import { HttpRequestOptions } from "@project/net/types";

const opts: HttpRequestOptions = { method: "GET", timeoutMs: 5_000 };
```

---

#### React Components

##### Example: `<Button />`

Props
```ts
type ButtonProps = {
  children: React.ReactNode;
  variant?: "primary" | "secondary" | "ghost";
  disabled?: boolean;
  onClick?: () => void;
}
```

Usage
```tsx
import { Button } from "@project/ui";

export function Toolbar() {
  return (
    <div>
      <Button variant="primary" onClick={() => console.log("clicked")}>Save</Button>
    </div>
  );
}
```

Accessibility Notes
- Ensure focus styles are visible.
- Provide `aria-pressed` for toggle buttons.

Component Documentation Template
```md
### <ComponentName>

Props
```ts
type <ComponentName>Props = { /* ... */ }
```

Description
- <purpose and behavior>

Usage
```tsx
<<minimal example>>
```

Accessibility
- <a11y considerations>
```

---

#### Python Functions and Classes

Example Function
```python
def parse_date(value: str, *, tz: str | None = None) -> datetime:
    """Parse ISO8601 `value` into a timezone-aware datetime.

    Raises ValueError for invalid inputs.
    """
    ...
```

Usage
```python
from project.dates import parse_date

dt = parse_date("2024-12-01T09:30:00Z")
```

Documentation Block Template
```md
#### <symbol>

Signature
```python
<def signature>
```

Description
- <behavior and constraints>

Examples
```python
<copy-pastable example>
```
```

---

#### CLI Commands

Template
```md
### `project <command>`

Description
- <what the command does>

Synopsis
```bash
project <command> [options]
```

Options
- **--flag**: description

Examples
```bash
project <command> --flag value
```
```

---

### Versioning
- Document the version each API was added or changed.
- Use semantic versioning where applicable.