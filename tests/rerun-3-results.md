# Re-run 3: remaining cases and a repeat

`rerun-2-results.md` ran 9 of the 25 cases after commit `98c1306`. This run covers the other 16 cases on both models, and repeats the five verdict cases on the smaller model. The instructions were not changed between the two runs. Raw replies are in `rerun-3-raw-replies.md`.

## How this was run, and its limits

- Same setup as `rerun-2-results.md`: a fresh agent per case, the five plugin files only, no web access, one run per case. Each agent wrote its reply to a file. A3 to A5 and C2 were one conversation each, one message at a time.
- The environment was the same as in `rerun-2-results.md`, with many more tools loaded into each agent than in `rerun-results.md`. The agents may have run on a different model from the one requested; this was not verified.
- Some agents broke the "Read and Write only" rule. At least one smaller-model agent tried to start a new remote session, which the environment blocked. One larger-model agent ran a harmless shell command. One larger-model agent read only the first 60 lines of `criteria.yaml` at first and read more later. None of this changed a reply file, but it shows the test agents do not always follow the test setup.
- One run per case, plus one repeat for five cases. That is still a small sample.
- The same person wrote the instructions, the expected behaviors, and this scoring. The raw replies are included so it can be checked.

## Scores: the 16 remaining cases

S = smaller model, L = larger model. "Before" is from `rerun-results.md`, which used the instructions before `98c1306`.

| ID | S before | S now | L before | L now | Notes |
|----|----------|-------|----------|-------|-------|
| A1 | partial | pass | pass | pass | S now says screen reader handling "varies by browser and screen reader" instead of stating it as fact. |
| A2b | partial | **partial** | pass | pass | All facts are in the question, so the expected verdict is "Fails". L said "Fails". S said "Cannot tell yet": the snippet could not show a label added by script. |
| A3 | pass | pass | pass | pass | Both confirmed the mode and said "Cannot tell yet". Neither stated the size in pixels, because neither had read the criterion text. |
| A4 | pass | pass | pass | pass | Both listed criteria first and gave no verdict. |
| A5 | pass | pass | pass | pass | Both confirmed the switch and answered in plain English with no criterion numbers. Both linked the specific Understanding page. |
| A6 | pass | pass | pass | pass | |
| B2 | partial | pass | pass | pass | Both said "Meets WCAG 2.2 AA, but is still a barrier". |
| B3 | pass | pass | pass | pass | |
| B4b | partial | **partial** | pass | pass | All facts are in the question, so the expected verdict is "Fails". L said "Fails". S said "Cannot tell yet" because it had not read the criterion's exceptions. It did state the facts that rule them out. |
| C2 | pass | pass | pass | pass | Both used "the Deaf community" in the follow-up. |
| C3 | partial | **partial** | pass | pass | S still lists people who are blind and use a screen reader among the people a focus indicator helps. A focus indicator is visual. |
| D2 | pass | pass | pass | pass | |
| D3 | pass | pass | pass | pass | |
| D4 | pass | pass | pass | pass | |
| D5 | pass | pass | pass | pass | |
| D6 | pass | pass | pass | pass | |

**Smaller model: 13 pass, 3 partial, 0 fail.** Before: 11 pass, 5 partial, 0 fail.
**Larger model: 16 pass.** Before: 16 pass.

## Scores: repeat of the five verdict cases (smaller model)

| ID | Run 2 | Repeat | Notes |
|----|-------|--------|-------|
| A2a | pass | pass | "Cannot tell yet", with Known and Still needed. |
| B1 | pass | pass | "Cannot tell yet". |
| B4a | pass | pass | "Cannot tell yet". Asked whether the puzzle is object recognition. |
| B5 | pass | pass | "Cannot tell yet". Asked whether the carousel keeps running. |
| B6 | pass | **partial** | Said "Fails". It decided for itself that dragging is not essential, which the user did not state, and it did not consider the exception for dragging the browser controls. The steps say a fact counts as known only if the user stated it. |

4 of 5 held. Combined with `rerun-2-results.md`, the smaller model followed the verdict steps in 9 of 10 runs of these cases. Before `98c1306`, it gave a flat "Fails" in all five.

## Findings

**K1: The smaller model now over-hedges when every fact is given.** A2b and B4b state every fact, and the expected verdict is "Fails". The larger model said "Fails" on both. The smaller model said "Cannot tell yet" on both. In B4b, the reason was that it had not read the criterion's exceptions. This is the opposite of the earlier problem. The step "a fact counts as known only if the user stated it" and the rule against paraphrasing unread criterion text push it toward "Cannot tell yet" even when the facts settle the question.

**K2: The verdict change mostly holds on repeat.** The smaller model followed the verdict steps in 9 of 10 runs across the two runs (B6 drifted once).

**K3: No regressions on the larger model.** It passed all 16 remaining cases, as it did before the change.

**K4: The focus indicator error in C3 persists on the smaller model** across four runs with three versions of the instructions.

## What this suggests

- K1 would likely shrink if the assistant had the criterion text. Then it could check the exceptions itself instead of treating them as unknown. That depends on the W3C document license, which has not been checked.
- Another option is to add to the verdict steps: "If the user states every fact a criterion needs, decide. Do not hold back only because you have not read the criterion text." This may push the smaller model back toward guessing, so it needs testing.
- C3 may need a direct example in the plain English rules, for example that a focus indicator helps people who see the screen and use a keyboard.
