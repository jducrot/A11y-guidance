# Re-run 4: verbatim criterion text

Commit `9dc6ba0` added `plugin/criteria-text.yaml`, the verbatim text of every WCAG 2.2 success criterion and the definitions it uses. It also changed `instructions.md`:

- Read each criterion's text and definitions from that file when choosing a verdict.
- Quote wording only from that file, exactly.
- When the user's facts rule out every exception in the text, decide.

This run checks the cases those changes target, on both models. Raw replies are in `rerun-4-raw-replies.md`.

## How this was run, and its limits

- A fresh agent per case, the six plugin files only, no web access, one run per case. Each agent wrote its reply to a file.
- A3 was sent as one message ("WCAG mode on. Is a 20px icon button a problem?") instead of two turns, to keep the run simple. The mode confirmation was not tested here; it passed in earlier runs.
- The environment was the same as in `rerun-3-results.md`. The agents may have run on a different model from the one requested; this was not verified.
- One run per case. The same person wrote the instructions, the expected behaviors, and this scoring.
- Every quotation of criterion text in the replies was checked by script against `criteria-text.yaml`. All of them matched. The script flagged a few other quoted strings, such as example link text ("click here") and the user's own words, which are not WCAG text.

## Scores

S = smaller model, L = larger model. "Before" is the most recent earlier run of each case: `rerun-3-results.md` for A2b, A3, and B4b, and the repeat in `rerun-3-results.md` for the others on S. L's earlier runs of A2a, B1, B4a, B5, and B6 are in `rerun-2-results.md`.

| ID | S before | S now | L before | L now | Notes |
|----|----------|-------|----------|-------|-------|
| A2a | pass | pass | pass | pass | Both said "Cannot tell yet", leaning toward Fails. L quoted 3.3.2 exactly. |
| A2b | partial | **pass** | pass | pass | Both said "Fails" under 4.1.2 and 1.3.1 and quoted the criteria exactly. S had said "Cannot tell yet" before. |
| A3 | pass | pass | pass | pass | Both said "Cannot tell yet", and both now quote the 24 by 24 CSS pixel minimum and name the five exceptions. Before, both declined to give the size. |
| B1 | pass | pass | pass | pass | Both said "Cannot tell yet" and quoted 2.4.4, including the part about link context. |
| B4a | pass | pass | pass | pass | Both said "Cannot tell yet" and quoted the four exceptions of 3.3.8. |
| B4b | partial | **pass** | pass | pass | Both said "Fails" and used the quoted exceptions to show none applies. S had said "Cannot tell yet" before. |
| B5 | pass | pass | pass | pass | Both said "Cannot tell yet", leaning toward Fails. |
| B6 | partial | partial | pass | partial | Both said "Fails". Both quoted the definition of "essential" correctly to rule out that exception. Both ruled out the user agent exception by assuming the team built the list, which the user did not state. The test case expects "Cannot tell yet". See J5. |

**Smaller model: 7 pass, 1 partial.** **Larger model: 7 pass, 1 partial.**

## Findings

**J4: The criterion text fixed the over-hedging.** On A2b and B4b, which give every fact, the smaller model moved from "Cannot tell yet" to "Fails". Both models now state figures from the text, such as the 24 by 24 CSS pixel minimum. The "I have not read the criterion text" disclaimer has gone from criterion answers. One reply still says it has not read an Understanding page, which is accurate.

**J5: B6 may be a test problem, not an assistant problem.** Both models gave the same well-argued "Fails". They read "our drag-and-drop list" as the team's own code, and they ruled out the essential exception using the definition of "essential". A strict reading of the verdict steps says "Cannot tell yet", because the user did not state who built the list. Many accessibility specialists would accept "Fails" here. The maintainer should decide which answer the test expects. Until then, it is scored partial.

**J6: The verdict steps still hold on the under-specified cases.** A2a, B1, B4a, and B5 stayed at "Cannot tell yet" on both models, so access to the full text did not make either model overconfident.

## Open questions

- Decide the expected answer for B6 (see J5).
- Run the plain-English and boundary cases again at some point, since `instructions.md` changed. They do not depend on criterion text, so a regression there is unlikely but not ruled out.
- C3 (the focus indicator error on the smaller model) is still open.
