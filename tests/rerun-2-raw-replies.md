# Raw replies, targeted re-run 2

Replies from both models, one run per case, exactly as each agent wrote them to file. Each agent read only the five plugin files at commit `98c1306` and had no web access. See `rerun-2-results.md` for scoring and caveats.

## Smaller model

### A2a

> WCAG mode is on for this question.
>
> **Verdict: Cannot tell yet.** It leans toward Fails WCAG 2.2 AA.
>
> **Criteria that could apply**
>
> 1. **3.3.2 Labels or Instructions**, Level A. Covers whether each input has a label or instructions that tell the person what to enter.
>    - Normative: https://www.w3.org/TR/WCAG22/#labels-or-instructions
>    - Informative: https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html
> 2. **1.3.1 Info and Relationships**, Level A. Covers whether the link between a label and its input is set in the markup, not only by how the page looks.
>    - Normative: https://www.w3.org/TR/WCAG22/#info-and-relationships
> 3. **4.1.2 Name, Role, Value**, Level A. Covers whether each input gives assistive technology a name and a role.
>    - Normative: https://www.w3.org/TR/WCAG22/#name-role-value
> 4. **1.4.3 Contrast (Minimum)**, Level AA. Covers the contrast of text. Placeholder text is text, so this check applies to it.
>    - Normative: https://www.w3.org/TR/WCAG22/#contrast-minimum
> 5. **1.3.5 Identify Input Purpose**, Level AA. Applies only if the field asks for a personal detail, such as a name, email address, or phone number.
>    - Normative: https://www.w3.org/TR/WCAG22/#identify-input-purpose
>
> **Known**
>
> - The input shows placeholder text.
> - You have described the placeholder as the only text that describes the field.
>
> **Still needed**
>
> - Whether the markup has a real label, or an accessible name set another way (for example, a label element tied to the input, or an aria-label attribute). If one exists, 3.3.2 and 4.1.2 may be met and the problem is only visual.
> - Whether the field asks for a personal detail (for 1.3.5).
> - The text and background colors of the placeholder, to check the contrast ratio (for 1.4.3).
> - Whether the instructions appear somewhere else on the page and are linked to the field.
> - Which browsers and assistive technologies the product supports. How a name is exposed can vary by browser and tool, so test it.
>
> **Not required by WCAG does not mean fine.** Placeholder-only inputs can block people even where a criterion is not clearly failed.
>
> **Back in plain English mode**
>
> A placeholder is faint hint text inside an empty box. It is not a label. Once someone starts typing, the hint often disappears, so the person may forget what the box is for. People who use a screen reader may hear no name for the box if no label is linked to it. People with low vision may not see faint hint text at all. People with memory or attention needs lose track of the question.
>
> Fix:
>
> - Designers: add a visible label above or beside each field. Keep the placeholder only for an example, such as "name@example.com", and check that its color contrast is strong enough.
> - Developers: connect each label to its input with a label element, so screen readers announce the name. Check that the label stays visible while the person types.
>
> Test the form with the keyboard and a screen reader, and ask people who use assistive technology to try it.
>
> Learn more: Understanding WCAG 2.2, Labels or Instructions, at https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html. The source of the requirements is WCAG 2.2 at https://www.w3.org/TR/WCAG22/, which the maintainers have reviewed.

