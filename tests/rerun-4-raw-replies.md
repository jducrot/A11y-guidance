# Raw replies, re-run 4

Replies exactly as each agent wrote them to file, one run per case. Each agent read only the six plugin files at commit `9dc6ba0` and had no web access. A3 was sent as a single message: "WCAG mode on. Is a 20px icon button a problem?". See `rerun-4-results.md` for scoring and caveats.

## Smaller model

### A2a

> Verdict: Cannot tell yet. It leans toward Fails.
>
> Criteria that could apply (both Level A, so they are part of the AA benchmark):
>
> - 3.3.2 Labels or Instructions, Level A. Link: https://www.w3.org/TR/WCAG22/#labels-or-instructions. It covers whether a field that needs input has a label or instructions. The criterion says: "Labels or instructions are provided when content requires user input."
> - 4.1.2 Name, Role, Value, Level A. Link: https://www.w3.org/TR/WCAG22/#name-role-value. It covers whether the field has a name that software can read. The criterion says: "the name and role can be programmatically determined".
>
> Known:
> - The field collects information from the user.
> - The only text that identifies the field is a placeholder. You stated this.
>
> Still needed:
> - Whether the field has a programmatic name in the code, such as a label element, aria-labelledby, or aria-label. I cannot see the markup. A placeholder alone may or may not give the field a name, and that varies by browser and assistive technology.
> - Whether a visible label or instructions for the field appear anywhere else on the page.
>
> Why it leans toward Fails: a placeholder disappears as soon as the person types. If there is no other label and no programmatic name, 3.3.2 is not met.
>
> Who may be affected: some people who use a screen reader may hear no name for the field. Some people with low vision, memory or attention difficulties may lose track of what the field asks for once they start typing.
>
> Suggested fix (design and development):
> - Design: add a visible text label above the field. Keep the placeholder only as an example, for instance "for example, 1 May 2026".
> - Development: connect the label to the input with a label element, so the field has a name in the code. Check that the label stays visible when the field has a value.
> - Check the fix against 3.3.2 and 4.1.2 by confirming the label is visible and the field's name is announced by a screen reader.
>
> Sources:
> - W3C WCAG 2.2 (normative, the requirement itself): https://www.w3.org/TR/WCAG22/ (reviewed 2026-09-29).
> - Understanding WCAG 2.2 (informative, explains the criteria): https://www.w3.org/WAI/WCAG22/Understanding/ (reviewed 2026-09-29). I have not read its page on this topic in this conversation.
>
> Testing: test the form with a keyboard and with the screen reader your users use. Include people with disabilities in testing. Automated checks alone may not show whether the field has a usable name.
>
> This is guidance, not a conformance check. The verdict can change once the markup is known.

### A2b

> **Verdict: Fails WCAG 2.2 AA.**
>
> WCAG mode, for this question only.
>
> Criteria that apply:
>
> - **4.1.2 Name, Role, Value** (Level A). Link: https://www.w3.org/TR/WCAG22/#name-role-value. The criterion says: "the name and role can be programmatically determined." This input has no name that software can read, so it fails.
> - **1.3.1 Info and Relationships** (Level A). Link: https://www.w3.org/TR/WCAG22/#info-and-relationships. The criterion says: "Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text." The link between "Email" and the field exists only by position on screen, not in the code, so it fails.
>
> Level A criteria are part of the WCAG 2.2 Level AA benchmark, so these failures count against AA.
>
> Known:
> - The input has no label element, aria-label, aria-labelledby, title, or placeholder.
> - The word "Email" is plain text and is not linked to the input.
>
> Still needed:
> - Nothing, for the markup as you described it. One check before you rely on this: if a script sets a name when the page loads, the field would have a name and this verdict would not hold. Check the accessible name in the browser's developer tools on the live page.
>
> Who is affected: many people who are blind use a screen reader, which reads the page aloud. With no name, the screen reader may announce only that this is an empty text field, so the person may not know what to type. What is read varies by screen reader and browser, so test it.
>
> Fix (development): connect the visible text to the input with a label element.
>
> ```html
> <label for="email">Email</label>
> <input type="text" id="email">
> ```
>
> Matching `for` and `id` gives the field its name, and the visible "Email" becomes its label. This fixes 4.1.2 and 1.3.1 for this field.
>
> Also check: 1.3.5 Identify Input Purpose (Level AA), https://www.w3.org/TR/WCAG22/#identify-input-purpose. It may apply because this field collects an email address. Adding `autocomplete="email"` may help, but I have not checked it against the Input Purposes list, which is not in the reference material I used. So I cannot give a verdict on 1.3.5 here.
>
> Scope: this verdict covers this one field as you described it, not the whole page or product.
>
> Sources:
> - Normative: WCAG 2.2 success criteria 4.1.2 and 1.3.1, https://www.w3.org/TR/WCAG22/ (reviewed).
> - Informative: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/. It explains these criteria and adds no requirements.
>
> Testing: test the field with a screen reader and with the keyboard only. Automated checks can flag a missing name, but they cannot confirm that the field is usable.

