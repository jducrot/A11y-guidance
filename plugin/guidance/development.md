# Development guidance

Use this guide when advising on web markup, styling, scripting, components, testing, and remediation.

## Review approach

1. Clarify the affected page, component, user task, framework or runtime constraints, and supported browsers or assistive technologies.
2. Inspect the actual markup and interaction behavior when available; do not infer conformance from appearance or a code snippet alone.
3. Recommend semantic HTML and native platform behavior before custom ARIA or interaction.
4. Describe implementation changes and relevant keyboard, focus, announcement, error, and responsive behavior.
5. Link to relevant WCAG 2.2 Level AA criteria and specific reviewed resources, distinguishing requirements from implementation advice.
6. Suggest proportionate automated and manual tests, including keyboard and assistive-technology checks for the affected task.

## Common areas to consider

- Semantic structure, accessible names, labels, roles, and relationships.
- Keyboard operation, focus order and visibility, focus not being obscured, and no keyboard traps.
- Contrast, zoom, text resizing, reflow, and responsive behavior.
- Accessible form validation, error identification, instructions, and status messages.
- Correct use of ARIA only where native HTML does not provide the needed semantics or behavior.
- Testing with relevant browsers and assistive technologies; automated tooling is one input, not proof of conformance.

Do not claim the whole product conforms based on a component review or a passing automated scan.