### B1

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if the text around the link does not say where it goes.
>
> **Criteria that could apply**
>
> - **2.4.4 Link Purpose (In Context)**, Level A. It covers whether a person can tell what a link does from its text, or from the text around it. Normative text: https://www.w3.org/TR/WCAG22/#link-purpose-in-context. Explanation: https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html
> - **2.4.9 Link Purpose (Link Only)**, Level AAA. This is not part of the WCAG 2.2 AA benchmark, so it does not set this verdict.
>
> I have not read the exact wording of 2.4.4 in this conversation. Check it at the normative link before you quote it.
>
> **Known**
> - The link text is "click here".
>
> **Still needed**
> - The text around the link: the sentence, list item, table cell, or heading it sits in.
> - Whether that text says where the link goes or what it does.
>
> **What the answer depends on**
> - If the link text, read with the text around it, makes the destination clear, the link may meet 2.4.4. Example: "Read the 2026 accessibility report. Click here." The sentence before the link may be enough.
> - If nothing nearby says where the link goes, it likely fails 2.4.4.
>
> **Why it matters**
> Some people who use a screen reader pull up a list of a page's links and hear them with no surrounding text. In that list, "click here" does not say where any of the links go.
>
> **Fix**
> - Name the destination in the link text. For example, "Read the 2026 accessibility report" instead of "click here". Content writers can make this change. Keep the words inside the link itself.
>
> "Click here" is weak practice, but it does not fail the criterion by itself. The question is whether people can tell where the link goes.
>
> **Testing**
> - Test with a screen reader, and with people who use one. Pull up the page's list of links and check that each one makes sense on its own. Automated checks cannot judge this reliably.
>
> **Sources**
> - Normative: WCAG 2.2, criterion 2.4.4 (linked above).
> - Informative: Understanding WCAG 2.2, criterion 2.4.4 page (linked above).

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if the puzzle tests a cognitive skill and the login has no other way to complete that step.
>
> **Criteria that could apply (WCAG 2.2, Level AA benchmark)**
>
> 1. **3.3.8 Accessible Authentication (Minimum), Level AA.** This covers sign-in steps that depend on a cognitive function test. Normative: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum. Informative: https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> 2. **1.1.1 Non-text Content, Level A.** A puzzle image is non-text content, so check whether it has an equivalent text alternative and whether an exception applies. Normative: https://www.w3.org/TR/WCAG22/#non-text-content. Informative: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>
> **Known**
>
> - The login asks users to solve a puzzle CAPTCHA.
> - No alternative is offered for that step.
>
> **Still needed**
>
> - What the puzzle asks the user to do. Does it test memory, reasoning, or recognizing content, or does it test something else, such as lining up a piece? This decides whether 3.3.8 applies and whether one of its exceptions applies.
> - Whether the puzzle needs a drag, a precise pointer action, or a time limit. These can bring in other criteria, such as 2.5.7 Dragging Movements (Level AA) and 2.2.1 Timing Adjustable (Level A).
> - Whether the puzzle can be finished with a keyboard only and with a screen reader.
> - Whether the password field accepts paste and password managers, and whether a passkey or another sign-in option exists that does not use the puzzle.
>
> **Who is affected**
>
> - People with some memory, learning, or reasoning disabilities may not be able to finish the puzzle, so they cannot sign in.
> - People who are blind may not be able to see a visual puzzle.
> - People with motor disabilities may not be able to complete a drag or a precise click.
>
> **Concrete next steps**
>
> - Confirm what the puzzle asks for, then test the login with a keyboard only and with a screen reader.
> - Add a second challenge that does not depend on a cognitive test, or add a sign-in route that does not need one, such as passkeys or support for password managers. Check each option against the normative text of 3.3.8, because the criterion has conditions.
> - Check 1.1.1 for a text alternative to the puzzle image, and check its exceptions.
> - Test with people with disabilities. Automated checks cannot show whether this step is accessible.
>
> **Sources**
>
> - Normative: WCAG 2.2 (the success criteria above).
> - Informative: Understanding WCAG 2.2 pages for 3.3.8 and 1.1.1.
>
> This is guidance, not a conformance check or legal advice.

