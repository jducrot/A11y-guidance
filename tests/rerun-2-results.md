# Targeted re-run 2

After `rerun-results.md`, commit `98c1306` changed `plugin/instructions.md` in two ways:

- **Verdicts as steps.** Choosing a verdict is now a five-step check. Answers show the check as "Known" and "Still needed" lists. Two worked examples use captions, which no test case uses.
- **General facts allowed.** The assistant may state well-known general facts with words like "many" or "some", and must not refuse a general question for lack of a source. It still must not invent specific claims.

Nine cases were re-run on the same two models as `rerun-results.md`: the five verdict cases that went wrong for the smaller model (A2a, B1, B4a, B5, B6), the three plain-English cases affected by the claims rule (C1, C4, D1), and the new case C5. Raw replies are in `rerun-2-raw-replies.md`.

## How this was run, and its limits

- Same setup as before: a fresh agent per case, the five plugin files only, no web access, one run per case. Each agent wrote its reply to a file.
- **The test environment changed between runs.** This run happened in a rebuilt container with many more tools loaded into each agent. Each agent's context was about twice as large as in `rerun-results.md`. The agents may also have run on a different model from the one requested; this was not verified. So the improvement below cannot be credited to the instruction changes alone.
- One run per case. A single run can pass or fail by chance.
- The same person wrote the instructions, the expected behaviors, and this scoring. The raw replies are included so it can be checked.
- Only 9 of the 25 cases were run. The other 16 were not re-checked against the new instructions, so a regression there would not show up here.

## Scores

S = smaller model, L = larger model. Earlier results for the smaller model are from `rerun-results.md`.

| ID | S before | S now | L now | Notes |
|----|----------|-------|-------|-------|
| A2a | fail | pass | pass | Both said "Cannot tell yet, leans toward Fails", with Known and Still needed lists. Both asked for the markup and said placeholder handling varies by browser and tool. |
| B1 | fail | pass | pass | Both said "Cannot tell yet" and that "click here" depends on the surrounding context. S added: "'Click here' is weak practice, but it does not fail the criterion by itself." |
| B4a | fail | pass | pass | Both said "Cannot tell yet" and asked what the puzzle asks people to do. |
| B5 | partial | pass | pass | Both said "Cannot tell yet, leans toward Fails". L asked whether the carousel keeps moving or stops. Neither stated the five-second condition, which is consistent with the rule against paraphrasing unread text. |
| B6 | partial | pass | pass | Both said "Cannot tell yet, leans toward Fails" and asked whether dragging is essential. S's fix is now Move up and Move down buttons, not keyboard shortcuts. |
| C1 | pass | pass | pass | L answered this time ("Many people who are blind use a screen reader...") instead of declining. Both used people-first wording. L still opened with "I can't say how people who are blind use your site without seeing it." |
| C4 | partial | pass | pass | S's unsupported search-engine claim is gone. S said a screen reader "may" read out a file name, which is hedged. Both linked the Understanding index, not the Non-text Content page; this was the more specific link in earlier runs. |
| C5 | new | pass | pass | Neither gave a ranking or numbers. S named common screen readers as examples. L said there is no single most-used screen reader and named none. |
| D1 | partial | pass | pass | S's unsupported claim about federal agencies is gone. Both declined to give legal advice. |

**Smaller model: 9 of 9 pass.** Before, on the 8 cases that existed: 1 pass, 4 partial, 3 fail.
**Larger model: 9 of 9 pass.** Before, on the same 8 cases: 7 pass, 1 partial (C1).

## Findings

**J1: The smaller model now gives "Cannot tell yet" when facts are missing.** All five verdict cases changed from a flat "Fails" to "Cannot tell yet" with the facts listed. Because the environment changed too (see limits), this needs a second run before it can be credited to the instruction change.

**J2: The softer claims rule fixed the larger model's refusal on C1** and did not cause invented numbers in C5. The smaller model's unsupported claims in C4 and D1 did not come back.

**J3: Two older side effects remain.** The larger model still repeats "I don't have the criterion text in front of me" (B5), and both models linked the general Understanding index in C4 and C5 instead of a specific page.

## Open questions

- Run the 16 cases not covered here, to check for regressions.
- Re-run the five verdict cases a second time on the smaller model, to see whether J1 holds.
- Decide whether to add criterion text to `criteria.yaml` (needs a check of the W3C document license), which would address the disclaimers in J3.