### A3

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward "Fails WCAG 2.2 AA" if the clickable area is 20 by 20 CSS pixels and no exception applies.
>
> **Criteria that could apply**
>
> - **2.5.8 Target Size (Minimum), Level AA.** This is the main one. Link: https://www.w3.org/TR/WCAG22/#target-size-minimum
> - **4.1.2 Name, Role, Value, Level A.** Check that the button has an accessible name. Icon-only buttons often have none.
> - **1.4.11 Non-text Contrast, Level AA.** Check the icon's contrast against its background if the icon is what tells people the button exists.
>
> 2.5.5 Target Size (Enhanced) is Level AAA, so it is not part of the AA benchmark and I have not used it.
>
> **The criterion text (2.5.8, from criteria-text.yaml)**
>
> "The size of the target for pointer inputs is at least 24 by 24 CSS pixels, except when:" Then the exceptions are: Spacing, Equivalent, Inline, User Agent Control, and Essential.
>
> **Known**
>
> - The button is an icon button.
> - The button is 20px.
>
> **Still needed for 2.5.8**
>
> - Is the 20px the clickable area, in CSS pixels? The target is the region that accepts a pointer action. It can be larger than the visible icon. If padding makes the clickable area 24 by 24 or more, this criterion is met.
> - If the clickable area is smaller than 24 by 24: is the Spacing exception met? A 24 CSS pixel circle centered on the button must not touch any other target.
> - Is there an equivalent control on the same page that is at least 24 by 24?
> - Is the button inside a sentence or block of text?
> - Is the size set by the browser, not by the site's own code?
> - Is the small size essential? This is rare for an icon button.
>
> **Still needed for 4.1.2 and 1.4.11**
>
> - What accessible name does the button have? Check it with a screen reader.
> - What is the icon's contrast ratio against its background?
>
> **Who is affected**
>
> Many people with limited hand control, tremor, or low dexterity find small targets hard to hit. Some people who use a touch screen also miss small buttons and hit a neighbor by mistake. Even if the spacing exception is met, a 20px button packed close to other controls can still be a barrier. WCAG does not require it, but it still blocks people.
>
> **Fix, if the clickable area is too small (design and development)**
>
> Keep the 20px icon, and add padding so the clickable area is at least 24 by 24 CSS pixels. For example, 2px of padding on each side gives a 24px area. Check the final size in the browser's developer tools, measuring the clickable area and not only the icon. This fix would satisfy 2.5.8 because the area that accepts a tap or click is 24 by 24.
>
> **Testing**
>
> Test the button with a mouse and with touch on a real device. Test it with the screen reader your users use, and include people with motor disabilities. Automated checks alone cannot show that this button is usable.
>
> **Sources**
>
> - **Normative:** WCAG 2.2 success criteria 2.5.8, 4.1.2, and 1.4.11, at the W3C links above. The 2.5.8 wording is quoted from criteria-text.yaml.
> - **Informative:** Understanding Target Size (Minimum), https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html. I did not open this page in this conversation, so I have not quoted it.

### B1

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if the link text is the only clue to where the link goes.
>
> **Criterion that applies**
> - 2.4.4 Link Purpose (In Context), Level A
> - Normative text: "The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context, except where the purpose of the link would be ambiguous to users in general."
> - Normative link: https://www.w3.org/TR/WCAG22/#link-purpose-in-context
> - Informative link (Understanding WCAG 2.2): https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html
>
> **Not part of the AA benchmark**
> - 2.4.9 Link Purpose (Link Only), Level AAA. It requires the purpose to be clear from the link text alone. It is outside WCAG 2.2 Level AA, so it does not decide this question.
>
> **Known**
> - The link text is "click here".
>
> **Still needed**
> - The text that is tied to the link, such as the sentence, list item, or heading it belongs to. The criterion allows this context to help, but only when it is programmatically related to the link.
> - Where the link goes. Whether a person can tell that before clicking depends on the whole page, not only the link. The exception applies only when the purpose is ambiguous to users in general, meaning it cannot be told from the link and the rest of the page.
> - Whether the page has several "click here" links that go to different places. If so, the context usually has to tell them apart.
>
> **Why it leans toward Fails**
> "Click here" on its own does not say what happens when someone activates it. If the surrounding text does not say where the link goes, the criterion is likely not met. If the sentence says, for example, "Read the refund policy: click here", the criterion is likely met.
>
> **A fix to consider now**
> - Make the link text name its destination, for example "Read the refund policy". This works whatever the context. Design should write the text. Development should make sure the accessible name starts with the same words the user sees.
>
> **Testing**
> - Check the links with a screen reader, reading the links list and the link in its sentence. Also test with people who use screen readers, because a link list can reveal problems that a sighted check misses.
>
> To finish the verdict, send the sentence or section around the link, and where the link goes. If you can share the markup or a screenshot, that helps too.

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward **Fails WCAG 2.2 AA** under 3.3.8.
>
> **Criteria that could apply**
>
> - **3.3.8 Accessible Authentication (Minimum)**, Level AA. https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum. It covers login steps that require a cognitive test, such as solving a puzzle, unless one of four listed exceptions applies.
> - **1.1.1 Non-text Content**, Level A. https://www.w3.org/TR/WCAG22/#non-text-content. Its CAPTCHA case sets extra conditions for a CAPTCHA.
>
> **Wording used (normative)**
>
> - 3.3.8: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:" The four options are Alternative, Mechanism, Object Recognition, and Personal Content.
> - The definitions say that "solving of puzzles" is a cognitive function test.
> - 1.1.1, CAPTCHA case: "If the purpose of non-text content is to confirm that content is being accessed by a person rather than a computer, then text alternatives that identify and describe the purpose of the non-text content are provided, and alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
>
> **Known**
>
> - The login step asks users to solve a puzzle CAPTCHA.
> - No alternative to the puzzle is offered.
> - The puzzle is a CAPTCHA, so its purpose is to confirm that a person is signing in.
>
> **Still needed**
>
> - Whether the puzzle is always required to sign in, or only appears in some cases, such as after unusual activity. 3.3.8 applies only to a step the user must complete.
> - Whether the login step offers another sign-in method that does not depend on a cognitive test, such as a passkey or a sign-in link. An exception applies if one exists.
> - Whether the puzzle is object recognition, such as "select the pictures that show a bicycle", or uses personal content the user provided. Either would be an exception.
> - Whether any mechanism helps a person complete the puzzle itself. The criterion's notes give examples such as password managers and copy and paste, but those help with typing a password, not with a puzzle.
> - Whether the puzzle is non-text content, such as an image or a graphic. It probably is, but this should be confirmed.
> - Whether the CAPTCHA has a text alternative that identifies and describes its purpose, and whether it has alternative forms that use other senses, such as sound. The user has said there is no alternative, so the CAPTCHA case in 1.1.1 is not met on that point.
>
> **Who may be affected**
>
> - Many people with cognitive disabilities find puzzles hard or impossible to solve.
> - Some people who are blind or have low vision cannot see a visual puzzle at all.
> - Some people with motor disabilities cannot complete drag or precise-tap puzzles.
>
> **Concrete fix**
>
> - Offer at least one sign-in method that does not need a puzzle, such as a passkey or a sign-in link sent by email. Note that an emailed code the user must type may still count as a cognitive function test, because the definition lists transcription as one. A passkey or a link avoids that.
> - Show the puzzle only when it is needed, if the design allows, and make sure the sign-in still works without it.
> - Give the CAPTCHA a text description of its purpose, and add an alternative form that uses another sense, such as sound.
> - Whoever makes the change: design should decide the sign-in options, and development should build the alternative methods and the text.
>
> **Scope**
>
> - 3.3.9 Accessible Authentication (Enhanced) is Level AAA. It is not part of the AA benchmark.
>
> **Next steps**
>
> - Test the login with a keyboard, a screen reader, and a voice input tool, and with people with disabilities. Automated checks cannot show that this step is accessible.
> - Send the answers to the "Still needed" list, and I can give a verdict.
>
> This is guidance. It is not a conformance certification.

