# Re-run results with updated instructions

After `other-model-results.md`, `plugin/instructions.md` was changed (commit `50e02cf`) to address findings G1 to G5. All 24 cases were then re-run on two different models, one smaller (the one used in `other-model-results.md`) and one larger. Raw replies are in `rerun-raw-replies-smaller-model.md` and `rerun-raw-replies-larger-model.md`.

## What changed in the instructions

- "Cannot tell yet" is the answer unless the question gives enough facts. Check each condition and exception of the criterion against the facts. A poor or common practice does not by itself fail a criterion.
- Do not quote or paraphrase a criterion's wording unless its text was read in the conversation. Otherwise name it, describe it in general terms, and link to it.
- Before recommending a fix, check that it would satisfy the criterion.
- People-first wording even when the user's wording is not. Define terms like ARIA. Do not state how people or assistive technology behave unless a source in the plugin supports it.
- For how-to questions in WCAG mode: list the criteria, then advise, then ask for more context only if it changes the advice.

## How this was run, and its limits

- Same setup as the earlier runs: fresh agent per case, five plugin files only, no web access, one run per case. Multi-turn cases (A3 to A5, C2) were one conversation each, one message at a time. B3 and C2 have the same additions as before.
- Each agent wrote its reply to a file, so the replies are exact. Previously most agents summarized their reply.
- One run per case per model. A single run can pass or fail by chance. Treat small differences as noise.
- The same person wrote the instructions, the expected behaviors, and this scoring. The raw replies are included so it can be checked.
- **There is no before-and-after for the larger model.** It was not run on the old instructions, so these results do not show whether the changes helped it. For the smaller model there is a before (`other-model-results.md`).
- The agents may have used a model different from the one requested. This was not verified.

## Scores

S = smaller model, L = larger model.

| ID | S | L | Notes |
|----|---|---|-------|
| A1 | partial | pass | S said screen readers "cannot identify what each field is for", which no source supports, and used "ARIA" undefined. L explained that behavior varies by browser and tool. |
| A2a | **fail** | pass | S said "Fails" and named 3.3.2 and 4.1.2. L said "Cannot tell yet", leaned toward fail, asked for the markup, and said WCAG does not name placeholders directly. |
| A2b | partial | pass | S's verdict was right but it described 2.4.6 as requiring labels to be associated with inputs, which is not what that criterion covers, and it omitted 1.3.1. L gave 4.1.2 and 1.3.1, and said 3.3.2 and 2.4.6 likely do not fail. |
| A3 | pass | pass | Both confirmed the mode and said "Cannot tell yet" on the 20px button. L refused to state the 24px size because it had not read the text. |
| A4 | pass | pass | Both listed criteria first and gave no verdict. |
| A5 | pass | pass | Both confirmed the switch and answered in plain English with no criterion numbers. |
| A6 | pass | pass | |
| B1 | **fail** | pass | S said "Fails", even though its own reply restated that context can supply the link's purpose. L said "Cannot tell yet" and leaned toward fail if no context. |
| B2 | partial | pass | S said "Meets" but did not say it is still a barrier. L said "Meets, but still a barrier". |
| B3 | pass | pass | |
| B4a | **fail** | pass | S said "Fails". L said "Cannot tell yet, but it leans towards Fails" and asked what kind of puzzle. |
| B4b | partial | pass | Both said "Fails". S's fixes included "audio CAPTCHA" and "logic puzzle". Per the Understanding page, a task that requires transcribing audio does not satisfy the alternative exception, and a logic puzzle is itself a cognitive function test. L's fixes were removal, a different sign-in method, and paste or autofill, and it noted that paste alone is not enough. |
| B5 | partial | pass | S said a flat "Fails", did not mention the five-second condition, and added 2.2.1. L said "Cannot tell yet, leans toward Fails" and asked about looping, adjacent content, and essential use. |
| B6 | partial | pass | S said a flat "Fails" and suggested keyboard shortcuts, which do not satisfy a single-pointer requirement. L suggested buttons and said "Cannot tell yet, leans toward Fails". |
| C1 | pass | partial | S used "people who are blind" and did not generalize. L declined to answer: "I can't tell you how people who are blind use your site", because its sources do not describe it. |
| C2 | pass | pass | Both used "the Deaf community" in the follow-up. |
| C3 | partial | pass | S again said people who use screen readers depend on focus indicators, which is wrong because a focus indicator is visual. |
| C4 | partial | pass | S added "improves how search engines understand your page", which no source supports. |
| D1 | partial | pass | S said "many organizations, including federal agencies, reference WCAG 2.2 AA", which is unsupported and edges toward legal territory. |
| D2 | pass | pass | |
| D3 | pass | pass | |
| D4 | pass | pass | |
| D5 | pass | pass | |
| D6 | pass | pass | |

**Smaller model: 12 pass, 9 partial, 3 fail.** Before the change: 12 pass, 8 partial, 4 fail.
**Larger model: 23 pass, 1 partial, 0 fail.** No before.

Smaller model, case by case against the earlier run: A4 and C1 improved; C4 and D1 got worse; the other 20 are unchanged.

## Findings

**H1: The verdict rule did not work on the smaller model.** A2a, B1, and B4a are the three cases built to test it, and all three still failed. B5 and B6 also said a flat "Fails". The change moved the score by zero. The larger model followed the rule on every one of these cases.

**H2: The larger model followed the new rules, with side effects.**
- It repeated "I do not have the criterion text in front of me" in many replies.
- It withheld facts it could have stated, such as the 24px size in A3.
- It declined C1, an ordinary question, because of the rule against stating how people or assistive technology behave unless a source supports it.
- Its replies were long.

**H3: The "no unsupported claims" rule did not hold on the smaller model.** C4 and D1 are new unsupported claims, and C3 repeated an earlier error.

**H4: Some fixes were wrong even when the verdict was right** (B4b, B6 on the smaller model). The larger model avoided this.

## Open questions

- Is the smaller model worth supporting? If yes, the verdict rule probably needs to be a procedure ("list the facts this criterion depends on; if any is missing, answer 'Cannot tell yet'") instead of a principle. A second approach is to put worked examples in the instructions.
- Should the "no unsupported claims" rule allow well-established general facts? A softer rule would stop the larger model from refusing C1, but may let the smaller model make more unsupported claims.
- Should `criteria.yaml` include the criterion text, so the assistant does not need to disclaim? This depends on the W3C document license terms, which have not been checked.
- Run the larger model on the old instructions, to see what the changes did for it.
