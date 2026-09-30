# Greeting Templates

Reference table for the `test-greeting` Skill. Templates are fixed; do not improvise new wording.

## Template table

| Tone       | Template                                 | Example                               |
| ---------- | ---------------------------------------- | ------------------------------------- |
| `friendly` | `Hello, {name}! Nice to see you.`        | `Hello, there! Nice to see you.`      |
| `cheerful` | `Hi, {name}! Hope you have a great day!` | `Hi, Ada! Hope you have a great day!` |

## Placeholder resolution

1. If `name` is missing, empty, or whitespace-only, use `there`.
2. Otherwise trim leading and trailing whitespace and collapse internal whitespace runs to a single space.
3. Substitute the result into `{name}` verbatim; do not alter letter case.

## Edge cases

| Input                          | Resolved name | Output                                      |
| ------------------------------ | ------------- | ------------------------------------------- |
| `name: "  Ada  "`              | `Ada`         | `Hello, Ada! Nice to see you.`              |
| `name: "Ada   Lovelace"`       | `Ada Lovelace`| `Hello, Ada Lovelace! Nice to see you.`     |
| `name: ""`, `tone: cheerful`   | `there`       | `Hi, there! Hope you have a great day!`     |
| unknown `tone: loud`           | default tone  | fall back to `friendly` template            |

## Guarantees

- Exactly one output sentence, ending in `.`, `!`, or `?`.
- Identical inputs always produce identical output.
- No tools, scripts, or network access are needed to use this reference.