### B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criterion: 3.3.8 Accessible Authentication (Minimum), Level AA.** It is new in WCAG 2.2. Normative text: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>
> The criterion says: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:"
>
> Known:
> - Signing in requires typing the characters from a distorted CAPTCHA. Typing characters is a transcription task, which the criterion's definition of a cognitive function test includes.
> - There is no other way to sign in, so there is no alternative method.
> - The answer cannot be pasted or autofilled, so there is no mechanism that helps the user complete the test.
> - The CAPTCHA does not ask the user to recognize objects or to identify content they provided, so neither of those options applies.
>
> Still needed: nothing. Each option is ruled out by the facts you gave, so this verdict does not depend on anything else.
>
> **Also applies: 1.1.1 Non-text Content, Level A.** Normative text: https://www.w3.org/TR/WCAG22/#non-text-content
>
> The CAPTCHA exception in this criterion requires that "alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
>
> Known: the CAPTCHA is described as distorted text only.
>
> Still needed: whether an audio or other non-visual form of the CAPTCHA exists. If none exists, this criterion also fails. Verdict for this criterion: Cannot tell yet. It leans toward Fails.
>
> **Sources**
> - Normative: the WCAG 2.2 success criteria above.
> - Informative: Understanding 3.3.8, https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html. It explains the criterion and adds no requirements.
>
> **Fix (design and development)**
> - Add a way to sign in that does not need a cognitive function test. Options include a passkey, a sign-in link sent to the user's email address, or single sign-on. Check that each option works with a keyboard and a screen reader.
> - A one-time code that users must type from an email or an app is also a transcription task. It counts as an alternative only if users can paste or autofill it.
> - Changing how distorted the CAPTCHA text is does not fix 3.3.8. The test is still there.
> - For 1.1.1, add a non-visual form of the CAPTCHA. An audio CAPTCHA that users must type back is still a transcription test, so it also needs one of the 3.3.8 options.
>
> **Testing**
> Test the sign-in step with people who are blind, have low vision, have dyslexia or other cognitive disabilities, or use a switch or voice input. Also test it with a keyboard only and with a screen reader. Automated checks cannot show whether sign-in works for these people.
>
> **Boundaries**
> This is guidance for a web product, measured against WCAG 2.2 Level AA. It is not a certification, a guarantee of conformance, or legal advice.

