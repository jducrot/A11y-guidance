# First-pass results

**What this is:** One model (the one that also wrote `plugin/instructions.md` and `sample-questions.md`) answered each case in a single session, then scored its own answer. Treat this as a smoke test, not an evaluation.

**Limits of this run**

- The same model wrote the instructions, wrote the tests, and took them. It is not an independent check.
- Multi-turn cases (A3–A5, C2) ran inside one short conversation, so they do not test drift over a long one.
- `www.w3.org` was blocked during the run, so the criterion levels and rules were written from memory. They were checked afterwards against the published WCAG 2.2 Recommendation (12 December 2024); see "Verification" below.

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
| B2 | pass* | "Meets, but still a barrier": reading level is, as far as the model recalls, a higher-level (AAA) item. *Verified afterwards.* |
| B3 | pass | "Cannot tell yet." Asked for exact colors, text size and weight, and the state. Refused to guess a ratio from a screenshot. |
| B4 | partial* | Hedged to "Cannot tell yet": the rule has exceptions, including recognizing objects in images, and "puzzle" does not say which type. The sample question is too vague (F4). *Verified afterwards.* |
| B5 | pass* | "Likely fails" the pause, stop, hide rule. Noted the 4 seconds is the gap between slides, and the rule looks at how long the movement continues. *Verified afterwards.* |
| B6 | pass* | "Likely fails" the dragging alternative rule, with a note about the essential-use exception. *Verified afterwards.* |
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

Totals: 15 pass (4 of them checked against the spec afterwards), 5 partial, 0 fail. Ratings are the model's own.

### Sample answer (C3)

> A focus indicator is a visible outline. It shows which item on the screen is selected right now. Some people cannot use a mouse. They may have tremors, pain, or low vision. They press the Tab key to move from one item to the next. If there is no outline, they cannot see where they are. Always show a clear outline on the selected item.

## Findings

**F1 — The catalog is too coarse.** The rules say to link to the specific resource, but `sources.yaml` has only three landing pages. A1, A2, and D4 could not meet the rule. WCAG mode also names criteria, which are not in the catalog at all. Fix: add per-criterion entries, or an index, with the criterion name, level, and its Understanding page.

**F2 — The verdict rule does not fit how-to questions.** In WCAG mode, "start with one verdict" makes sense for "does this fail?" but not for "how do I fix this?". Fix: give a verdict only when the user asks whether something meets or fails. Otherwise list the relevant requirements.

**F3 — No rule for confirming the mode.** The instructions do not say whether to confirm "WCAG mode on". A one-line confirmation would help users know the switch worked.

**F4 — Two sample questions are vague.** B4 ("puzzle CAPTCHA") should say which type. A2's expected behavior should match the four verdicts. Fix the questions, not the instructions.

**F5 — Nothing was verified.** The environment blocks `www.w3.org`. The assistant also could not check its own criterion claims, which is the same limit any user of this plugin will hit without web access.

**F6 — The test is not independent.** Re-run on a different model, or at least a fresh session, before drawing conclusions.

## Verification (added after the run)

After `www.w3.org` was allowed, the claims flagged above were checked against the published WCAG 2.2 text. All held:

- **2.2.2 Pause, Stop, Hide** is Level A. It applies to moving content that starts automatically, lasts more than five seconds, and is shown alongside other content. So B5's "4 seconds" is not the test; how long the movement continues is.
- **2.4.4 Link Purpose (In Context)** is Level A and fails only if the purpose cannot be worked out from the link text or its programmatic context, except where the purpose is ambiguous to users in general. B1's "likely meets, but poor practice" was right.
- **2.5.7 Dragging Movements** is Level AA, with exceptions for essential dragging and for functions the user agent controls. B6 held.
- **3.3.8 Accessible Authentication (Minimum)** is Level AA. It names "solving a puzzle" as a cognitive function test, but has four exceptions: alternative method, assistive mechanism, object recognition, and personal content. B4's hedge was correct; a puzzle that is object recognition may be allowed.
- **3.1.5 Reading Level** is Level AAA, so B2's "meets AA, but still a barrier" held.
- **2.5.8 Target Size (Minimum)** is Level AA. It requires 24 by 24 CSS pixels, with exceptions for spacing, an equivalent control, inline targets, user agent controls, and essential size. A3 held.
- **3.3.2 Labels or Instructions** is Level A: "Labels or instructions are provided when content requires user input." It does not mention placeholders, so A2's hedge was fair.

F1 is addressed by `plugin/criteria.yaml` and a matching rule in `instructions.md`. F2 and F3 are addressed by edits to `instructions.md` (no verdict on how-to questions; one-line confirmation when the mode is switched). Cases A3, A4, and A5 now expect that behavior; see "Second pass" below. F4 was addressed by splitting A2 and B4 (see below).

## Second pass (A2a, A2b, A3–A5, B4a, B4b)

Same limits as the first pass: the same model wrote the cases and answered them, in one session, with the spec text read first. Multi-turn cases (A3–A5) again ran in one short conversation. The criteria cited were taken from `plugin/criteria.yaml` and the spec text, not from memory.

| ID | Result | Notes |
|----|--------|-------|
| A2a | pass | "Cannot tell yet." Asked for the markup, the placeholder text, whether the instruction is needed after typing, and the browser and assistive technology. Said plainly that 3.3.2 and 4.1.2 do not mention placeholders, so no rule says they fail. Noted that disappearing text can still be a barrier for people with memory or attention difficulties. |
| A2b | pass | "Fails." No programmatic name (4.1.2) and a visible word not tied to the input (1.3.1). Said 3.3.2 is not the main issue because visible text is present. Suggested `<label for="email">`. |
| A3 | pass | Opened with "WCAG mode is on. Say 'WCAG mode off' to go back to plain English." Then "Cannot tell yet" on the 20px button, asking about spacing and whether an equivalent control exists. |
| A4 | pass | Gave no verdict for the how-to question. Listed relevant requirements from the index (Keyboard 2.1.1, No Keyboard Trap 2.1.2, Focus Order 2.4.3, Focus Visible 2.4.7, Focus Not Obscured (Minimum) 2.4.11, Name, Role, Value 4.1.2), then advice. |
| A5 | pass | Opened with "Plain English mode is on." Then answered about the 20px button with no criterion numbers. |
| B4a | pass | "Cannot tell yet." Explained that a puzzle is a cognitive function test with four exceptions, and asked what kind of puzzle and whether another way to sign in exists. Mentioned 1.1.1's CAPTCHA rule as a separate check. |
| B4b | pass | "Fails" 3.3.8. Typing characters is transcription, which the definition counts as a cognitive function test, and none of the four exceptions applies. Noted that an audio alternative would not help if users must transcribe it. |

**Reading these results:** All seven passed, but the same model wrote the cases and the answers, so this shows the cases are consistent with the instructions, not that other models will follow them. The cases that matter most are the "a" cases, because they check that the assistant asks for missing information instead of guessing. Run them on a different model before trusting them.

F4 is closed. F6 (the test is not independent) is still open.