### B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Criteria that could apply**
>
> - 2.2.2 Pause, Stop, Hide (Level A). It covers moving or auto-updating content that starts on its own. Link: https://www.w3.org/TR/WCAG22/#pause-stop-hide
> - 2.2.1 Timing Adjustable (Level A). It covers time limits. Nothing you described is a time limit on the user, so this is unlikely to be the main criterion here.
>
> **Facts the verdict depends on (2.2.2)**
>
> Known:
> - The carousel starts and advances on its own every 4 seconds.
> - It has no pause button.
>
> Still needed:
> - Whether it shares the page with other content that people read or use while it moves.
> - Whether any other control stops or hides it, such as a stop or hide button.
> - Whether the movement is essential to what the page is for. This is rarely true for a carousel.
>
> **Verdict: Cannot tell yet.** It leans toward Fails. If the carousel moves alongside other content and nothing lets people pause, stop, or hide it, it would fail 2.2.2. This is a Level A criterion, and Level A is part of the Level AA benchmark.
>
> **Fix (this does not change the verdict)**
>
> - Add a visible pause control near the carousel that stops the auto-advance and keeps it stopped until the person starts it again. Design should place and label it; development should wire it up. This is what 2.2.2 looks for.
> - Good practice: make the control reachable by keyboard and give it a clear name, such as "Pause carousel", so people using a keyboard or screen reader can find it.
> - Good practice, not a WCAG requirement: also pause when someone hovers over or focuses on the carousel.
> - Test with a keyboard and a screen reader, and with people who use them. Automated checks cannot confirm this.
>
> **Sources**
>
> - Normative: WCAG 2.2, 2.2.2 Pause, Stop, Hide: https://www.w3.org/TR/WCAG22/#pause-stop-hide
> - Informative: Understanding WCAG 2.2, Pause, Stop, Hide: https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html
> - Informative: How to Meet WCAG (Quick Reference): https://www.w3.org/WAI/WCAG22/quickref/#pause-stop-hide

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails.
>
> **Criteria that could apply**
>
> - 2.5.7 Dragging Movements, Level AA. This covers functions that need a drag. It asks for a single-pointer alternative to the drag, unless dragging is essential. Link: https://www.w3.org/TR/WCAG22/#dragging-movements
> - 2.1.1 Keyboard, Level A. This covers operating functions from a keyboard. Link: https://www.w3.org/TR/WCAG22/#keyboard
>
> **Known**
>
> - Items in the list can be reordered only by dragging.
> - There is no other way to reorder them, so there is no single-pointer alternative and no keyboard way to reorder.
>
> **Still needed**
>
> - Whether dragging is essential to the task. The essential exception is narrow. It applies when the drag itself is required, not when drag is only the chosen design. Check the exceptions on the Understanding pages before you decide. Understanding page for 2.5.7: https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html
>
> If dragging is not essential, both criteria fail for this list, and the verdict would be Fails WCAG 2.2 AA.
>
> **Who is affected**
>
> People who cannot make a precise drag, such as people with motor disabilities, people using a switch device, and people who cannot use a mouse. Keyboard users and screen reader users also cannot reorder items at all.
>
> **Concrete fix (development)**
>
> - Add a visible control for each item that moves it up or down, such as Move up and Move down buttons, or a Move to menu.
> - Use real button elements with clear names, such as "Move Quarterly report up". Make sure they work from the keyboard and with a single click or tap.
> - Keep drag and drop if you want it, but only as an extra. It does not replace the new controls.
> - Good practice: announce the new position when an item moves, so screen reader users know where it went.
>
> Design can help by showing these controls in the layout and in the focus and error states.
>
> **Sources**
>
> - Normative: WCAG 2.2, W3C. Reviewed 2026-09-29. https://www.w3.org/TR/WCAG22/
> - Informative: Understanding WCAG 2.2, W3C. Reviewed 2026-09-29. https://www.w3.org/WAI/WCAG22/Understanding/
>
> **Testing**
>
> Test the reorder with the keyboard only and with a screen reader. Then test with people who use assistive technology and with people with motor disabilities. Automated checks cannot show whether this works for them.
>
> This is guidance, not a conformance statement.

### C1

> Many people who are blind use a screen reader. A screen reader is software that reads the page aloud, or sends the text to a braille display. Many also move around with the keyboard instead of a mouse. How they do it depends on the person, the browser, and the screen reader. Some people who are blind use no screen reader at all, so do not assume one setup.
>
> People who use a screen reader often move around a page in these ways:
>
> - Jump from heading to heading to scan the page.
> - Move from link to link, or from button to button.
> - Jump to a form field and fill it in.
> - Read the page from top to bottom.
>
> Each of these depends on the page being built well. Here is what to check on your site, and who can fix each item.
>
> 1. **Headings.** Use real heading levels in order: one main title, then section titles. If a heading is only large bold text, the person cannot jump to it. Design sets the outline. Development marks it up.
>
> 2. **Link and button names.** A screen reader often reads a link on its own, out of context. "Click here" or "Read more" tells the person nothing. Use names that stand alone, such as "Read the 2026 pricing guide." Content and design write the names. Development checks the name in the code.
>
> 3. **Images.** Give each meaningful image a short text description. Hide decorative images from the screen reader so they do not add noise. Content writes the descriptions. Development adds them to the page.
>
> 4. **Forms.** Every field needs a visible label that is connected to it in the code. A placeholder inside the box is not a replacement for a label. When something is wrong, the error should say what happened and how to fix it, in text next to the field. Development should make sure the screen reader announces the error.
>
> 5. **Changes on the page.** Some updates happen without a page load, such as search results or "item added to cart." A screen reader may not notice them. Show a short status message that is announced, such as "5 results found." Development builds this.
>
> 6. **Reading order.** The content should make sense when read in order, without seeing the layout. Design checks the layout. Development keeps the code order the same as the visual order.
>
> 7. **Keyboard access.** Everything a person can click should also work with the keyboard. The person should always be able to tell where they are on the page. Development builds and tests this.
>
> 8. **Video.** People who are blind need to know what is on screen. A spoken or written description of key visual content, called audio description, helps. A transcript also helps. Content and development provide these.
>
> 9. **Hidden content.** Menus that open only on hover, or content that appears only with a mouse, may be out of reach. Make sure these also open from the keyboard and are announced.
>
> Testing matters most here. Try your main tasks with a screen reader yourself. Then test with people who are blind. Automated checking tools find some problems, but they cannot show how the site works for a person.
>
> To give you more specific advice, I need a few details. What does the site do, such as sell products, share news, or handle sign-ups? Which screen reader and browser do you test with? Which pages or tasks matter most?
>
> Learn more: W3C, Understanding WCAG 2.2: https://www.w3.org/WAI/WCAG22/Understanding/
>
> If you want this answered in formal standard terms, say "WCAG mode on."