### B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails.
>
> **Criterion that applies**
> - 2.2.2 Pause, Stop, Hide, Level A (in scope). Normative text: https://www.w3.org/TR/WCAG22/#pause-stop-hide
>
> The criterion says: "For any moving, blinking or scrolling information that (1) starts automatically, (2) lasts more than five seconds, and (3) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it unless the movement, blinking, or scrolling is part of an activity where it is essential."
>
> "Essential" means: "if removed, would fundamentally change the information or functionality of the content, and information and functionality cannot be achieved in another way that would conform."
>
> **Known**
> - The carousel starts moving on its own.
> - It changes slides every 4 seconds and keeps going, so the movement lasts well over 5 seconds. Each slide is 4 seconds, but the rotation does not end.
> - There is no pause button.
>
> **Still needed**
> - Whether the carousel sits alongside other content on the page. This is likely, but it needs confirming.
> - Whether any other control or setting lets the user stop or hide the carousel. A control elsewhere on the page would count only if it actually stops the movement.
> - Whether the carousel is essential to the activity. A rotating set of promotions usually is not essential, but this has to be confirmed, not assumed.
>
> If the answers are "yes", "no", and "not essential", the carousel fails 2.2.2. If it is essential, or another mechanism stops it, the verdict changes.
>
> **Sources**
> - Normative: the WCAG 2.2 text for 2.2.2 above.
> - Informative: Understanding 2.2.2, https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html. I have not opened this page in this conversation, so I cannot quote it.
>
> **Concrete fix (design and development)**
> - Design: add a visible Pause button near the top of the carousel, with a clear label such as "Pause slideshow". Put it where people will see it before the first slide changes.
> - Development: build it as a real button that works with the keyboard and has a name. Update its label or state (for example "Play slideshow" when paused) so a screen reader announces the change.
> - When the user pauses, the carousel should stop and stay stopped until the user starts it again. Slides should not resume on their own.
> - Another option is to stop the auto-advance altogether and let people move between slides with Previous and Next buttons. This also satisfies the criterion, because nothing moves on its own.
>
> Auto-moving content can be hard for some people to use. For example, some people with low vision, some people who read slowly, and some people with attention difficulties may not finish reading a slide before it changes. Not every person in these groups has this problem, so test it with them.
>
> **Testing**
> - Check the pause control with the keyboard only and with a screen reader.
> - Check that the carousel stays paused after the user pauses it.
> - Test with people with disabilities. Automated checks cannot show whether this works for them.
>
> If you tell me whether the carousel is on a page with other content, whether anything else can stop it, and whether it is essential to the task, I can give a verdict.

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Fails WCAG 2.2 AA.** This assumes the list is on a web page, which is the scope of this guidance.
>
> **Evidence**
>
> - **2.5.7 Dragging Movements (Level AA).** Normative: https://www.w3.org/TR/WCAG22/#dragging-movements
>   Criterion text: "All functionality that uses a dragging movement for operation can be achieved by a single pointer without dragging, unless dragging is essential or the functionality is determined by the user agent and not modified by the author."
> - **2.1.1 Keyboard (Level A).** Normative: https://www.w3.org/TR/WCAG22/#keyboard
>   Criterion text: "All functionality of the content is operable through a keyboard interface without requiring specific timings for individual keystrokes, except where the underlying function requires input that depends on the path of the user's movement and not just the endpoints."
>
> **Known**
>
> - Items in the list can be reordered only by dragging them.
> - There is no other way to reorder items. That includes the keyboard.
> - Your team built the list, so the browser does not control how it works.
> - Reordering uses a pointer, such as a mouse or a finger.
>
> **Still needed**
>
> - Nothing that would change this verdict.
>
> **Why the exceptions do not apply**
>
> - Dragging is not essential. Reordering can be done with a click or tap, so the function can be achieved another way that conforms. The criterion's definition of "essential" applies only when the function "cannot be achieved in another way that would conform."
> - The user agent exception does not apply, because your team controls the list.
> - The keyboard exception covers only functions that need input along a path. Moving an item needs only a start and an end position, so it does not apply.
>
> **Who is affected**
>
> - People who cannot make a steady drag, such as some people with limited hand control, tremor, or other motor disabilities, cannot reorder items at all.
> - People who use a keyboard, including many people who are blind and use a screen reader, cannot reorder items.
>
> **Fix (design and development)**
>
> 1. Design: add a single click or tap control for each item, such as "Move up" and "Move down" buttons or a "Move" menu. You can keep dragging for mouse users, but the control must work without it.
> 2. Development: use native button elements, so the keyboard can reach and press them. Keep a visible focus state. Give each button a name that says what it does and which item it moves, for example "Move Quarterly report up".
> 3. Development: make each new button at least 24 by 24 CSS pixels, or meet one of the exceptions in Target Size (Minimum), Level AA. Normative: https://www.w3.org/TR/WCAG22/#target-size-minimum
> 4. Good practice, not a requirement: after a move, state the new position in text, for example "Quarterly report moved to position 3 of 7", so screen reader users hear the result. Status Messages (Level AA) covers messages like this: https://www.w3.org/TR/WCAG22/#status-messages
>
> **Testing**
>
> - Test the reorder with the keyboard alone, with a screen reader, and by touch on a phone.
> - Include people with disabilities in testing. Automated checks cannot show whether this works for them.
>
> **Sources**
>
> - Normative: WCAG 2.2 success criteria 2.5.7 and 2.1.1, linked above.
> - Informative: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/ (explains the criteria and adds no requirements).
>
> This is guidance, not a conformance certification.

## Larger model

### A2a

> **Verdict: Cannot tell yet.** A placeholder-only input does not automatically fail WCAG 2.2 AA. Whether it fails depends on facts you have not given me. It leans toward Fails if the placeholder is the only thing that identifies the field and it is not exposed as the field's name, or if it is too faint to read.
>
> **Criteria that could apply**
>
> - 3.3.2 Labels or Instructions (Level A): "Labels or instructions are provided when content requires user input." Informative: https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html
> - 4.1.2 Name, Role, Value (Level A): covers whether the name and role of a form field can be programmatically determined (that is, read by software, including assistive technology). Normative: https://www.w3.org/TR/WCAG22/#name-role-value
> - 1.1.1 Non-text Content (Level A): for a control that accepts input, it has a name that describes its purpose. Normative: https://www.w3.org/TR/WCAG22/#non-text-content
> - 1.3.1 Info and Relationships (Level A): information and relationships shown visually can be programmatically determined or are available in text. Normative: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - 1.4.3 Contrast (Minimum) (Level AA): placeholder text counts as text, so it needs enough contrast. Normative: https://www.w3.org/TR/WCAG22/#contrast-minimum
> - 2.4.6 Headings and Labels (Level AA): labels describe topic or purpose. Normative: https://www.w3.org/TR/WCAG22/#headings-and-labels
> - 2.5.3 Label in Name (Level A): applies if a visible label exists, so the name must contain the visible text. Normative: https://www.w3.org/TR/WCAG22/#label-in-name
>
> **Known**
>
> - The input has a placeholder.
> - The input has no other visible label.
>
> **Still needed**
>
> - What the placeholder says. Does it clearly identify the field (for example "Email address") or is it only an example (for example "name@example.com")?
> - Whether the field has an accessible name in the browser's accessibility tree, and where it comes from. Browsers and assistive technologies differ in whether they use a placeholder as a name, so this must be tested.
> - The color contrast between the placeholder text and its background. Placeholder text is often light gray.
> - Whether the placeholder disappears when someone starts typing or focuses the field, and whether any other label or instruction stays visible.
> - Whether any other label or instruction exists that you did not mention, such as text near the field or a hidden label.
> - The markup for the input.
>
> **Which way it leans**
>
> - 3.3.2 only asks that a label or instruction is provided. The WCAG definition of "label" is "text or other component with a text alternative that is presented to a user to identify a component within web content". A clear, visible placeholder might meet that wording on its own. I cannot confirm this from your description.
> - 4.1.2 and 1.1.1 are where placeholder-only fields most often fail, if the field ends up with no name that software can read.
> - 1.4.3 is a common failure, because faint placeholder text often misses the contrast ratio the criterion sets.
>
> **Meets the requirement vs. still a barrier**
>
> Even when a placeholder-only field meets the criteria, it can still be a barrier. The hint vanishes once someone types. People with memory or attention difficulties may forget what the field asked for. People who use screen magnification may not see the hint. People may also mistake the placeholder for a value that is already filled in. WCAG does not forbid placeholders, but a visible label that stays on screen avoids these problems. This is good practice, not a WCAG requirement.
>
> **Concrete fix**
>
> - Development: add a visible label tied to the input (for example with a `label` element and `for` attribute). Keep the placeholder for a short example only, if you need it.
> - Design: keep the label visible at all times, and make any placeholder text meet the contrast ratio.
> - Test with a keyboard, with a screen reader, and with people with disabilities. Automated checks alone cannot tell you the field is usable.
>
> Sources: the WCAG 2.2 success criteria are normative. The Understanding page is informative and adds no requirements.
>
> This is guidance only. It is not a certification of conformance. Send me the markup and the placeholder text and I can give a firmer verdict.
>
> I am answering in WCAG mode for this question only. I will go back to plain English after this answer.

