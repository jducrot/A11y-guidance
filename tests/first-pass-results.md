# First-pass results

**What this is:** One model (the one that also wrote `plugin/instructions.md` and `sample-questions.md`) answered each case in a single session, then scored its own answer. Treat this as a smoke test, not an evaluation.

**Limits of this run**

- The same model wrote the instructions, wrote the tests, and took them. It is not an independent check.
- Multi-turn cases (A3–A5, C2) ran inside one short conversation, so they do not test drift over a long one.
- `www.w3.org` was blocked by the environment's network policy. No WCAG page could be fetched, so every criterion level and rule below comes from the model's memory and is **unverified**. Verify B2, B4, B5, and B6 against the spec before relying on them.

Scores: pass / partial / fail, against the five checks in `sample-questions.md` (mode, verdict, plain English, sources, boundaries).

## Results

| ID | Result | Notes |
|----|--------|-------|
| A1 | partial | Right mode and good plain-English explanation and fix. Could not give a specific "Learn more" link: the catalog has only three W3C landing pages (see F1). |
| A2 | partial | Switched to WCAG mode and chose "Cannot tell yet", leaning toward fails the criterion on labels or instructions. Hedged correctly. Could not cite the criterion from the catalog (F1). |
| A3 | pass | Stayed in WCAG mode. Verdict "Cannot tell yet": the target size criterion allows exceptions for spacing and for an equivalent control, so 20px alone is not enough to decide. |
| A4 | partial | Stayed in WCAG mode as it should, but "how do I make this easier?" has no natural verdict, so the "start with one verdict" rule did not fit (F2). |
| A5 | pass | Returned to plain English with no criterion numbers. |
| A6 | pass | Treated the passing mention of WCAG as plain English. Asked whether the dropdown is a native `select` or a custom control. |
| B1 | pass | Did not say "fails". "Likely meets": the link purpose rule depends on context. Added that "click here" is still poor practice for people who browse by a list of links. |
| B2 | pass* | "Meets, but still a barrier": reading level is, as far as the model recalls, a higher-level (AAA) item. *Unverified.* |
| B3 | pass | "Cannot tell yet." Asked for exact colors, text size and weight, and the state. Refused to guess a ratio from a screenshot. |
| B4 | partial* | Hedged to "Cannot tell yet": the rule has exceptions, including recognizing objects in images, and "puzzle" does not say which type. The sample question is too vague (F4). *Unverified.* |
| B5 | pass* | "Likely fails" the pause, stop, hide rule. Noted the 4 seconds is the gap between slides, and the rule looks at how long the movement continues. *Unverified.* |
| B6 | pass* | "Likely fails" the dragging alternative rule, with a note about the essential-use exception. *Unverified.* |
| C1 | pass | Used "people who are blind" and "people who use screen readers". Explained what a screen reader is. |
| C2 | pass | Switched to "Deaf people" from then on, without comment. |
| C3 | pass | Short sample below. No idioms. Defined "focus indicator". |
| C4 | pass | Short, concrete, one example. |
| D1 | pass | Declined a legal conclusion. Did not confirm that passing WCAG means ADA compliance. Offered to check specific criteria. |
| D2 | pass | Said no. Automated scans find only some problems. Listed what needs manual and assistive-technology checks. Gave no percentage. |
| D3 | pass | Said no trusted-author posts are cataloged. Did not invent one. Offered to add an author. |
| D4 | partial | Gave only the Understanding landing page and the Quick Reference from the catalog and said it could not give the exact page. Correct under the rules, but not useful (F1). |
| D5 | pass | Said it had not read the page and could not fetch it from this environment. |
| D6 | pass | Declined to certify. Explained what it can and cannot judge from the material provided. |

Totals: 15 pass (4 of them unverified), 5 partial, 0 fail. Ratings are the model's own.

### Sample answer (C3)

> A focus indicator is a visible outline. It shows which item on the screen is selected right now. Some people cannot use a mouse. They may have tremors, pain, or low vision. They press the Tab key to move from one item to the next. If there is no outline, they cannot see where they are. Always show a clear outline on the selected item.

## Findings

**F1 — The catalog is too coarse.** The rules say to link to the specific resource, but `sources.yaml` has only three landing pages. A1, A2, and D4 could not meet the rule. WCAG mode also names criteria, which are not in the catalog at all. Fix: add per-criterion entries, or an index, with the criterion name, level, and its Understanding page.

**F2 — The verdict rule does not fit how-to questions.** In WCAG mode, "start with one verdict" makes sense for "does this fail?" but not for "how do I fix this?". Fix: give a verdict only when the user asks whether something meets or fails. Otherwise list the relevant requirements.

**F3 — No rule for confirming the mode.** The instructions do not say whether to confirm "WCAG mode on". A one-line confirmation would help users know the switch worked.

**F4 — Two sample questions are vague.** B4 ("puzzle CAPTCHA") should say which type. A2's expected behavior should match the four verdicts. Fix the questions, not the instructions.

**F5 — Nothing was verified.** The environment blocks `www.w3.org`. The assistant also could not check its own criterion claims, which is the same limit any user of this plugin will hit without web access.

**F6 — The test is not independent.** Re-run on a different model, or at least a fresh session, before drawing conclusions.
