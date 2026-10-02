# Other-model results

A second, smaller model than the one that wrote the plugin answered each case in a fresh conversation. Raw replies are in `other-model-raw-replies.md`.

## How this was run, and its limits

- Each case was a fresh agent that read only the five plugin files (`instructions.md`, `design.md`, `development.md`, `sources.yaml`, `criteria.yaml`). It had no web access and did not read the tests or the README.
- A3–A5 and C2 were multi-turn. The agent received one message at a time.
- There was one run per case. Models are not deterministic, so a single run can pass or fail by chance. Re-run before treating any single result as a rule.
- The author of the expected behaviors also did the scoring, so scoring is not independent. The raw replies are included so it can be checked.
- B3 told the agent to imagine an attached screenshot with no color values. C2 added a follow-up question so there was something to check the wording against.
- Most agents summarized their reply in their final report instead of reproducing it. The scored text comes from their transcripts.
- Criterion levels and rules were checked against the published WCAG 2.2 text, as described in `first-pass-results.md`.
- The agents may have used a model different from the one requested. This was not verified.

## Scores

**Total: 12 pass, 8 partial, 4 fail, out of 24.** The first pass is not a fair comparison: that run was the plugin's author checking its own work, and it had 22 cases.

| ID | Result | What happened |
|----|--------|---------------|
| A1 | partial | Plain English, good fix, specific link. Said placeholder text "isn't announced as a label" to screen readers, which the spec does not say and which varies by browser. Used "ARIA" without defining it. |
| A2a | **fail** | Gave a flat "Fails" with two criteria. Expected "Cannot tell yet". Described 2.4.6 as "form inputs must have labels", which is not what that criterion says. |
| A2b | partial | Correct verdict ("Fails") and cited 4.1.2. But it also put quotation marks around text for 2.4.6 and 3.3.2 that is not the real wording. |
| A3 | pass | Confirmed the mode. Then "Cannot tell yet" on the 20px button, asking about spacing and alternatives. Minor slip: called keyboard a pointer input. |
| A4 | partial | No verdict, as intended. But it asked a list of questions and gave general ideas instead of listing the relevant requirements. |
| A5 | pass | Confirmed the switch, then answered in plain English with no criterion numbers. |
| A6 | pass | Plain English, no criterion numbers, native `select` first. One flag for an expert: it told developers to "trap focus" in a dropdown, which sits oddly with the no-keyboard-trap requirement. |
| B1 | **fail** | "Fails" 2.4.4. The criterion allows the purpose to come from context, and the answer ignored that. Expected "likely meets" or "cannot tell yet". |
| B2 | partial | Right outcome ("meets, but still a barrier"). But it misstated the Level AAA rule as "upper secondary education level or higher"; the rule says more advanced than lower secondary. |
| B3 | pass | "Cannot tell yet". Asked for color values and text size. Correct contrast thresholds. |
| B4a | **fail** | "Fails" 3.3.8 on a vague "puzzle CAPTCHA". Expected "Cannot tell yet". It also paraphrased 3.3.8 in a way that is not the criterion's text. |
| B4b | partial | Right verdict. But its reasoning was about vision and dexterity, not transcription as a cognitive function test. Its fix list included "a logic puzzle", which is itself a cognitive function test. |
| B5 | partial | Flat "Fails" on 2.2.2 without the five-second condition or the essential-activity exception. The "4 seconds" in the question was not examined. |
| B6 | partial | "Fails" 2.5.7 is reasonable. But its suggested fixes included keyboard shortcuts, which do not meet a requirement about single-pointer operation. Did not mention the exceptions. |
| C1 | **fail** | Repeated "blind users" throughout instead of people-first wording. Also overgeneralized ("can't see visual design, color, layout"). |
| C2 | pass | Acknowledged the preference, then used "the Deaf community" in the next answer. |
| C3 | partial | Short sentences and defined terms. But it said people who use screen readers "depend on focus indicators", which is wrong: a focus indicator is visual. |
| C4 | pass | Short, plain, concrete, with a specific link. |
| D1 | pass | Declined to give legal advice. Did not confirm that passing WCAG means ADA compliance. |
| D2 | pass | "No." Explained what automated scans miss and recommended human testing. Gave no percentage. |
| D3 | pass | Said no blog is cataloged. Added an unsourced claim that placeholder labels are "generally considered a barrier". |
| D4 | pass | Gave 2.5.8 and 2.5.5 with links, and the exact Understanding page. |
| D5 | pass | Said it had no web access and asked the user to paste the content. |
| D6 | pass | Declined to certify. "Cannot tell yet", listing what it would need. |

## Findings

**G1: Overconfident verdicts on under-specified questions.** On the three questions that lacked information (A2a, B1, B4a), the model answered "Fails". B5 did the same. The model did choose "Cannot tell yet" for B3 and A3, so it can do it. The instructions allow the verdict but do not push the assistant toward it when the facts are missing. This is the central finding, because the verdict labels were designed for exactly these cases.

**G2: Normative wording is invented.** Four answers misquoted or misparaphrased criteria (A2a, A2b, B2, B4a). `criteria.yaml` holds only metadata, so the model fills in the wording from memory. The instructions say to take numbers, names, levels, and links from the file. They do not say to avoid quoting or paraphrasing the criterion text.

**G3: Plain-language slips.** People-first wording failed in C1. Jargon appeared undefined in A1 ("ARIA"). Two answers (A1, C3) stated user-impact claims that the sources do not support.

**G4: A4 skipped the list of requirements.** The how-to rule says to list relevant requirements, but the model asked questions instead. The instructions also say to ask for context, so the two rules pull in different directions.

**G5: Fix advice can be wrong even when the verdict is right.** B4b and B6 suggested remedies that would not satisfy the criterion. This is a risk for a guidance plugin, and the plugin has no source that holds the right fixes.

**What worked:** Mode switching and confirmation (A3, A5, C2), refusing legal and certification questions (D1, D6), not inventing sources or pages (D3, D5), and asking for color values on contrast (B3).

## Open questions

- These results are for one smaller model, one run per case. A larger model may do better on G1 and G2. It is worth running before changing the instructions.
- Whether adding the normative text to `criteria.yaml` would fix G2 depends on the W3C document license terms. This has not been checked.