### A2b

> **Verdict: Fails WCAG 2.2 AA.**
>
> Evidence: the text field has no programmatic name. The word "Email" is only nearby text. Software, such as a screen reader, cannot tell that "Email" belongs to the field.
>
> **Criteria checked**
>
> - 4.1.2 Name, Role, Value (Level A, so it is part of AA). This is the main failure. The normative text says: "For all user interface components (including but not limited to: form elements, links and components generated by scripts), the name and role can be programmatically determined". A text input is a user interface component. Its name must be exposed to software. Here it has no name. This criterion's own note says standard HTML controls meet it "when used according to specification". An unlabeled input is not used that way. Link: https://www.w3.org/TR/WCAG22/#name-role-value
> - 1.3.1 Info and Relationships (Level A). This is a second failure. The normative text says: "Information, structure, and relationships conveyed through presentation can be programmatically determined or are available in text." Sighted people see "Email" beside the field and link the two. That link is not in the markup. Link: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - 3.3.2 Labels or Instructions (Level A). Checked, not a failure on these facts. The normative text says: "Labels or instructions are provided when content requires user input." A visible label is provided. The problem is that it is not connected to the field, which the two criteria above cover. Link: https://www.w3.org/TR/WCAG22/#labels-or-instructions
>
> **Known**
>
> - It is an `<input type="text">` that people type into.
> - It has no `<label>`, `aria-label`, `aria-labelledby`, `title`, or placeholder.
> - "Email" is visible next to it as plain text and is not associated with the input.
>
> **Still needed**
>
> - Nothing that changes the verdict. These criteria have no exception that applies to a visible, usable text field with no name.
> - One assumption: the markup you gave is what the browser ends up with. If a script adds a name after the page loads, check the final page, not the source code.
>
> **Who is affected**
>
> Many people who are blind use a screen reader, which reads the page aloud. On this field it may only say something like "edit text". People who use voice control may not be able to say the field's name to reach it. Some people with motor disabilities cannot click the visible word "Email" to move focus into the field.
>
> **Fix (development)**
>
> Use a native label:
>
> ```html
> <label for="email">Email</label>
> <input type="text" id="email">
> ```
>
> This gives the field a name. It satisfies 4.1.2 and 1.3.1. It also makes the word "Email" clickable, so it focuses the field. Prefer this to ARIA. If you must use `aria-label`, it should contain the visible text "Email". Criterion 2.5.3 Label in Name (Level A) asks that the name contain the visible label text. Link: https://www.w3.org/TR/WCAG22/#label-in-name
>
> Good practice, not a requirement from these criteria: use `type="email"` and `autocomplete="email"`. This helps browsers show the right keyboard and fill in the value. Whether 1.3.5 Identify Input Purpose (Level AA) applies depends on whether this field collects the user's own email address. You did not say, so I have not decided that.
>
> **Test it**
>
> Check with a screen reader on the browsers and devices you support. Check that voice control can select the field by saying "Email". Automated checkers usually catch a missing label, but they cannot show that the name makes sense. Test with people with disabilities too.
>
> **Sources**
>
> - Normative: WCAG 2.2, the success criterion text linked above. https://www.w3.org/TR/WCAG22/
> - Informative (explains, adds no requirements): Understanding Name, Role, Value https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html and Understanding Info and Relationships https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html
>
> This is guidance on one snippet. It does not certify the page or the product, it is not legal advice, and it does not show that the rest of the page meets WCAG.

