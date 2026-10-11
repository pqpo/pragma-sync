---
name: test-greeting
description: A minimal test Skill for validating the Skill revision workflow.
---

# Test Greeting123

Produce a single friendly greeting sentence. This Skill exists to validate the Skill revision workflow, so keep its behavior simple, deterministic, and self-contained.

## When it applies

Use this Skill when the task asks for:

- a friendly greeting sentence,
- a greeting addressed to a specific person, or
- a minimal end-to-end check of the Skill revision workflow.

Do not use it for multi-paragraph introductions, translations, or anything requiring external data.

## Inputs and outputs

Inputs (all optional):

- `name`: who the greeting is addressed to. Default: `there`.
- `tone`: `friendly` (default) or `cheerful`.

Output: exactly one sentence ending in a period, exclamation mark, or question mark. No preamble and no trailing text.

## Workflow

1. Read the requested `name` and `tone`; if either is absent, use its default.
2. Choose the template from `references/greeting-templates.md`:
   - `friendly` → `Hello, {name}! Nice to see you.`
   - `cheerful` → `Hi, {name}! Hope you have a great day!`
3. Resolve `{name}` using the placeholder rules in `references/greeting-templates.md`; keep the template wording exactly as written.
4. Return exactly that sentence and nothing else.
5. Verify the result is a single sentence and contains the resolved name (or the default).

## Constraints

- Never call tools, scripts, or network services; produce the reply directly.
- Do not add emojis, extra sentences, or commentary.
- Keep the same sentence structure across runs for identical inputs.

## Failure handling

- If `tone` is unknown, fall back to `friendly` and still return one sentence.
- If `name` has leading, trailing, or repeated whitespace, trim and collapse it; if it is empty after trimming, use the default.
- If the request is not a greeting task, state that this Skill does not apply instead of forcing a greeting.

## Example

Input: `name: Ada`, `tone: cheerful`
Output: `Hi, Ada! Hope you have a great day!`

Input: greeting for no particular person
Output: `Hello, there! Nice to see you.`

Input: `name: "  Ada Lovelace  "`, `tone: friendly`
Output: `Hello, Ada Lovelace! Nice to see you.`

## References

- `references/greeting-templates.md`: the fixed template table, placeholder resolution rules, and whitespace edge cases.
