# A11y-guidance

A model- and platform-neutral accessibility guidance plugin for people designing and developing web products. It helps users apply WCAG 2.2 Level AA and gives actionable advice grounded in trusted resources.

## Scope

- Digital products delivered on the web.
- WCAG 2.2 Level AA is the default benchmark, not a guarantee of legal compliance or a product certification.
- Guidance should account for context, identify uncertainty, and encourage testing with people with disabilities in addition to automated and manual checks.

## Structure

```text
plugin/
├── manifest.yaml
├── instructions.md
├── guidance/
│   ├── design.md
│   └── development.md
├── criteria.yaml
└── sources.yaml
tests/
└── sample-questions.md
```

- `plugin/instructions.md` defines how the assistant should give and qualify guidance.
- `plugin/guidance/design.md` and `plugin/guidance/development.md` organize practical advice for each audience.
- `plugin/criteria.yaml` indexes every WCAG 2.2 success criterion with its level and links to the normative text and W3C explanations. It holds metadata only and was generated from the published Recommendation.
- `plugin/sources.yaml` catalogs specific resources and the trusted authors whose blog posts may be used.
- `tests/sample-questions.md` lists manual test questions with expected behavior. `tests/first-pass-results.md` and `tests/other-model-results.md` record two runs of them, with raw replies in `tests/other-model-raw-replies.md`.
- `plugin/manifest.yaml` describes the plugin and its scope without binding the guidance to a particular LLM platform.

## Sources

The source catalog includes canonical W3C resources and can include individual blog posts from authors the project maintainer has explicitly trusted. A blog post is an additional perspective, not a replacement for WCAG or W3C guidance. The assistant should link to the specific resource supporting its advice, distinguish normative requirements from recommendations, and not imply that a source is endorsed by W3C.

To add a trusted author, add an entry under `trusted_authors` in `plugin/sources.yaml`; then add each reviewed post as an individual resource and associate it with that author's ID. Record a review date and relevant topics so sources can be maintained over time. Do not add an author or post as trusted by default.

## Using the plugin

The files in `plugin/` are the platform-neutral source of truth. Platform-specific packaging or adapters can be added later without duplicating the guidance or source catalog.