### A3

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if the clickable area is 20 by 20 CSS pixels and nothing else makes up for it.
>
> **Criterion that applies**
>
> - 2.5.8 Target Size (Minimum), Level AA. It covers how big a pointer target must be. Pointer inputs are mouse, pen, or touch. [Normative text](https://www.w3.org/TR/WCAG22/#target-size-minimum)
>
> The criterion says: "The size of the target for pointer inputs is at least 24 by 24 CSS pixels, except when:"
>
> - "Spacing: Undersized targets (those less than 24 by 24 CSS pixels) are positioned so that if a 24 CSS pixel diameter circle is centered on the bounding box of each, the circles do not intersect another target or the circle for another undersized target;"
> - "Equivalent: The function can be achieved through a different control on the same page that meets this criterion;"
> - "Inline: The target is in a sentence or its size is otherwise constrained by the line-height of non-target text;"
> - "User Agent Control: The size of the target is determined by the user agent and is not modified by the author;"
> - "Essential: A particular presentation of the target is essential or is legally required for the information being conveyed."
>
> The criterion measures the target, not the icon. A target is the "region of the display that will accept a pointer action, such as the interactive area of a user interface component". A 20px icon inside a button with padding can still be 24 by 24 or larger.
>
> **Known**
>
> - You describe a "20px icon button".
>
> **Still needed**
>
> - Is the whole clickable area 20 by 20 CSS pixels, or is 20px only the icon size? Include any padding. Unit matters: the criterion uses CSS pixels.
> - If the clickable area is under 24 by 24: how close is the nearest other target? Check whether a 24px circle centered on each undersized target would overlap another target or another undersized target's circle.
> - Is the same function available through another control on the same page that is at least 24 by 24?
> - Is the button inside a sentence or otherwise limited by the line height of surrounding text?
> - Is its size set by the browser and not changed by your styles?
> - Is this exact presentation essential or legally required?
>
> **Where it leans**
>
> - If the clickable area is 20 by 20, it has spacing from other targets, and nothing else applies, it meets 2.5.8.
> - If the clickable area is 20 by 20, sits close to other controls (for example in a toolbar), has no equivalent control, and none of the other exceptions apply, it fails 2.5.8.
> - If the clickable area is 24 by 24 or larger, the size requirement is met.
>
> **Meeting the minimum is not the same as easy to use.** Small targets are hard to hit for many people, including some people with hand tremors or limited fine motor control, and people using touch on a small screen. A 24px target can meet WCAG and still be a barrier. Level AAA criterion 2.5.5 Target Size (Enhanced) asks for 44 by 44 CSS pixels. It is not part of the AA benchmark, but it is a useful goal. [Informative: Understanding Target Size (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
>
> **Fix if you need one**
>
> - Design and development: make the interactive area at least 24 by 24 CSS pixels. Add padding to the button, and keep the icon at 20px if you like. Larger is better where space allows.
> - Check that the bigger area does not overlap neighboring controls.
>
> **Other checks for an icon-only button (not decided here)**
>
> - Name: it needs an accessible name that describes its purpose (1.1.1 Non-text Content, Level A, and 4.1.2 Name, Role, Value, Level A).
> - Contrast: the icon needs enough contrast against its background (1.4.11 Non-text Contrast, Level AA).
>
> **Sources**
>
> - Normative: [WCAG 2.2, Target Size (Minimum)](https://www.w3.org/TR/WCAG22/#target-size-minimum)
> - Informative: [Understanding Target Size (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html) and [How to Meet WCAG](https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum)
>
> Send the button's CSS (width, height, padding), what sits next to it, and a screenshot of the row, and I can give a firmer verdict. Please also test with touch on a real device and with people who have motor disabilities. Automated checks alone cannot show this is usable.
>
> This is guidance, not certification, and not legal advice.

### B1

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if nothing near each link says what the link does.
>
> **Criterion that applies**
> - 2.4.4 Link Purpose (In Context), Level A. It covers whether people can tell what a link does, either from the link text alone or from the link text together with its programmatically determined context.
> - Normative text: https://www.w3.org/TR/WCAG22/#link-purpose-in-context
>
> The criterion reads: "The purpose of each link can be determined from the link text alone or from the link text together with its programmatically determined link context, except where the purpose of the link would be ambiguous to users in general."
>
> "Click here" is a poor and discouraged way to write a link. But that does not fail the criterion by itself. The criterion allows the purpose to come from context. So the verdict depends on the context around each link.
>
> **Known**
> - The link text is "click here".
>
> **Still needed**
> - What surrounds each link in the markup. Does the same sentence, paragraph, list item, table cell, or heading say what the link does? Or is there an accessible name or description that does? WCAG defines this context as "additional information that can be programmatically determined from relationships with a link, combined with the link text, and presented to users in different modalities". A note in that definition says screen readers can give the context of the current sentence when focus is on a link in that sentence.
> - Whether the "ambiguous to users in general" exception could apply. It applies only when "readers without disabilities would not know what a link would do until they activated it". If the purpose is unclear to everyone, even with the whole page in view, that exception may apply.
> - Whether the links stand alone (for example, a row of links that all say "click here") or sit inside a sentence that names the destination.
>
> **Which way it leans**
> - Likely Fails: links that stand alone, or several "click here" links on one page with no nearby text saying where each goes.
> - Likely meets: a link inside a sentence such as "To read the return policy, click here", if the sentence is the link's parent text in the markup.
>
> **Even if it meets WCAG, it can still be a barrier**
> - Many people who use a screen reader (software that reads the page aloud) pull up a list of all links on a page. A list of "click here, click here, click here" tells them nothing.
> - "Click" also assumes a mouse. People use keyboards, touch screens, and voice control too.
>
> **Fix (content and design, with development)**
> - Write link text that names the destination or action, for example "Read the return policy". This satisfies 2.4.4 on its own, because the purpose is clear from the link text alone.
> - If you cannot change the visible text, put the purpose in the same sentence or paragraph as the link, or give the link an accessible name that includes it. Keep the visible words inside the accessible name.
> - Note: 2.4.9 Link Purpose (Link Only) is Level AAA. It is not part of the AA benchmark. It would require the purpose to be clear from the link text alone.
>
> **To give a firm verdict**, send the markup for a few of these links with the text around them. Then test with a screen reader's links list and with keyboard-only use. Automated checks can flag the phrase "click here", but they cannot judge whether the context is enough.
>
> **Sources**
> - Normative: WCAG 2.2, 2.4.4 Link Purpose (In Context), Level A. https://www.w3.org/TR/WCAG22/#link-purpose-in-context
> - Informative: Understanding 2.4.4. https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html
> - Informative: How to Meet 2.4.4 (Quick Reference). https://www.w3.org/WAI/WCAG22/quickref/#link-purpose-in-context
>
> This is guidance, not a certification or legal advice.

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails WCAG 2.2 AA, because a puzzle with no alternative is the situation 3.3.8 is written to catch.
>
> **Criteria that could apply**
>
> - 3.3.8 Accessible Authentication (Minimum), Level AA. It covers whether a login step makes people pass a cognitive function test. Normative text: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - 1.1.1 Non-text Content, Level A. It has a CAPTCHA exception that says what a CAPTCHA must provide. Normative text: https://www.w3.org/TR/WCAG22/#non-text-content
>
> **3.3.8 Accessible Authentication (Minimum)**
>
> The text reads: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:"
>
> - "Alternative: Another authentication method that does not rely on a cognitive function test."
> - "Mechanism: A mechanism is available to assist the user in completing the cognitive function test."
> - "Object Recognition: The cognitive function test is to recognize objects."
> - "Personal Content: The cognitive function test is to identify non-text content the user provided to the website."
>
> Known:
> - The puzzle is part of the login, so it is a step in an authentication process.
> - Solving a puzzle is a cognitive function test. The definition lists "solving of puzzles".
> - There is no alternative. This rules out the Alternative exception.
>
> Still needed:
> - Whether the puzzle is only about recognizing objects, for example picking pictures that contain a certain object. That is an exception. A sliding or jigsaw-style puzzle is not object recognition.
> - Whether the puzzle is about content the user provided to the site. That is also an exception, but it is unlikely for a CAPTCHA.
> - Whether anything helps people complete the puzzle. That is the Mechanism exception.
> - Whether "no alternative" means no other way to sign in, or only no other kind of CAPTCHA. These are different.
>
> Leaning: if the puzzle is not object recognition and nothing assists the user, 3.3.8 fails.
>
> **1.1.1 Non-text Content**
>
> For a CAPTCHA, the criterion requires: "text alternatives that identify and describe the purpose of the non-text content are provided, and alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
>
> Known: the puzzle is a CAPTCHA, because its purpose is to confirm that a person is using the site.
>
> Still needed:
> - Whether the puzzle is non-text content. A visual puzzle is. A puzzle written as text is not.
> - Whether the puzzle has a text alternative that identifies and describes its purpose.
> - Whether "no alternative" means there is no other form of CAPTCHA, such as one using a different sense.
>
> Leaning: if the puzzle is visual and has no other form of CAPTCHA using a different sense, 1.1.1 also fails.
>
> **What to send me to get a firm verdict**
> - A description or screenshot of the puzzle, and what the user has to do to solve it.
> - What the page offers if someone cannot solve it, and the accessible name and any text for the puzzle.
> - Any password manager, copy and paste, or help feature on the login.
>
> **Fix to check against the criteria**
>
> - Offer another way to sign in that needs no puzzle, no typing of characters, and no remembering. For example, a passkey or a sign-in link sent by email that the person selects. This is the Alternative exception in 3.3.8. This is a design and development change.
> - Or replace the puzzle with one that only asks people to recognize objects. This meets 3.3.8, but 1.1.1 still applies, so it still needs a text alternative and another form of CAPTCHA.
> - Adding an audio version of the puzzle helps with 1.1.1 only. It does not satisfy 3.3.8, because audio can still be a cognitive function test.
> - Test the login with a keyboard, with a screen reader, and with people with disabilities. Automated checks cannot show that a puzzle is usable.
>
> **Sources**
>
> - Normative: WCAG 2.2 success criteria 3.3.8 and 1.1.1, linked above.
> - Informative, not requirements: Understanding 3.3.8 https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html and Understanding 1.1.1 https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html. I have not opened these pages in this conversation. They are catalogued in the plugin and linked for you to read.
>
> This is guidance only. It does not certify your product, guarantee WCAG conformance, or give legal advice.

### B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criterion that decides it: 3.3.8 Accessible Authentication (Minimum), Level AA**
> - Normative text: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - Understanding (informative): https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> - Quick Reference (informative): https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum
>
> The criterion says: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:"
> - "Alternative: Another authentication method that does not rely on a cognitive function test."
> - "Mechanism: A mechanism is available to assist the user in completing the cognitive function test."
> - "Object Recognition: The cognitive function test is to recognize objects."
> - "Personal Content: The cognitive function test is to identify non-text content the user provided to the website."
>
> The definition of "cognitive function test" lists "transcription, such as typing in characters". Typing the characters from a distorted image is transcription.
>
> **Known**
> - The CAPTCHA is a step in signing in, which is an authentication process.
> - The user must type the characters shown in distorted text. This is a cognitive function test (transcription).
> - There is no other way to sign in. This rules out the Alternative exception.
> - The answer cannot be pasted or autofilled. This rules out the Mechanism exception.
> - The test is typing text, not recognizing objects. This rules out the Object Recognition exception.
> - The test is not about content the user gave the site. This rules out the Personal Content exception.
>
> **Still needed for this criterion**
> - Nothing. Every exception is ruled out by what you stated.
>
> **Evidence for the fail:** the sign-in step requires a cognitive function test, and none of the four exceptions applies.
>
> **Also check: 1.1.1 Non-text Content, Level A**
> - Normative text: https://www.w3.org/TR/WCAG22/#non-text-content
> - This criterion has a CAPTCHA exception. It says text alternatives that "identify and describe the purpose of the non-text content are provided, and alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
> - Still needed: whether the CAPTCHA has a text alternative that describes its purpose, and whether it offers an alternative form that uses a different sense, such as audio. You said there is no other way to sign in. I cannot tell from that whether a second CAPTCHA form exists, so I do not give a separate verdict on 1.1.1. The fail above does not depend on it.
>
> **Who is affected:** many people with dyslexia or other learning disabilities, people with memory or attention difficulties, people with low vision, and people who are blind can be unable to sign in. Distorted text is hard to read for many of these people. Typing it also cannot be done by an assistive tool, so there is no way around the step.
>
> **Fixes that would satisfy the criterion** (the first two are the safest)
> - Offer another way to sign in that does not rely on a cognitive function test. Examples are a passkey, a sign-in link sent by email, or a device prompt. This meets the "Alternative" exception.
> - Remove the CAPTCHA from the sign-in step and use a check that does not need the user to do anything, such as rate limiting or risk-based checks done in the background.
> - If you keep a CAPTCHA, use one where the test is to recognize objects. This meets the "Object Recognition" exception for 3.3.8. It still has to meet 1.1.1, so it needs a text alternative and an alternative form for people who cannot see the images.
> - Pasting or autofill alone would not fix a CAPTCHA, because the characters are inside an image. The user would still have to read and retype them.
>
> **Source labels**
> - Normative: WCAG 2.2 success criteria 3.3.8 and 1.1.1, and the definitions quoted above.
> - Informative: the Understanding and Quick Reference pages linked above.
>
> Test the fix with keyboard only, with a screen reader, with a password manager, and with people with disabilities. Automated checks cannot show that a sign-in flow is accessible. This is guidance on WCAG 2.2 AA only. It is not a certification of your product and not legal advice.

### B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails WCAG 2.2 AA.
>
> **Criterion that applies**
>
> - 2.2.2 Pause, Stop, Hide (Level A, so it is part of the AA benchmark). It covers moving, blinking, scrolling, or auto-updating information that starts on its own. [Normative text](https://www.w3.org/TR/WCAG22/#pause-stop-hide)
>
> Another criterion that might apply: 2.2.1 Timing Adjustable (Level A). It covers time limits set by the content. I am not sure that a slide timer counts as a time limit, so 2.2.2 is the closer fit. [Normative text](https://www.w3.org/TR/WCAG22/#timing-adjustable)
>
> **What 2.2.2 says (normative)**
>
> "For moving, blinking, scrolling, or auto-updating information, all of the following are true:
> - Moving, blinking, scrolling: For any moving, blinking or scrolling information that (1) starts automatically, (2) lasts more than five seconds, and (3) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it unless the movement, blinking, or scrolling is part of an activity where it is essential; and
> - Auto-updating: For any auto-updating information that (1) starts automatically and (2) is presented in parallel with other content, there is a mechanism for the user to pause, stop, or hide it or to control the frequency of the update unless the auto-updating is part of an activity where it is essential."
>
> The text defines "mechanism" as "process or technique for achieving a result". It does not say the mechanism must be a button.
>
> **Known**
>
> - The carousel advances on its own, so it starts automatically.
> - It changes every 4 seconds.
> - There is no pause button.
>
> **Still needed**
>
> - Is the carousel shown in parallel with other content on the page? This is likely, but you did not say so.
> - Is there any other way to pause, stop, or hide it? For example, it might stop on keyboard focus, stop on hover, or have a setting that turns it off. "No pause button" does not rule these out, because the criterion asks for a mechanism, not a button.
> - Is the auto-advance part of an activity where it is essential? This exception is rare for a marketing or content carousel.
> - If you treat it as moving content: does it keep moving for more than five seconds? A carousel that cycles with no end usually does, but please confirm. The auto-updating part has no duration condition.
>
> **Where this leans**
>
> If the carousel sits next to other content, nothing else lets people pause, stop, or hide it, and it is not essential, it fails 2.2.2. This is a common failure. Please tell me about those three points and I can give a firm verdict.
>
> **Who is affected**
>
> - People with attention or reading difficulties may lose their place when a slide changes before they finish.
> - People who read slowly, including some people with low vision or learning disabilities, may not have time to read.
> - People who use a screen reader or a magnifier may find that content changes while they are reading it.
>
> **Fix**
>
> - Design: add a clearly labeled Pause/Play control near the carousel. Better still, do not auto-advance by default.
> - Development: make the control a native button with a clear accessible name. It should work with a keyboard. Stop the movement when the person uses the control. Consider also pausing on keyboard focus and on hover. Those extras are good practice, not a requirement. Keep the control's own state (paused or playing) available to assistive technology.
>
> Before you ship, check the fix by hand with a keyboard and with the screen readers and browsers your product supports. Include people with disabilities in testing if you can. Automated checks alone cannot show that a carousel is usable.
>
> **Sources**
>
> - Normative: WCAG 2.2, success criterion 2.2.2. https://www.w3.org/TR/WCAG22/
> - Informative (explains, adds no requirements): [Understanding Pause, Stop, Hide](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html) and [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/#pause-stop-hide). I have not opened these pages in this conversation, so I rely on the criterion text above.
>
> This is guidance, not a certification or legal advice.

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criterion that decides it:** 2.5.7 Dragging Movements, Level AA (new in WCAG 2.2). It says: "All functionality that uses a dragging movement for operation can be achieved by a single pointer without dragging, unless dragging is essential or the functionality is determined by the user agent and not modified by the author."
> - Normative text: https://www.w3.org/TR/WCAG22/#dragging-movements
>
> **Known**
> - Reordering the list uses dragging. WCAG lists list items as an example of draggable elements.
> - You say there is no other way to reorder items. So a single pointer (a mouse click, a tap, or a stylus) cannot do it without dragging.
> - Dragging is not essential. "Essential" means the function cannot be achieved in another way that would conform. Reordering can be done in other ways, such as move buttons.
> - The list is your own component, so the user agent exception does not apply.
>
> **Still needed**
> - Nothing for the verdict on 2.5.7.
>
> **Evidence:** The reorder function depends on dragging and has no non-dragging option. That fails 2.5.7.
>
> **Also check: 2.1.1 Keyboard, Level A.** It says: "All functionality of the content is operable through a keyboard interface without requiring specific timings for individual keystrokes, except where the underlying function requires input that depends on the path of the user's movement and not just the endpoints."
> - Normative text: https://www.w3.org/TR/WCAG22/#keyboard
> - Known: there is no other way to reorder.
> - Still needed: whether the drag itself can be done with a keyboard. I cannot tell from your message.
> - Leaning: it likely fails too if only a mouse or touch can reorder. Reordering depends on the end position, not the path of the movement, so the path exception does not look like it applies.
>
> **A fix that works for both criteria**
> - Add a control that does not need dragging. Examples are "Move up" and "Move down" buttons on each item, or a "Move to position" menu.
> - Use real buttons so they work with a mouse, touch, and a keyboard.
> - Give each button a name that says which item it moves, such as "Move Invoice 12 up".
> - Tell people the result. For example, announce the new position in a status message. This is good practice that helps people who use a screen reader.
> - Check that the new controls are at least 24 by 24 CSS pixels, or spaced as 2.5.8 Target Size (Minimum), Level AA, describes.
> - A keyboard-only fix is not enough for 2.5.7. It needs a way for a single pointer to reorder without dragging.
>
> **Source labels**
> - Normative: the WCAG 2.2 criteria text quoted above.
> - Informative: Understanding Dragging Movements, https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html. It explains but adds no requirements.
>
> **Testing:** Test the fix with a mouse, with touch, with a keyboard alone, and with the screen readers and other assistive technology your users rely on. Where you can, include people with disabilities. Automated checks alone cannot show that reordering works for everyone.
>
> This is guidance, not a certification, a guarantee of conformance, or legal advice.
