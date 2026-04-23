---
name: mockup
description: Create production-ready UI mockups tied to real API states and design system constraints. Use when the user asks for polished screen mockups, stateful UI explorations, or handoff-ready visual specs.
---

# Mockup Creation

Build implementation-ready mockups that align with backend states, the project's design schema, and design system constraints.

## Workflow

1. Define scope
  - Confirm target screens, user flow, and platform (web/mobile).
  - Identify required states: loading, empty, success, error, and permission-restricted.
2. Map data contract
  - List the API endpoints and response fields each screen depends on.
  - Represent realistic payload sizes and edge cases in the mockup (long text, missing fields, zero-state).
3. Design system and brand alignment
  - Follow `../wireframes/design-schema.md` as the source of truth for brand, token, and interaction decisions.
  - If the schema is missing or incomplete, do not invent brand colors, typography, or voice. Call out the missing decisions and use clearly labeled neutral placeholders only where needed.
  - Use a consistent spacing scale, typography hierarchy, and semantic color usage when those rules are defined in the schema.
4. Produce mockup package
  - Primary mockup for each screen.
  - Variant mockups for each required state.
  - Annotation layer with:
    - element purpose
    - bound API field(s)
    - interaction behavior
    - validation/error rules
5. Handoff details
  - Include component inventory and reusable tokens.
  - Include interaction notes (hover, focus, disabled, keyboard behavior).
  - Include implementation risks and unanswered product questions.

## Quality Bar

- Every important backend state is represented.
- Critical paths are complete end-to-end.
- Layout and copy are internally consistent.
- Accessibility constraints are represented in the design.
- Missing schema decisions are called out explicitly instead of guessed.
- Specs are actionable for engineering handoff without additional clarification.