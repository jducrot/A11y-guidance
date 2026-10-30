# CLAUDE.md

This repo is a content-only accessibility guidance plugin: Markdown prompts, a YAML source catalog, and a YAML index of WCAG 2.2 success criteria. It has no code, build, dependencies, or automated tests. "Changing the plugin" means editing prose and YAML. `tests/` holds manual test cases and the results of past runs.

## What lives where

- `plugin/manifest.yaml` is the plugin descriptor. `entrypoint`, `guidance`, `sources`, and `criteria` hold paths relative to `plugin/`.
- `plugin/instructions.md` is the entrypoint. It defines two answer modes: Plain English mode (the default) and WCAG mode (only when the user asks). WCAG mode answers "does this pass?" questions with one of four verdicts. "Rules for both modes" holds the shared rules for context, citation, and testing.
- `plugin/guidance/design.md` and `plugin/guidance/development.md` each hold a numbered "Review approach" and a "Common areas to consider" list for their audience.
- `plugin/sources.yaml` lists the resources the assistant may cite, plus `trusted_authors`, which is currently empty. Its `criteria_index` key points to `criteria.yaml`.
- `plugin/criteria.yaml` indexes every WCAG 2.2 success criterion: number, name, level, status, and links to the normative text, Understanding page, and Quick Reference. WCAG mode takes criterion details from this file, not from memory.
- `tests/sample-questions.md` lists manual test cases with expected behavior and a scoring rubric. Other files in `tests/` record the results of runs against those cases.
- `README.md` explains the project to people, including a directory tree of `plugin/` and `tests/`.

## Invariants to preserve

- **Platform neutrality.** Files in `plugin/` are the source of truth and must not reference a specific LLM, vendor, or tool format. Platform-specific adapters belong outside `plugin/` and should reference these files rather than copy them.
- **Plain English by default.** Answers use plain English unless the user asks for WCAG terms. Keep WCAG jargon, criterion numbers, and conformance levels out of the Plain English mode rules and examples.
- **Scope.** The scope is web products only, with WCAG 2.2 Level AA as the only benchmark in WCAG mode. Never word the guidance as certification, a conformance guarantee, or legal advice. `instructions.md` "Boundaries" and the README "Scope" section say this, so keep any new text consistent with them.
- **Source hierarchy.** W3C/WCAG sources are authoritative for normative requirements. Trusted-author posts only add perspective and never override W3C. APG patterns are examples, not WCAG requirements.
- **Keep files in sync.** If you add, rename, or remove a file in `plugin/`, update `manifest.yaml` and the README structure tree and file list. If you add a file to `tests/`, update the README tree and file list.
- **Rules belong in one place.** Cross-cutting response rules (citation, uncertainty, testing) belong in `instructions.md`, under "Rules for both modes" unless they apply to only one mode. The guidance files only cover what is specific to design or development.

## Editing `sources.yaml`

- Catalog each resource individually with a stable kebab-case `id`, `type`, `title`, `publisher`, `url`, `topics`, `use_for`, and `reviewed_on`.
- Known `type` values are `w3c-standard`, `w3c-guidance`, `w3c-resource`, and `trusted-author-blog`. Use one of them unless a new type is clearly needed.
- `topics` values in use are `all`, `design`, and `development`. `use_for` is a short kebab-case phrase.
- Write `reviewed_on` as a quoted date string (`"YYYY-MM-DD"`). Use `null # pending maintainer review` when the maintainer hasn't reviewed the resource yet. Never fill in a review date yourself; it records a human review.
- **Never add a trusted author or blog post on your own initiative.** The maintainer must explicitly approve each one. Approved posts are added as individual resources whose `author` is a `trusted_authors` id. The commented example shapes at the bottom of the file are the template.

## Editing `criteria.yaml`

- The file is generated from the published W3C Recommendation. Do not hand-edit numbers, names, levels, or links, and never fill them in from memory. If something is wrong, regenerate the file from the spec and update `spec.retrieved_on`.
- It holds metadata only. Do not copy criterion text into it; `normative_url` points to the exact wording.
- `status` is `active` or `removed-in-wcag-22`. Removed criteria have `level: null`. `in_scope_default` is true only for active Level A and AA criteria.
- `spec.counts` must match the entries: active criteria counted by level, plus removed ones.

## Manual tests

- When you change how the assistant should behave in `instructions.md`, add or update the matching cases in `tests/sample-questions.md`.
- Results files record what happened in a specific run. Do not edit past results to match new instructions; add a new results file instead, and note which model ran it and any limits of the run.

## Writing style

Write the prose in plain, direct imperative English with short sentences and short bullets, as `instructions.md` asks the assistant to do. In guidance, separate WCAG requirements from good practice. Use people-first language and name the users affected. Recommend manual and assistive-technology testing rather than relying on automated checks. Match the hedged, non-absolute tone of the existing files.

## Verifying changes

There is no test runner. Before you finish:
- Check that the YAML still parses: `ruby -ryaml -e 'ARGV.each { |f| YAML.load_file(f) }; puts "ok"' plugin/*.yaml`. PyYAML isn't installed here; Ruby's YAML parser is built in.
- Check that every path in `manifest.yaml` exists: `ruby -ryaml -e 'm = YAML.load_file("plugin/manifest.yaml"); p [m["entrypoint"], m["sources"], m["criteria"], *m["guidance"]].reject { |f| File.exist?("plugin/#{f}") }'` should print `[]`.
- If you touched `criteria.yaml`, check its counts: `ruby -ryaml -e 'd = YAML.load_file("plugin/criteria.yaml"); got = d["criteria"].group_by { |x| x["status"] == "active" ? x["level"] : "removed" }.transform_values(&:size); puts got == d["spec"]["counts"] ? "ok" : got'`.
- Check that the README tree matches `plugin/` and `tests/`.