### C4

> Alt text is a short written description of an image. It gives people who cannot see the image the same meaning.
>
> - Many people who are blind use a screen reader, which reads the page aloud. Without alt text, the screen reader may skip the image or read out a file name like "IMG_4832.jpg".
> - If an image does not load, many browsers show its alt text in its place.
>
> How to do it:
> - Designers: write what the image is for, in one short line. For example: "Bar chart: sales rose 20% from May to June." Mark images that only decorate the page, so developers know to hide them from screen readers.
> - Developers: put that text in the image's alt attribute (the HTML field that holds it). Decorative images get an empty alt value.
>
> Test it: turn on a screen reader and listen to the page. Include people who use screen readers in your testing if you can.
>
> Learn more: Understanding WCAG 2.2 (https://www.w3.org/WAI/WCAG22/Understanding/). It is the W3C's explanation with examples.

### C5

> Many people who are blind use a screen reader. A screen reader is software that reads the page aloud or sends the text to a braille display. Some people use it on a computer with the keyboard. Others use it on a phone or tablet with touch.
>
> Which screen reader is most used depends on the device, the country, and the person. Common examples are NVDA and JAWS on Windows, VoiceOver on Apple devices, and TalkBack on Android. I cannot give you a reliable ranking. This plugin has no usage data, so I will not guess at one.
>
> What this means for your product:
>
> - Do not build for one screen reader only. Test with at least two, on the devices your users actually use.
> - Give every button, link, and form field a clear label. The screen reader reads that label aloud, so a label like "Click here" tells the person very little.
> - Make sure every control works with the keyboard alone. Some people cannot use a mouse or touch screen well, and some screen reader users move through a page with the keyboard.
> - Test with people who use screen readers every day. Automated checks cannot show that a page works for them.
>
> Learn more: W3C's guide to understanding the web accessibility guidelines (https://www.w3.org/WAI/WCAG22/Understanding/). It explains the guidelines with examples. It does not rank screen readers by how many people use them.

### D1

> That question depends on the law, so I can't give a yes or no. Whether the ADA applies to your product, and what it requires, is a question for a lawyer who knows the ADA and your sector.
>
> Passing a technical standard also does not, on its own, make a product compliant with the law. It shows that the product met the checks in that standard. It does not guarantee that no person with a disability will run into a barrier.
>
> I can help with the accessibility side. WCAG 2.2 is a technical standard from the W3C. It describes how to make web content usable for people with disabilities, including people who are blind, people with low vision, people who are deaf or hard of hearing, and people who use only a keyboard or voice.
>
> Two next steps:
>
> - Ask a legal adviser what the ADA requires for your product.
> - If you want, I can switch to WCAG mode and check a specific page or feature against WCAG 2.2 Level AA. I would then say what passes, what fails, and what we still need to know. Even then, that is guidance, not certification, and testing with people with disabilities is still needed.
>
> Learn more: W3C, Web Content Accessibility Guidelines (WCAG) 2.2, https://www.w3.org/TR/WCAG22/

## Larger model

### A2a

> **Verdict: Cannot tell yet. It leans toward Fails WCAG 2.2 AA.**
>
> **Criteria that could apply**
>
> - 3.3.2 Labels or Instructions, Level A. It covers giving people labels or instructions for input fields. [Normative text](https://www.w3.org/TR/WCAG22/#labels-or-instructions)
> - 1.3.1 Info and Relationships, Level A. It covers whether the label-to-field relationship is available in the code, not only in the look of the page. [Normative text](https://www.w3.org/TR/WCAG22/#info-and-relationships)
> - 4.1.2 Name, Role, Value, Level A. It covers whether the field has a name that assistive technology can use. [Normative text](https://www.w3.org/TR/WCAG22/#name-role-value)
> - 2.4.6 Headings and Labels, Level AA. It covers whether labels describe the purpose of the field. [Normative text](https://www.w3.org/TR/WCAG22/#headings-and-labels)
> - 1.4.3 Contrast (Minimum), Level AA. It covers the contrast of the placeholder text, if the placeholder is the only text that tells people what to enter. [Normative text](https://www.w3.org/TR/WCAG22/#contrast-minimum)
>
> **Known**
>
> - The field has a placeholder.
> - You describe it as placeholder-only. I read that to mean there is no separate visible label.
>
> **Still needed**
>
> - The markup. Does the field have an accessible name from another source, such as a `label` element, `aria-label`, or `aria-labelledby`? Browsers and assistive technologies differ in how they treat a placeholder as a name, so I cannot assume it.
> - Is there other visible text nearby that works as a label or instruction, such as a heading or a line of text above the field?
> - Does the placeholder text disappear when someone types or focuses the field, and is there any other way to see what the field is for?
> - The placeholder color and background, to check contrast.
> - What the field is for, for example a search box or a long form. This affects how clear the purpose is without a label.
>
> **Which way it leans**
>
> A placeholder-only field with no other visible label and no accessible name is very likely to fail 3.3.2 and 4.1.2. The label disappears once someone starts typing. Some people with cognitive or memory disabilities may forget what the field asks for. Some people who use a screen reader may hear no name for the field, and that depends on the browser and tool. Placeholder text is often light gray, so low contrast (1.4.3) is a common extra problem.
>
> If a visible label or an accessible name is present, the verdict may change. A placeholder-only field can still be a barrier even when it technically meets a criterion. That is why I would not treat "not required by WCAG" as "fine".
>
> **Sources**
>
> - Normative: WCAG 2.2 success criteria, linked above. Source: [WCAG 2.2](https://www.w3.org/TR/WCAG22/).
> - Informative: [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/). For example, [Understanding 3.3.2](https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html), [Understanding 4.1.2](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html), and [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/).
> - I have not opened these pages in this conversation, so I am not quoting their wording. Please read the linked text for the exact requirement.
>
> **Suggested fix (development and design)**
>
> - Add a visible label that stays on screen, and connect it to the field with a native `label` element.
> - Use the placeholder only for a short example or hint, if you use it at all. Do not use it as the only label.
> - Check that the placeholder text has enough contrast, if you keep it.
>
> **Test it**
>
> - Check the field with a keyboard and with a screen reader on the browsers you support.
> - Zoom in and test with real users, including people with cognitive or memory disabilities and people who use assistive technology. Automated checks alone cannot show that the field is usable.
>
> Send me the field's markup and a screenshot or description of its states. Then I can give you a firmer verdict.
>
> This is guidance only. It is not a certification of conformance or legal advice.

### B1

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** Link text that says "click here" does not fail by itself. It depends on the context around the link. It leans toward Likely meets if the surrounding text makes the link's purpose clear in the code. It leans toward Fails if the link has no such context.
>
> **Criterion that applies**
>
> - 2.4.4 Link Purpose (In Context), Level A. It covers whether a user can work out where a link goes or what it does. That can come from the link text alone, or from the link text plus context that software can identify, such as the same sentence, paragraph, list item, table cell, or the heading before it. There is an exception for links whose purpose is unclear to everyone. Link: https://www.w3.org/TR/WCAG22/#link-purpose-in-context (normative)
>
> 2.4.9 Link Purpose (Link Only) is Level AAA. It is not part of the AA benchmark, so it does not decide this verdict.
>
> **Known**
>
> - The link text is "click here".
>
> **Still needed**
>
> - The surrounding text and structure. Is the link inside a sentence, paragraph, list item, table cell, or under a heading that says what the link is for?
> - The markup. Is that context identifiable by software, so assistive technology can find it? Or is it only visual, for example text in a separate element that is only positioned nearby?
> - Whether an accessible name has been set, such as an aria-label or a visually hidden text addition. If so, that name is what counts.
> - Whether the purpose is unclear to all users, not only to people using assistive technology. That is an exception.
> - Where the link goes, and whether it is the only link on the page that says "click here" or one of several that go to different places.
>
> **Why it can still be a barrier even if it meets 2.4.4**
>
> A practice that is poor or discouraged does not by itself fail a criterion, and this case needs checking against what 2.4.4 requires. But "click here" can still block people. Many people who use a screen reader (software that reads the page aloud) open a list of all links on a page. In that list, several links that all say "click here" tell them nothing. People who use voice control may also find it hard to say a link name that is the same as many others. Also, "click" assumes a mouse, but people use keyboards, touch, and other input.
>
> Meeting 2.4.4 through context is a requirement. Descriptive link text is good practice, and it is the safer way to build.
>
> **Suggested fix (development and content design)**
>
> - Write link text that names the destination or action, for example "Read the 2025 pricing guide". The link text then makes sense on its own.
> - If you cannot change the visible text, add context that software can identify, such as putting the link in the sentence or list item that describes it. Test that it works in the tools your users have.
>
> **Sources**
>
> - WCAG 2.2, 2.4.4 Link Purpose (In Context): https://www.w3.org/TR/WCAG22/#link-purpose-in-context (normative)
> - Understanding Link Purpose (In Context): https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html (informative)
> - How to Meet WCAG, Link Purpose (In Context): https://www.w3.org/WAI/WCAG22/quickref/#link-purpose-in-context (informative)
>
> I did not open these pages in this conversation. They are the links listed in the plugin's criteria index. Read the normative page for the exact wording.
>
> **Testing**
>
> Check the links in a screen reader's link list, with voice control, and with a keyboard. Automated checks alone cannot show whether link context is clear. Test with people with disabilities when you can.
>
> If you share the markup and the text around the link, I can give a firmer verdict. This is guidance, not a certification or a statement that your product meets WCAG.

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails WCAG 2.2 AA if the puzzle asks people to solve or remember something, and no other way to log in is offered.
>
> **Criteria that could apply**
>
> - 3.3.8 Accessible Authentication (Minimum), Level AA. It covers steps that make people complete a cognitive function test to log in. [Normative](https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum) | [Understanding](https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html) | [Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum)
> - 1.1.1 Non-text Content, Level A. It covers text alternatives for non-text content, including CAPTCHAs. [Normative](https://www.w3.org/TR/WCAG22/#non-text-content) | [Understanding](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html) | [Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/#non-text-content)
>
> **Known**
>
> - The step is a login.
> - It asks users to solve a puzzle CAPTCHA.
> - You say there is no alternative.
>
> **Still needed**
>
> - What the puzzle asks users to do. For example: pick out everyday objects in pictures, solve a spatial or logic puzzle, drag a slider or piece, or retype distorted text. 3.3.8 has exceptions for some kinds of tasks, so the puzzle type changes the answer.
> - What "no alternative" means. Is there no other way to log in at all? Or is there no other way to pass the CAPTCHA (for example, an audio or text option)? Is there any help for the step, such as a way to skip it?
> - Whether the CAPTCHA has a text alternative that says what it is for. This matters for 1.1.1.
> - Whether the CAPTCHA sits on the login step itself, or elsewhere in the flow.
>
> **Why it leans toward Fails.** If the puzzle is a test that depends on memory, reasoning, or skills such as spatial thinking, and it is the only way to pass, 3.3.8 is likely failed. I am not stating the criterion's exact wording here. Check the conditions and exceptions in the normative text linked above.
>
> **Who is affected.** Many people with cognitive or learning disabilities, some people who are blind or have low vision, and some people with motor disabilities may be unable to finish a puzzle. If it is the only route, they cannot log in.
>
> **Fix options (design and development)**
>
> - Remove the puzzle where you can. Use bot checks that need no user task, such as checks running in the background.
> - Offer another way to log in that needs no puzzle, such as a one-time link sent by email, a passkey, or a password manager that can fill in the form.
> - If you keep a CAPTCHA, give it a text alternative that says what it is for, and offer a different kind of check that does not rely on the same ability.
> - Before you ship a fix, confirm it covers every person who reaches the login. A second puzzle of the same kind would not fix the problem.
>
> **Source labels**
>
> - Normative: the WCAG 2.2 success criteria linked above (source: WCAG 2.2, https://www.w3.org/TR/WCAG22/).
> - Informative: the Understanding and Quick Reference pages linked above.
>
> This is guidance only. It is not a conformance guarantee or legal advice. Test the login with a keyboard, with screen readers and other assistive technology, and with people with disabilities. Automated checks cannot judge this. Send me the puzzle type and what "no alternative" means, and I can give a firm verdict.

### B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet. It leans toward Fails.**
>
> **Criterion that could apply**
> - 2.2.2 Pause, Stop, Hide (Level A). In general terms, it covers content that moves, scrolls, blinks, or updates automatically, and whether people can control it.
>   - Normative: https://www.w3.org/TR/WCAG22/#pause-stop-hide
>   - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html
>
> I don't have the criterion text in front of me in this conversation. I am describing it in general terms only. Please check the exact conditions and exceptions in the normative text before you decide.
>
> **Known**
> - The carousel starts moving by itself and advances every 4 seconds.
> - There is no pause button.
>
> **Still needed**
> - Is there another way to pause, stop, or hide the movement? Examples are pausing on hover or keyboard focus, a stop control elsewhere on the page, or a setting. A missing button does not decide the question if another mechanism exists and works for keyboard and touch users.
> - Does the carousel keep moving for more than a short time, or does it stop by itself after a few rotations?
> - Is the carousel shown alongside other content on the page?
> - Is the movement essential to the content? For example, is the activity unusable without it?
> - Do the slides contain anything that flashes? That would raise a separate criterion, so tell me if they do.
>
> **Why it leans toward Fails.** An auto-advancing carousel with a looping cycle, shown next to other content, and with no pause, stop, or hide mechanism, is the situation this criterion is aimed at. If the answers above confirm that, the verdict becomes Fails WCAG 2.2 AA under 2.2.2. The 4-second interval is not what decides it.
>
> **Who is affected**
> - People with attention or reading difficulties. Content changes before they finish reading it.
> - Many people who use a screen reader or screen magnifier. Content can change while they are reading it.
> - People with motor impairments, who may not reach a control in time.
> - People who are distracted by movement.
>
> **Good practice (not a separate requirement)**
> - Offer a visible pause or stop control that works with a keyboard and has an accessible name.
> - Consider not auto-advancing at all.
> - Pause the movement when someone hovers over the carousel or moves keyboard focus into it.
>
> Test with a keyboard, with a screen reader, and with people with disabilities. Automated checks alone can't show this is accessible. This is guidance, not a certification or legal advice.
>
> If you send the markup and tell me about any other pause mechanism, I can give a firmer verdict.

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet. It leans toward Fails WCAG 2.2 AA.**
>
> **Criteria that could apply**
> - 2.5.7 Dragging Movements, Level AA. It covers actions that need dragging and whether a simpler single-pointer way to do the same thing exists. [Normative](https://www.w3.org/TR/WCAG22/#dragging-movements) | [Understanding](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html) | [Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/#dragging-movements)
> - 2.1.1 Keyboard, Level A. It covers whether functionality can be operated from a keyboard. [Normative](https://www.w3.org/TR/WCAG22/#keyboard) | [Understanding](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html) | [Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/#keyboard)
>
> **Known**
> - This is a web page with a drag-and-drop list.
> - Dragging is the only way to reorder items. There is no keyboard method and no click or tap alternative.
>
> **Still needed**
> - Whether dragging is essential here. Both criteria have exceptions, and I have not been told whether any apply. Reordering a list is often possible by other means, but you have not said that this one is an exception.
> - Whether the drag behavior is custom code or built-in browser behavior that your code does not change. Built-in behavior can be an exception under 2.5.7.
> - For 2.1.1, whether reordering depends on the path of the movement, or only on the final position. If only the final position matters, a keyboard method is expected.
>
> **Which way it leans:** a custom drag-and-drop list with no other method most likely fails both criteria. If you confirm that dragging is not essential and the behavior is custom, the verdict would be Fails WCAG 2.2 AA.
>
> **Who is affected:** people who use a keyboard, a switch, or voice control. People with tremors or limited hand control may also be unable to hold a drag. Many people who are blind and use a screen reader (software that reads the page aloud) rely on keyboard commands as well.
>
> **Source labels:** the WCAG 2.2 criteria above are normative. The Understanding and Quick Reference pages are informative.
>
> **A fix to consider (good practice, not a WCAG requirement):**
> - Add "Move up" and "Move down" buttons to each item. Alternatively, let people select an item and choose a new position from a menu.
> - Make sure the alternative works from a keyboard and with a single click or tap.
> - Announce the new position to assistive technology, for example "Item moved to position 3 of 8".
> - Keep a visible focus indicator on the moved item.
>
> Test the result with a keyboard only, with the screen readers and browsers your product supports, and with people with disabilities. Automated checks cannot confirm that reordering works. This is guidance only. It is not a conformance claim or legal advice.

### C1

> I can't say how people who are blind use your site without seeing it. I can tell you how many people who are blind use the web in general, and what to check on your site.
>
> **How people who are blind often use the web**
>
> - Many people who are blind use a screen reader. This is software that reads the page aloud or sends it to a braille display (a device that shows text in braille). Not everyone who is blind uses one. Some people use other tools, such as magnification, and some people have some sight.
> - Many people use the keyboard or touch gestures instead of a mouse. They do not point at things. They move through the page in order.
> - Many screen reader users move by headings, links, buttons, and form fields. They often skip to the part they need instead of listening to the whole page.
> - Screen readers and browsers differ. The same page can sound different in different tools.
>
> **What this means for your site**
>
> A screen reader can only read what is in the page code. If something is only visible, the person may never find it. Common barriers:
>
> - Images with no text description. The person does not know what the image shows.
> - Buttons and links with unclear names, such as "Click here". The person hears the name with no context.
> - Form fields with no label. The person does not know what to type.
> - Headings that are missing or out of order. The person cannot scan the page.
> - Menus, dialogs, or pop-ups that cannot be reached with the keyboard, or that do not tell the person when they open.
> - Error or status messages that appear on screen but are not announced. The person does not know a problem happened.
> - Information shown only by color or position, such as "the red field".
>
> **How to find out for your site**
>
> - Design can help by planning headings, labels, and the reading order from the start.
> - Development can help by using standard HTML elements first, because they work with screen readers by default.
> - Test the main tasks, such as signing up or buying, with a keyboard and with a screen reader. Automated checks help, but they miss many problems.
> - The best way is to test with people who are blind and who use your site's main tasks.
>
> To give you more specific advice, it would help to know:
>
> - Which tasks matter most on your site?
> - Is it a new design or an existing site?
> - Which browsers and screen readers do your users have?
>
> **Learn more:** [Understanding WCAG 2.2 (W3C)](https://www.w3.org/WAI/WCAG22/Understanding/) explains the barriers above and how to fix them. If you want a WCAG-based answer, say "WCAG mode on".
>
> This is general guidance. It does not certify your site or replace testing with people with disabilities.

### C4

> Alt text is a short written description of an image. It gives the same information to people who cannot see the image.
>
> - Many people who are blind use a screen reader, which reads the page aloud. Without alt text, the screen reader cannot say what the image shows. People may miss key information or not know what a button or link does.
> - Alt text also shows up when an image does not load, for example on a slow connection.
> - Some people who use other tools, such as braille displays, also depend on it.
>
> Good alt text says what the image is for, not every detail. If an image is only decoration, it should be hidden from screen readers so it does not add noise.
>
> Learn more: Understanding WCAG 2.2 (W3C), https://www.w3.org/WAI/WCAG22/Understanding/
>
> I can say more about writing good alt text, or answer in WCAG terms, if you want.

### C5

> There is no single screen reader that most people who are blind use. A screen reader is software that reads the content of a screen aloud, or sends it to a braille display. Many people who are blind use one, but not everyone does. Some people with low vision use screen magnification instead, and some people use both.
>
> Which screen reader a person picks depends on things like their device, their browser, their work or school, the cost, and what they learned first. These choices also change over time and differ between countries. I do not have a reliable source in this plugin for usage numbers, so I will not name a "most popular" one or give a percentage.
>
> What this means for your work:
>
> - Do not build or test for just one screen reader. The same page can sound different in different screen readers and browsers.
> - Test the main tasks of your product (such as signing in, searching, and paying) with the screen readers and browsers your users are likely to use. Check your own user data or ask your users if you can.
> - Start with plain, standard HTML. It tends to work well across many tools. Use custom code and ARIA (extra attributes that describe parts of a page to assistive technology) only when standard HTML cannot do the job.
> - Automated checks are useful, but they cannot tell you how a page feels to use with a screen reader. Where you can, include people who are blind in your testing.
>
> If you want, I can suggest a simple screen reader test plan for a specific page or feature.
>
> Learn more: Understanding WCAG 2.2 (W3C), https://www.w3.org/WAI/WCAG22/Understanding/. This explains how accessibility requirements help people who use assistive technology. It does not give screen reader usage numbers.

### D1

> I can't tell you whether you are ADA compliant. That is a legal question, and I don't give legal advice or say whether something meets any law or regulation. A lawyer who knows accessibility law in your region can answer it.
>
> Here is what I can say about the standard itself:
>
> - WCAG 2.2 Level AA is the only standard I use. It is a technical standard for web content. It is not a law.
> - Meeting WCAG 2.2 AA does not by itself tell you that you meet any law. I can't say how a court or regulator would treat it for your product.
> - I can't certify that a product meets WCAG 2.2 AA either. I give guidance only.
> - A product can meet the standard and still be hard to use for some people. Real barriers can remain.
>
> What to do next:
>
> - Ask a lawyer what applies to your business and where you operate.
> - Test your product against WCAG 2.2 AA. Use automated checks, but do not rely on them alone, because they can't show that something is accessible.
> - Test by hand with a keyboard and with assistive technology, such as a screen reader (software that reads the page aloud).
> - Test with people with disabilities. They will find problems that checklists miss.
>
> If you want, tell me which pages or features you are working on. I can help you find barriers and suggest fixes. I can also answer in WCAG terms if you say "WCAG mode on".
>
> Learn more: Web Content Accessibility Guidelines (WCAG) 2.2, from W3C, the official standard: https://www.w3.org/TR/WCAG22/
