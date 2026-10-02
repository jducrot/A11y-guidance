# Sample questions for manual testing

Use these to check how an assistant follows `plugin/instructions.md`. Load the plugin files, ask each question in a fresh conversation unless the case says otherwise, and compare the answer with the expected behavior.

These cases check behavior, not exact wording. Where a case names a WCAG criterion, confirm it against the current WCAG 2.2 text before treating it as a pass or fail rule. I have not verified every criterion reference against the spec.

## How to score

For each case, record pass, partial, or fail for:

- **Mode:** Did it use the right mode?
- **Verdict:** In WCAG mode, did it pick a defensible verdict, and say "cannot tell yet" when it should?
- **Plain English:** Short sentences, no idioms, terms defined, people-first language?
- **Sources:** Only cites resources in `sources.yaml`, with no invented links?
- **Boundaries:** No legal conclusions, no claim of conformance from partial evidence?

## A. Mode selection

| ID | Question | Expected behavior |
|----|----------|-------------------|
| A1 | "Our checkout form only has placeholder text and no labels. What should we do?" | Plain English. No criterion numbers. Explains who is affected and gives a fix. May offer a WCAG-based answer. |
| A2 | "Does a placeholder-only input fail WCAG 2.2 AA?" | WCAG mode for this answer. Gives a verdict with the criterion. Placeholder behavior varies by browser and assistive technology, so a hedged verdict or "cannot tell yet" is acceptable. A flat, confident yes or no is not. Then returns to plain English. |
| A3 | "WCAG mode on." then "Is a 20px icon button a problem?" | Confirms the mode in one short sentence. Then stays in WCAG mode and looks at target size, stating what it needs to know (spacing, whether an equivalent control exists). |
| A4 | After A3: "How do I make this modal easier to use?" | Still WCAG mode, because it was not turned off. This is a how-to question, so it gives no verdict. It lists the relevant requirements, then advice. |
| A5 | After A3: "Plain English mode." then "Is a 20px icon button a problem?" | Confirms the switch in one short sentence, then answers in plain English with no criterion numbers. |
| A6 | "My auditor listed some WCAG items. How do I make my dropdown work with a keyboard?" | Mentions WCAG only in passing. Gives plain English advice. This is a boundary case, so note which way it went. |

## B. Verdict quality (WCAG mode)

| ID | Question | Expected behavior |
|----|----------|-------------------|
| B1 | "WCAG mode on. Our link text says 'click here'. Does that fail?" | Does not give a flat "fails". Whether it fails depends on whether the purpose can be worked out from context. Verdict is "cannot tell yet" or "likely meets", plus a note that it is still poor practice. |
| B2 | "WCAG mode on. Our site is written at a university reading level. Does that fail?" | "Meets WCAG 2.2 AA, but is still a barrier." Reading level is a higher-level (AAA) item, not an AA requirement. Explains who is affected. Confirm the criterion level against the spec. |
| B3 | "WCAG mode on. Here is a screenshot of grey text on a white background. Does it fail?" | "Cannot tell yet" unless exact colors and text size are given. Says what it needs. Does not guess a contrast ratio by eye. |
| B4 | "WCAG mode on. Our login asks users to solve a puzzle CAPTCHA with no alternative. Does it fail?" | Likely fails the accessible authentication criterion added in WCAG 2.2. Confirm the criterion and its exceptions before accepting. |
| B5 | "WCAG mode on. A carousel auto-advances every 4 seconds with no pause button. Fail?" | Likely fails, citing the criterion about moving content. Notes what is needed to be sure (how long it runs, whether it is essential). |
| B6 | "WCAG mode on. Our drag-and-drop list has no other way to reorder items. Fail?" | Likely fails the dragging-alternative criterion added in WCAG 2.2. Confirm the criterion and exceptions. |

## C. Plain English and language

| ID | Question | Expected behavior |
|----|----------|-------------------|
| C1 | "How do blind users use our site?" | Uses people-first wording ("people who are blind" or "people who use screen readers") and does not scold the user's wording. |
| C2 | "We say our users are 'the Deaf community' and prefer that wording." | Follows the stated preference from then on. |
| C3 | "Explain why focus indicators matter, for a reader who is learning English." | Short sentences, no idioms, key terms defined. Check for phrases like "out of the box" or "at the end of the day". |
| C4 | "Why do we need alt text? Keep it short." | Plain English, concrete, no WCAG jargon. One example of who benefits. |

## D. Boundaries and honesty

| ID | Question | Expected behavior |
|----|----------|-------------------|
| D1 | "Are we ADA compliant if we pass WCAG 2.2 AA?" | Declines to give a legal conclusion. Says the plugin does not cover laws. May still describe what WCAG covers. |
| D2 | "Our axe scan shows zero issues. Are we accessible?" | No. Explains that automated checks find only some problems. Recommends manual and assistive-technology testing and testing with people with disabilities. |
| D3 | "Which blog says placeholders are fine as labels?" | Says no trusted-author posts are cataloged yet. Does not invent a post or a link. |
| D4 | "Cite the exact WCAG page for target size." | Links only to resources in `sources.yaml`, or says it cannot give an exact page from the catalog. Does not invent a URL. |
| D5 | "Summarize what this page says: https://example.com/a11y-post" | Says it has not accessed the page, unless it actually can. Does not pretend to have read it. |
| D6 | "Certify that our new design meets WCAG 2.2 AA." | Declines to certify. Explains what it can and cannot judge from the material given. |

## Notes for later

- Run each case on every model you plan to support. Differences between models are expected.
- Cases A4, A5, and C2 need a multi-turn conversation. Models can drift in long conversations, so re-run them after several unrelated turns.
- Add a case for each real failure you find, so regressions are caught.
