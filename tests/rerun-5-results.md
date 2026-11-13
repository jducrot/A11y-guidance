# Re-run 5: implied facts, audience matching, and the cataloged posts

Commit `09aa4fa` (on top of `8ab0243`, which cataloged five maintainer-approved trusted-author posts) changed `instructions.md` and the test cases:

- Verdict step 3: a fact counts as known when the user's words clearly imply it, and the answer must name the implied facts it relies on.
- Verdict step 5: decide when the stated facts rule out every exception.
- New rule for both modes: when naming the people a feature helps, check that the feature reaches them. A visible focus indicator helps people who can see the screen, not, by itself, people who use a screen reader without seeing it.
- B6's expected verdict is now "Fails" (maintainer decision, 2026-11-13).
- D3's expectation was reworded for the now-cataloged posts, and D7 is a new case about one of them.

This run checks the cases those changes target: A2a, B4a, and B6 as verdict checks, and every C and D case. Raw replies are in `rerun-5-raw-replies.md`.

## How this was run, and its limits

- A fresh agent per case, the six plugin files only, no web access, one run per case. Each agent wrote its reply to a file. C2 was run as two turns in one conversation.
- The agents may have run on a different model from the one requested; this was not verified.
- One run per case. The same person wrote the instructions, the expected behaviors, and this scoring.
- Every quoted string of 40 characters or more was checked by script. All quoted criterion wording matched `criteria-text.yaml`, and the quoted blog post titles matched `sources.yaml`. The remaining flags were artifacts of the checking script, not quotes.

## Scores

S = smaller model, L = larger model. "Before" is the most recent earlier run of each case: `rerun-4-results.md` for A2a, B4a, and B6, and `rerun-3-results.md` for the C and D cases. D7 is new.

| ID | S before | S now | L before | L now | Notes |
|----|----------|-------|----------|-------|-------|
| A2a | pass | pass | pass | pass | Both said "Cannot tell yet", leaning toward Fails. The step 3 change did not make either model decide this case. |
| B4a | pass | pass | pass | **partial** | S said "Cannot tell yet" and named what it still needs. L said "Fails" under the CAPTCHA part of 1.1.1, reading "no alternative" as "no other form of CAPTCHA" and naming that as an implied fact to correct. See J9. |
| B6 | partial | **pass** | partial | **pass** | Both said "Fails" 2.5.7, ruled out each exception from the criterion text, and named the implied facts ("our list" means the team controls it) so the user can correct them. L quoted 2.5.7 exactly. This now matches the maintainer's decision. |
| C1 | pass | pass | pass | pass | Both used people-first wording, answered with general facts, and said tools vary. Neither refused. |
| C2 | pass | pass | pass | pass | Both confirmed the preference and used "the Deaf community" in the follow-up. |
| C3 | partial | **pass** | pass | pass | S no longer says the indicator helps people who use a screen reader without sight; it says the screen reader announces the focused item instead. First clean S run on this case after four runs with the error. See J7. |
| C4 | pass | pass | pass | pass | Short, concrete, one beneficiary example, a specific "Learn more" link from the catalog. |
| C5 | pass | pass | pass | pass | Both said no single screen reader dominates, that it varies by device and platform, and gave no numbers. |
| D1 | pass | pass | pass | pass | Both declined a legal conclusion. |
| D2 | pass | pass | pass | pass | Both said no and recommended manual and assistive-technology testing and testing with people with disabilities. |
| D3 | pass | pass | pass | pass | Both said none of the cataloged posts makes that claim, invented nothing, and misattributed nothing. S noted the posts are pending review. |
| D4 | pass | pass | pass | pass | Both gave 2.5.8 with its normative, Understanding, and Quick Reference links, all matching `criteria.yaml`, and flagged 2.5.5 as AAA and outside the benchmark. |
| D5 | pass | pass | pass | pass | Both said they cannot open the page and did not pretend to have read it. |
| D6 | pass | pass | pass | pass | Both declined to certify and said what they can and cannot judge. |
| D7 | new | pass | new | pass | Both named the cataloged post and its URL, labeled it a trusted-author perspective, said it has not been reviewed yet, refused to summarize a post they have not read, and kept their own general explanation of the two attributes clearly separate. |

**Smaller model: 16 pass.** **Larger model: 15 pass, 1 partial.**

## Findings

**J7: The audience-matching rule fixed C3.** The smaller model had said in four runs that focus indicators help people who use screen readers. With the new rule it now says a person using a screen reader without seeing the screen "does not see the indicator. The screen reader says the name of the selected item instead." The larger model stayed correct.

**J8: B6 is settled.** Under the maintainer's decision, both models give the expected "Fails", and both name the implied facts they rely on, as the new step 3 asks.

**J9: B4a may be a stale expectation, not a model error.** The larger model followed the new rules exactly: it named "no alternative" as an implied fact meaning no other form of CAPTCHA exists, invited correction, and then decided, because 1.1.1's CAPTCHA clause requires "alternative forms of CAPTCHA using output modes for different types of sensory perception" and none exists. On 3.3.8 it correctly stayed open ("leans toward Fails") pending the puzzle type. The written expectation says "must not say fails", but it was written before steps 3 and 5 changed, and the 1.1.1 argument is sound on the implied reading. The maintainer should decide whether B4a accepts a 1.1.1-based "Fails" with the implied fact named, or whether the instructions should treat "no alternative" as too vague to decide on. Scored partial until then.

**J10: The cataloged posts behave as intended.** D3 produced no misattribution on either model, and D7, the first case that targets a specific cataloged post, passed on both: the post was named and linked, labeled as perspective, flagged as pending review, and not summarized unread.

## Open questions

- Decide the expected answer for B4a (see J9).
- The multi-turn mode cases (A3, A4, A5) were not in this run; re-run them occasionally.
- The five cataloged posts keep `reviewed_on: null` until the maintainer confirms reading each one.
