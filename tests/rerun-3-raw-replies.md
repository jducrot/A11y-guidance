# Raw replies, re-run 3

Replies exactly as each agent wrote them to file, one run per case. Each agent read only the five plugin files at commit `98c1306` (unchanged in `7796c43`) and had no web access. See `rerun-3-results.md` for scoring and caveats.

## Smaller model

### A1

> Placeholder text is useful as a short hint, but it cannot replace a label. Placeholder text is the faint words inside an empty box.
>
> **Why placeholder text is not enough**
>
> - It disappears as soon as someone starts typing. Anyone who forgets what a field asked for, or wants to check an entry before submitting, loses that information.
> - Many people with low vision find the faint grey text hard to read.
> - Some screen readers, which read the page aloud for people who are blind, may skip placeholder text or announce it inconsistently. This varies by browser and screen reader, so do not rely on it.
> - People with memory or attention difficulties benefit from a label that stays on screen.
> - Tools such as voice control and autofill need a clear name for each field to find it.
>
> **What to do**
>
> 1. Add a visible label above each field, and keep it on screen while the person types. (Design)
> 2. Connect each label to its field in the code, so the label is read out when the field gets focus. Use the standard HTML label element where you can. (Development)
> 3. Use placeholder text only for a short example, such as "MM/YY". Never use it as the only instruction. (Design)
> 4. Mark required fields in words, such as "(required)" in the label. Do not rely on an asterisk or color alone. (Design)
> 5. Add autocomplete hints for common fields such as name, email, address, and card number, so browsers can fill them in. This helps people with motor or memory difficulties avoid retyping. (Development)
> 6. When an error happens, show a text message next to the field that says how to fix it. Do not rely on red color alone. (Design and Development)
> 7. Design the states the form can be in: focus, error, and success. (Design)
>
> **How to test it**
>
> - Move through the whole form with only the keyboard. Every field should be reachable, and the focus should be easy to see.
> - Turn on a screen reader, such as NVDA on Windows or VoiceOver on Mac and iPhone, and check that each field announces its label.
> - If you can, ask people who use these tools to try the form.
>
> Automated checks can find some missing labels, but they cannot show that the form is easy to use.
>
> **Learn more:** Understanding WCAG 2.2, by W3C: https://www.w3.org/WAI/WCAG22/Understanding/ (This is the W3C guide that explains the accessibility guidelines, with examples.)
>
> To give you exact changes, tell me the platform, the framework or form library you use, and whether the fields are custom components or standard HTML inputs.

### A2b

> WCAG mode is on for this answer.
>
> **Verdict: Cannot tell yet. It leans toward Fails.**
>
> **Criteria that could apply**
>
> - 4.1.2 Name, Role, Value (Level A). A form field needs a name that software can read. Link: https://www.w3.org/TR/WCAG22/#name-role-value
> - 1.3.1 Info and Relationships (Level A). The link between a label and its field must be readable by software. Link: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - 3.3.2 Labels or Instructions (Level A). Inputs need a label or instructions. Link: https://www.w3.org/TR/WCAG22/#labels-or-instructions
>
> **Known**
>
> - The input has no label element, aria-label, aria-labelledby, title, or placeholder.
> - The visible word "Email" is not associated with the input.
>
> **Still needed**
>
> - The input's accessible name as the browser builds it on the rendered page. The snippet alone cannot show a label added by JavaScript, or one placed elsewhere in the page. Check the browser's accessibility inspector, or listen with a screen reader.
>
> If the browser reports no name for the input, the verdict is Fails WCAG 2.2 AA under 4.1.2. 1.3.1 and 3.3.2 are supporting evidence.
>
> **Sources**
>
> - Normative: the WCAG 2.2 success criteria, which define the requirement.
> - Informative: Understanding WCAG 2.2, which explains it without adding requirements.
>
> ---
>
> Back in plain English mode.
>
> Someone using a screen reader, which reads the page aloud, may tab to this field and hear no name for it. They may not know what to type. Someone using voice control may not be able to say "click Email". The visible word helps people who can see the page, but it does not reach the software that reads the page to them.
>
> **Fix (for developers):** connect the visible text to the field with a label element:
>
> <label for="email">Email</label>
> <input type="text" id="email">
>
> The `for` value must match the input's `id`. For an email address, also add `autocomplete="email"` so browsers can help fill it in.
>
> **Test it:** turn on a screen reader, tab to the field, and check that it announces "Email". The exact wording varies by screen reader. Also check that a click on the word "Email" moves the cursor into the field.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html

### A6

> Here is a plain-English guide. If you paste the list from your auditor, I can match each item to the exact requirement it refers to.
>
> **Who this affects**
> People who cannot use a mouse, such as some people with motor disabilities, rely on the keyboard to get around. Many people who are blind use a screen reader, which reads the page aloud. They need to hear what the dropdown is, whether it is open, and which option is highlighted.
>
> **Best option: use the built-in control (development)**
> If you can, use the standard select or button elements in your HTML. Browsers already handle the keyboard, and screen readers already announce them. Custom dropdowns are a common source of barriers, so only build one when the built-in control cannot do what you need.
>
> **If you build a custom dropdown (development)**
> A common keyboard pattern looks like this:
> 1. Tab moves focus to the dropdown button.
> 2. Enter, Space, or the Down Arrow opens the list.
> 3. The Up and Down Arrow keys move through the options. The highlighted option must be clear.
> 4. Enter chooses the highlighted option, closes the list, and returns focus to the button.
> 5. Escape closes the list without changing the choice.
> 6. Tab moves on to the next control. Focus must never get stuck inside the dropdown.
>
> Also make sure:
> - The button announces its name and whether the list is open or closed.
> - The list does not cover the item that has focus.
> - Any "selected" message is announced to screen reader users when the choice changes.
>
> **Design (for designers)**
> - Show a clear outline or highlight on the focused button and on the focused option. Many people need to see where they are.
> - Label the dropdown with words that say what it sets, such as "Country", not just the current value.
> - Plan the open, closed, focused, and error states so each one works with the keyboard.
>
> **Testing**
> - Use the page with only the keyboard, with the mouse unplugged. Try every step above.
> - Test with a screen reader that comes with the device, and if you can, ask people who use one to try it.
> - Automated checks can miss keyboard problems, so do not rely on them alone.
>
> **Learn more**
> ARIA Authoring Practices Guide (W3C): https://www.w3.org/WAI/ARIA/apg/
> This resource has not been reviewed by the maintainer yet. Treat its component patterns as one way to build a dropdown, not as a requirement.
>
> If your auditor's items use WCAG terms, say "WCAG mode on" and I will list the criteria that apply to this dropdown. I will also tell you which facts I still need, such as whether the dropdown is a built-in control or a custom one.

### B2

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Meets WCAG 2.2 AA, but is still a barrier.** This verdict covers reading level only. It says nothing about the rest of the site.
>
> No, a university reading level does not fail WCAG 2.2 Level AA. The reading-level criterion is Level AAA, which is outside the AA benchmark.
>
> **Criteria checked**
>
> - 3.1.5 Reading Level, Level AAA (not part of the AA benchmark). Requirement: https://www.w3.org/TR/WCAG22/#reading-level
> - 3.1.3 Unusual Words, Level AAA (not part of the AA benchmark). Requirement: https://www.w3.org/TR/WCAG22/#unusual-words
> - 3.1.4 Abbreviations, Level AAA (not part of the AA benchmark). Requirement: https://www.w3.org/TR/WCAG22/#abbreviations
>
> **Known**
>
> - The site is written at a university reading level.
> - The reading-level criterion that applies is 3.1.5, which is Level AAA.
>
> **Still needed**
>
> - Nothing, for the AA verdict.
>
> **Who is affected**
>
> Not required by WCAG AA does not mean fine. Some people with cognitive or learning disabilities may find dense text hard to follow. Some people who read the language as a second language may also find it hard. Long sentences and technical words make both groups work harder to complete a task.
>
> **Practical fixes (good practice, not a WCAG AA requirement)**
>
> - Rewrite the most important pages first: the home page, forms, instructions, and help pages. Content and design teams can do this together.
> - Use short sentences and common words. Explain any technical term the first time it appears, or avoid it.
> - Add a short plain-language summary at the top of long pages.
> - Use clear headings and short paragraphs.
>
> **Testing**
>
> - Ask people with cognitive or learning disabilities, and people who read the language as a second language, to try the key tasks and tell you where they get stuck.
> - Automated checks cannot tell you whether text is easy to read.
>
> **Sources**
>
> - Normative: WCAG 2.2, https://www.w3.org/TR/WCAG22/ (reviewed 2026-09-29).
> - Informative: Understanding WCAG 2.2, reading-level page, https://www.w3.org/WAI/WCAG22/Understanding/reading-level.html (reviewed 2026-09-29). It explains the criterion and adds no requirements.
>
> This is guidance, not a conformance guarantee or legal advice.

### B3

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** The screenshot does not give exact colors or text size, so I cannot decide the contrast question from it.
>
> **Criteria that could apply**
>
> - **1.4.3 Contrast (Minimum)**, Level AA. This covers the contrast between text and its background. This is the main criterion for grey text on white.
>   - Normative: https://www.w3.org/TR/WCAG22/#contrast-minimum
>   - Understanding: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
> - **1.4.5 Images of Text**, Level AA. This applies only if the text is part of an image rather than live text on the page.
>   - Normative: https://www.w3.org/TR/WCAG22/#images-of-text
> - **1.4.11 Non-text Contrast**, Level AA. This applies only if the grey is used for something other than text, such as an icon, a border, or a form control outline.
>   - Normative: https://www.w3.org/TR/WCAG22/#non-text-contrast
>
> **Known**
>
> - The text is grey.
> - The background is white.
>
> **Still needed**
>
> - The exact text color and background color, as hex values or from a color picker on the live page. Colors read from a screenshot are not reliable.
> - Whether the text is live text or an image of text.
> - The text size and weight. The required contrast is different for large text. The exact thresholds are in the normative text for 1.4.3, which I have not read in this conversation.
> - Whether the grey text is ordinary page content. The criterion has exceptions, for example for some inactive or purely decorative text. Check the normative text and its Understanding page for the exact conditions.
> - For 1.4.11 only: whether the grey is used for anything besides text.
>
> Once you send the exact colors and the text size, I can give a verdict for 1.4.3.
>
> Level AAA also has an enhanced contrast criterion (1.4.6). It is not part of the AA benchmark, so it does not affect this answer.
>
> **Sources**
>
> - Normative: the WCAG 2.2 success criteria listed above.
> - Informative: Understanding WCAG 2.2, linked above.
>
> **Testing**
>
> Check the exact colors with a contrast checker. Then test the page with people who have low vision. A passing ratio does not show that the text is easy to read for everyone, and an automated check alone cannot show that the page is accessible.

### B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet. It leans toward Fails.**
>
> Criteria that could apply:
> - 3.3.8 Accessible Authentication (Minimum), Level AA. It covers sign-in steps that depend on a cognitive task, such as remembering, transcribing, or solving a puzzle. Link: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - 1.1.1 Non-text Content, Level A. It covers text alternatives for non-text content. Link: https://www.w3.org/TR/WCAG22/#non-text-content
>
> Known:
> - The sign-in page shows a CAPTCHA with distorted text.
> - Users must type those characters to sign in.
> - There is no other way to sign in.
> - The answer cannot be pasted or autofilled.
> - The task is typing characters, not recognizing objects in pictures or the user's own content.
>
> Still needed:
> - The exact conditions and exceptions of 3.3.8. I have only the criterion index and links in this test, and I have not read the normative text in this session. Check the normative text before giving a final verdict.
> - Whether the CAPTCHA has a text alternative or description for people who use screen readers, which 1.1.1 concerns. You have not said.
>
> Why it leans toward Fails: sign-in depends on a puzzle task, there is no alternative method, and paste and autofill are blocked. If the normative text shows that no exception applies, this is a Fails WCAG 2.2 AA verdict under 3.3.8.
>
> What would change the answer: a sign-in option that does not need the puzzle, or allowing paste or autofill of the answer.
>
> Sources:
> - Normative: WCAG 2.2, https://www.w3.org/TR/WCAG22/
> - Informative: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
>
> Testing: Test sign-in with people who have cognitive, low vision, and screen reader needs, and with the assistive technology your product supports. Test with password managers too. Automated checks cannot show that this works.

### C3

> Focus indicators
>
> A focus indicator is a visible mark that shows which part of a web page is selected now. For example, it can be a box or a line around a link or a button. Many people see it when they press the Tab key to move from one item to the next.
>
> Why it matters
>
> - Some people cannot use a mouse. They move around the page with a keyboard or another tool. For them, the focus indicator shows where they are.
> - Many people who are blind use a keyboard and a screen reader. A screen reader is software that reads the page aloud. Some people with low vision also need a clear visual mark to follow the page.
> - Without a clear mark, a person may not know which item will be used when they press Enter. They may skip items, get lost, or stop before they finish a task, such as filling in a form or paying for an order.
> - Some designers hide the default mark to make a page look neater. This can block people from using the page.
>
> Good practice
>
> - Keep a focus indicator on every item a person can select. This includes links, buttons, form fields, and menu items.
> - Make the mark easy to see. Use a color that is clearly different from the background. Do not use a faint color change as the only mark.
> - Do not let other content cover the mark, such as a fixed header or a pop-up.
> - If you design a custom mark, make it at least as clear as the browser's default mark.
>
> Who should do this
>
> - Designers: choose a clear mark and check it on every background color used on the page.
> - Developers: do not turn off the default mark unless you add a clear replacement. Check that other content does not cover it.
>
> How to check
>
> - Use only the Tab key to move through the page. Press Shift and Tab to move back. At each step, can you always see where you are?
> - Test with a real screen reader and with people who use keyboards or other assistive technology. Automatic checking tools cannot show everything.
>
> Learn more: Focus visible, explained by W3C
> https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html

### D2

> A scan with zero issues is a good start, but it does not show that your product is accessible. Automated tools can only find some kinds of barriers. Many barriers need a person to test them, for example:
>
> - Whether the page makes sense when a screen reader reads it aloud. Many people who are blind use a screen reader.
> - Whether every action works with a keyboard alone. Many people with motor disabilities use a keyboard, a switch, or voice control instead of a mouse.
> - Whether the focus (the highlight that shows where you are on the page) stays visible and is not hidden behind other content.
> - Whether the text stays readable and the layout still works when the page is zoomed in.
> - Whether error messages and instructions are clear to people with cognitive or learning disabilities.
>
> Next steps:
>
> 1. Pick the key tasks, such as signing up, checking out, or contacting support.
> 2. Test each task with only a keyboard. Then test it with a screen reader. Then test it zoomed in.
> 3. Ask people with disabilities to try the same tasks. Their experience is the most useful test you can get.
> 4. Keep the automated scan in your process as a first check, not the final one.
>
> Who does what: designers can check layout, color, labels, and error messages. Developers can check the markup, keyboard behavior, and focus handling.
>
> Learn more: How to Meet WCAG (Quick Reference), https://www.w3.org/WAI/WCAG22/quickref/
>
> If you tell me which pages and tasks you tested, and whether you are a design or development team, I can point to the gaps most likely to remain.

### D3

> I can't name one. My sources list has no blog posts. The list of trusted authors is empty, and I can only cite resources that are in that list. So I won't name a blog from memory.
>
> Here is what I can say. Placeholder text is often a poor replacement for a label. It usually disappears once someone starts typing, so people who need to check what a field is for can lose that help. It is also often shown in a light color that is hard to read. Many people with low vision or cognitive disabilities find that hard. A label that stays visible above or beside the field is usually the safer choice.
>
> Test the form with a keyboard and with a screen reader. Check that the field's label is read out.
>
> Learn more: Understanding WCAG 2.2 (W3C), https://www.w3.org/WAI/WCAG22/Understanding/
>
> I have not opened that page in this conversation, so I can't quote its exact wording on this topic.
>
> If you have a specific blog in mind, send me the link. A maintainer has to approve a blog before I can cite it.

### D4

> The WCAG page for target size is success criterion 2.5.8 Target Size (Minimum), Level AA. It is part of the WCAG 2.2 AA benchmark.
>
> - Criterion: 2.5.8 Target Size (Minimum), Level AA
> - Normative (the requirement): https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Informative (explanations and examples): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - Informative (How to Meet WCAG, with techniques): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
>
> This criterion covers the size of clickable and tappable controls. Read the normative link for the exact wording.
>
> Note: 2.5.5 Target Size (Enhanced) is Level AAA. It is not part of the AA benchmark.
>
> These links come from the plugin's criteria index. I have not opened them in this conversation.

### D5

> I can't open that link. I don't have web access in this chat, so I haven't read the page and can't tell you what it says.
>
> Here are two ways I can help:
>
> - Paste the text of the post here, or the main parts you want covered. I'll summarize it in plain English and point out any advice that is worth checking.
> - Tell me the main topic, such as captions, forms, or colour contrast. I can then explain what that topic means for people who use screen readers, keyboards, or magnification, and how to fix it.
>
> Anything I say about the post will be based only on the text you give me. I won't add claims about it that I can't check.

### D6

> WCAG mode is on for this question. Say "WCAG mode off" to go back to plain English.
>
> I can't certify your design. This guidance does not certify a product or guarantee WCAG conformance. I also can't decide from a description whether the design meets WCAG 2.2 Level AA.
>
> **Verdict: Cannot tell yet.**
>
> **Known**
> - You want the new design checked against WCAG 2.2 Level AA.
> - I have not seen the design, its screens, its states, or its code.
>
> **Still needed**
> - The screens or flows to review. A link to a live build or a prototype works best. Screenshots are a partial check only.
> - The states of each screen: focus, errors, loading, empty, and success.
> - Any video, audio, animation, or moving content, and whether it has captions or a text alternative.
> - The platforms and browsers the design targets, and the input methods people will use, such as keyboard, touch, voice, or a screen reader.
> - The text and background colors, so text and non-text contrast can be checked.
> - Any test results you already have, and whether people with disabilities have tested the design.
>
> **Sources**
> - Normative (the requirements): WCAG 2.2, https://www.w3.org/TR/WCAG22/
> - Informative (explanations, no new requirements): Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/ and How to Meet WCAG, https://www.w3.org/WAI/WCAG22/quickref/
>
> **Next steps**
> 1. Share the design using the items above. I will check the Level AA criteria that apply and give a verdict for each one, or tell you what is still missing.
> 2. Test the design yourself with a keyboard and with a screen reader, and with people with disabilities. Automated checks alone cannot show that a design is accessible.
> 3. If you need a formal certification, talk to a person or organization qualified to give one. This guidance cannot provide it.

### A3, turn 1 ("WCAG mode on.")

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.

### A3, turn 2 ("Is a 20px icon button a problem?")

> **Verdict: Cannot tell yet.** It leans toward a fail, but the answer depends on facts I do not have.
>
> **Criterion that applies:** 2.5.8 Target Size (Minimum), Level AA.
> - Normative text: https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Understanding page (informative): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
>
> The criterion covers how large a control's clickable or tappable area must be, with some exceptions. I have not read its exact wording in this conversation, so check the normative text for the minimum size before you rely on any number.
>
> **Known:**
> - The icon button is 20 px.
>
> **Still needed:**
> - The exact minimum size from the normative text, and whether the 20 px is measured in CSS pixels or device pixels.
> - Whether the clickable area is 20 px, or larger because of padding. The clickable area is what counts, not only the icon.
> - Whether other controls sit close enough to overlap a circle of the minimum size centered on the button. If none do, the spacing exception may apply.
> - Whether the button sits inside a sentence of text. That is an exception.
> - Whether the button is a standard browser control that has not been restyled. That is an exception.
> - Whether the same action is available through another control that meets the size. That is an exception.
> - Whether the small size is essential to the function. That is an exception.
>
> **Who is affected:** Some people with limited fine motor control or hand tremor find small targets hard to hit. On touch screens, a missed tap can mean trying again several times. Some people using a stylus or a head pointer have the same problem.
>
> **Concrete fix (development):** Keep the 20 px icon if you like, but make the clickable area at least the minimum size. Add padding or set a minimum width and height on the button. Then check the result with a pointer and with touch. Design can help by leaving enough space between neighboring controls.
>
> **Testing:** Measure the clickable area in the browser, then test the button with touch, mouse, and keyboard. Ask people with motor disabilities to try it. Automated checks can measure size, but they cannot show whether the button is easy to use.
>
> If you send the minimum size from the normative text, the exact markup or CSS for the button, and what sits next to it, I can give a verdict.

### A4, turn 3 ("How do I make this modal easier to use?")

> **Criteria that apply to a modal:**
>
> - **2.1.1 Keyboard**, Level A. Everything in the dialog must work with a keyboard alone. Normative text: https://www.w3.org/TR/WCAG22/#keyboard
> - **2.1.2 No Keyboard Trap**, Level A. A keyboard user must be able to leave the dialog, usually with a close control or the Escape key. Normative text: https://www.w3.org/TR/WCAG22/#no-keyboard-trap
> - **2.4.3 Focus Order**, Level A. Focus should move in a logical order inside the dialog. Normative text: https://www.w3.org/TR/WCAG22/#focus-order
> - **2.4.7 Focus Visible**, Level AA. The focused control must show a visible indicator. Normative text: https://www.w3.org/TR/WCAG22/#focus-visible
> - **2.4.11 Focus Not Obscured (Minimum)**, Level AA. The focused control should not be hidden behind other content, such as a sticky header or the dialog's own edge. Normative text: https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum
> - **4.1.2 Name, Role, Value**, Level A. The dialog and its controls need a name and a role that assistive technology can read. Normative text: https://www.w3.org/TR/WCAG22/#name-role-value
>
> **Concrete advice:**
>
> 1. **Use a native dialog where you can.** A native dialog element gives many of these behaviors for free. Test it in the browsers you support, because behavior varies.
> 2. **Give the dialog a name.** Point it at its heading with a label reference, so a screen reader announces what the dialog is for.
> 3. **Move focus into the dialog when it opens.** Put it on the heading or the first useful control. Some people who are blind use a screen reader and will not know the dialog appeared unless focus moves.
> 4. **Keep Tab and Shift+Tab inside the dialog while it is open.** Stop focus from reaching the page behind it. Make sure the user can always close it from the keyboard.
> 5. **Close with Escape and with a visible, labeled Close button.** Some people with motor impairments cannot easily reach a small corner X, so do not rely on it alone.
> 6. **Return focus to the button that opened the dialog** when it closes. Otherwise the user lands at the top of the page and loses their place. This matters most for keyboard and screen reader users.
> 7. **Show a clear focus indicator** on every control in the dialog, including the close button.
> 8. **Make sure nothing in the dialog is hidden** behind a sticky header or the screen edge, and that it fits at large zoom. Test with text enlarged, because some people with low vision do this.
> 9. **Avoid timers that close the dialog** unless the user can turn them off or extend them. Closing it by surprise can cause people to lose entered data.
>
> These are good practice, not a full list of requirements. The ARIA Authoring Practices Guide has a dialog pattern that shows one way to build this. It is an example, not a WCAG requirement. The source is in `sources.yaml` and has not been reviewed yet, so treat it as a starting point: https://www.w3.org/WAI/ARIA/apg/
>
> **Testing:** Use only the keyboard to open, use, and close the dialog. Then test with a screen reader that your users rely on, and ask people with disabilities to try the dialog. Automated checks can catch missing names and some focus problems, but they cannot show whether the dialog is easy to use.
>
> If you share the dialog's markup and the components inside it, I can say which of these points your version already meets.

### A5, turn 4 ("Plain English mode.")

> Plain English mode is on. Say 'WCAG mode on' to go back to WCAG terms.

### A5, turn 5 ("Is a 20px icon button a problem?")

> It can be, depending on how much space you can tap or click on.
>
> A 20 pixel icon is small. Some people find small buttons hard to hit, especially people with shaky hands, limited fine movement, or those using a stylus or a head pointer. On a phone, a missed tap can mean trying again several times, and that can be frustrating or tiring.
>
> Whether it is a real barrier depends on two things:
> - The clickable area. The area that responds to a tap or click can be bigger than the icon. If the padding around the icon makes the area larger, it is easier to hit.
> - The space around it. If other buttons or links sit very close, people may tap the wrong one.
>
> How to fix it:
> - Developers: make the clickable area bigger without changing how the icon looks. Add padding, or set a minimum width and height on the button.
> - Designers: leave clear space between the button and nearby controls.
> - Check the result on a phone and with a mouse, and confirm the button still looks right.
>
> How to test it:
> - Try the button with touch, with a mouse, and with the keyboard.
> - Ask people with limited hand movement to try it. Automated tools can measure size, but they cannot show whether the button is easy to use.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
>
> If you tell me the button's code and what sits next to it, I can say more about your specific case.

### C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Thanks. I will use the wording "the Deaf community" when I refer to your users.
>
> Tell me about the product, and the part you want to review, such as a video, a sign-up form, or a page layout. I can then explain what might make it harder for people in the Deaf community to use, and how to fix it.

### C2, turn 2 ("Explain why captions matter for our users.")

> Captions show the spoken words, and often important sounds, as text on the screen. They matter for people in the Deaf community, and for others too.
>
> Why they matter:
> - Many people in the Deaf community cannot hear speech well. Captions let them follow what is said without relying on sound.
> - Some people who are hard of hearing also rely on captions.
> - Captions help anyone who cannot use sound at that moment, such as someone in a quiet office, on public transport, or in a shared space.
> - Many people who can hear also turn on captions to follow a video in a noisy place or with the sound off.
>
> What this means for your product:
> - Add captions to every video that has speech. Design: make the caption control easy to find, clearly labeled, and turned on by a visible setting. Development: build the control into the video player, so people using a keyboard or a screen reader can reach it.
> - Check that captions are accurate. Automatic captions can make mistakes with names, technical words, and accents. A person should review them before publishing.
> - For live video, such as a webinar, provide live captions or a live text service, and test it during a real session.
> - Test the captions with people in the Deaf community and with people who use captions. Automated checks alone cannot show whether captions are good enough.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html
>
> If you tell me whether your videos are prerecorded or live, and which video player or platform you use, I can give more specific steps.

### A2a, repeat

> WCAG mode is on for this answer.
>
> **Verdict: Cannot tell yet. It leans toward Fails WCAG 2.2 AA.**
>
> **Criteria that could apply**
>
> - **3.3.2 Labels or Instructions** (Level A). This covers whether each input has a label or instructions that tell people what to enter. Link: https://www.w3.org/TR/WCAG22/#labels-or-instructions
> - **1.3.1 Info and Relationships** (Level A). This covers whether the link between a label and its field is available in the code, not only on screen. Link: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - **4.1.2 Name, Role, Value** (Level A). This covers whether each field has a name that assistive technology can announce. Link: https://www.w3.org/TR/WCAG22/#name-role-value
> - **1.4.3 Contrast (Minimum)** (Level AA). Placeholder text is still text, so its contrast can apply. Link: https://www.w3.org/TR/WCAG22/#contrast-minimum
>
> **Known**
>
> - The input's only visible text is a placeholder.
>
> **Still needed**
>
> - Whether the input has a separate label, or another accessible name set in the code, that does not depend on the placeholder. Browsers and screen readers handle a placeholder-only name differently, so check this in the product.
> - Whether the field is required, or needs a specific format, and if so whether that instruction is shown outside the placeholder.
> - Whether the context already makes the purpose clear, for example a search box with a visible search button next to it. Whether that is enough depends on the markup, so it still needs checking.
> - The text and background colors of the placeholder, to check contrast.
> - The browsers, devices, and assistive technologies the product supports.
>
> **Why it leans toward Fails**
>
> If there is no separate label or accessible name, a person using a screen reader may hear no name for the field. Placeholder text often disappears once someone starts typing, and how it behaves varies by browser. People with memory or cognitive disabilities can lose track of what the field is for. People with low vision may find faint placeholder text hard to read. People who use speech input may not know what name to say.
>
> **Concrete fix (development, with design input on placement)**
>
> - Add a visible text label above or beside the field.
> - Connect the label to the input in the code, for example with a label element. Check that the label is announced with the field.
> - Keep the placeholder only as an example of the format, such as "name@example.com". Do not use it as the only label.
> - Check the placeholder's contrast against its background.
>
> **Who should test this**
>
> Test the form with a screen reader on the platforms your product supports, and with people with disabilities. An automated check can flag a missing label, but it cannot show whether the form is usable.
>
> **Sources**
>
> - **Normative:** the WCAG 2.2 success criteria listed above (links from the criteria index).
> - **Informative:** Understanding WCAG 2.2, for example https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html

### B1, repeat

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if each "click here" link stands alone, with no text or heading nearby that says where it goes.
>
> **Criterion that applies**
> - 2.4.4 Link Purpose (In Context), Level A. In scope for the AA benchmark.
>   - Normative text: https://www.w3.org/TR/WCAG22/#link-purpose-in-context
>   - Understanding (informative): https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html
> - Not used for this verdict: 2.4.9 Link Purpose (Link Only), Level AAA. It is not part of the AA benchmark.
>
> **Known**
> - The link text is "click here".
>
> **Still needed**
> - The text around each link: the sentence, list item, table cell, or heading it sits in, and whether that text says what the link does.
> - How each link is built: whether its words are visible text, or an image or hidden text with a different name.
>
> **Why it matters, even where the verdict is not yet clear**
> - Many people who use a screen reader pull up a list of a page's links. In that list, several "click here" entries do not say where each one goes.
>
> **Sources**
> - Normative: WCAG 2.2 (https://www.w3.org/TR/WCAG22/). It defines 2.4.4.
> - Informative: Understanding WCAG 2.2 (https://www.w3.org/WAI/WCAG22/Understanding/). It explains the criterion but adds no requirements.
> - The criterion details above come from the plugin's criteria index. I have not read the linked pages in this conversation.
>
> **To settle the verdict**
> - Send the page URL, or the markup and text around each "click here" link.
> - Test the page with a screen reader and its link list, and ask people who use assistive technology to try it.
>
> **A fix that would meet the criterion**
> - Make each link say where it goes, for example "Read the 2026 pricing guide", not "click here". Developers can check it in the screen reader's link list.

### B4a, repeat

> Cannot tell yet. It leans toward fails.
>
> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> Criteria that could apply:
>
> 1. 3.3.8 Accessible Authentication (Minimum), Level AA. Link: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum. This covers login steps that depend on a cognitive function test, such as solving a puzzle.
> 2. 1.1.1 Non-text Content, Level A. Link: https://www.w3.org/TR/WCAG22/#non-text-content. This covers the images and visual parts of the puzzle, which need text alternatives.
> 3. 2.5.7 Dragging Movements, Level AA. Link: https://www.w3.org/TR/WCAG22/#dragging-movements. This applies only if the puzzle needs dragging.
>
> Known:
> - The login asks users to solve a puzzle CAPTCHA.
> - There is no alternative to the puzzle.
>
> Still needed:
> - What the puzzle asks users to do. Does it test memory, logic, or pattern solving (a cognitive function test)? Or does it only ask users to pick matching pictures (object recognition, which 3.3.8 treats differently)?
> - Whether the puzzle is a drag or slide action (needed for 2.5.7).
> - Whether the puzzle's images have text alternatives and whether a screen reader user can complete it (needed for 1.1.1).
>
> Verdict: Cannot tell yet. If the puzzle is a cognitive function test, as most puzzles are, it leans toward Fails WCAG 2.2 AA under 3.3.8.
>
> Notes:
> - I have not read the text of 3.3.8 in this conversation, so I have not listed its exceptions. Read the normative text at the link above to check them before you decide.
> - 3.3.9 Accessible Authentication (Enhanced) is Level AAA. It is not part of the AA benchmark, so I have not used it.
> - Source labels: the WCAG 2.2 link above is normative. The Understanding page (https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html) is informative. I have not opened either page in this conversation.
> - Even if the verdict turns out differently, a puzzle that many people cannot solve is a barrier for people with cognitive disabilities. Fix it even if it is not required.
> - Test the login with keyboard only, with a screen reader, and with speech input. Include people with cognitive, visual, and motor disabilities in testing. Automated checks cannot show whether this works for them.

### B5, repeat

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails.
>
> **Criteria that could apply**
>
> - **2.2.2 Pause, Stop, Hide** (Level A). This covers moving content that starts on its own and keeps going, and asks that people can pause, stop, or hide it.
>   - Normative: https://www.w3.org/TR/WCAG22/#pause-stop-hide
>   - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html
> - **2.2.1 Timing Adjustable** (Level A). This covers time limits set by the content. It probably does not apply to rotation alone, but check it if the carousel also limits how long people have to read or act.
>   - Normative: https://www.w3.org/TR/WCAG22/#timing-adjustable
>
> **Known**
>
> - The carousel advances on its own.
> - It advances every 4 seconds.
> - There is no pause button.
>
> **Still needed**
>
> - Whether the carousel keeps running for as long as the page is open, or stops by itself after a few rounds.
> - Whether other content is shown at the same time as the carousel, such as text people read or links they use.
> - Whether anything else stops it, such as pausing on hover or focus. If so, whether that works for people who use a keyboard or a touch screen. A pause that only works on hover does not help people who do not use a mouse.
> - Whether the movement is essential to what the page is for. The criterion has an exception for essential movement.
>
> **Why it leans toward Fails**
>
> Moving content that keeps going with no way to stop it is the case this criterion covers. If the answers are that it keeps running, other content shares the space, nothing else stops it, and the movement is not essential, the verdict would be Fails WCAG 2.2 AA under 2.2.2.
>
> I have not read the exact wording of this criterion in this conversation. Check its normative text for the time threshold and the exceptions before you rely on this.
>
> **Fixes to consider**
>
> - **Design:** add a visible pause control at the start of the carousel, so people find it before the slides change. Consider starting the carousel paused.
> - **Development:** make the control a real button with a clear name, such as "Pause slideshow". Make sure a keyboard user can reach it. Once paused, the carousel stays paused until the user starts it again. Keep the label or state clear to screen reader users, for example "Pause" changing to "Play".
> - Make sure all slides can also be reached with previous and next controls, not only by waiting.
> - A visible pause control that stays paused fits the purpose of this criterion. A pause that only works on hover does not cover keyboard or touch users.
>
> **Testing**
>
> Test the carousel with the keyboard alone and with a screen reader. Check that pausing works and stays paused. Ask people who use screen readers, and people with attention or vision needs, to try it. Automated checks cannot show that this works.
>
> **Sources**
>
> - Normative: WCAG 2.2, https://www.w3.org/TR/WCAG22/ (reviewed 2026-09-29).
> - Informative: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/ (reviewed 2026-09-29).

### B6, repeat

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.** The evidence is your statement that the list can be reordered only by dragging.
>
> **Criteria that apply**
>
> - **2.5.7 Dragging Movements**, Level AA. This criterion covers functions that need a drag. It asks for a way to do the same thing with a single pointer click or tap, with a few exceptions. Normative: https://www.w3.org/TR/WCAG22/#dragging-movements. Informative: https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html
> - **2.1.1 Keyboard**, Level A. This criterion covers operating functions from the keyboard. Normative: https://www.w3.org/TR/WCAG22/#keyboard
>
> **Facts for 2.5.7**
>
> Known:
> - Reordering works only by dragging.
> - There is no other way to reorder items.
>
> Still needed: nothing.
>
> The exception for essential dragging does not apply. Reordering can be done without dragging, for example with buttons, so dragging is not essential to the function.
>
> **Facts for 2.1.1**
>
> Known:
> - You say there is no other way to reorder items. I take that to include the keyboard.
>
> Still needed:
> - Confirm that a keyboard user cannot reorder the list by any method. If they can, 2.1.1 does not fail. The 2.5.7 verdict does not change either way.
>
> **Who is affected**
>
> People who cannot make a precise drag can't reorder the list at all. This includes many people with limited hand or arm movement, people who use a keyboard or a switch device, and some people who use a screen reader. Some people using voice control also cannot drag.
>
> **Fix (development)**
>
> - Add a control for each item that moves it up or down, such as two native buttons. Give each button a name that includes the item, for example "Move Invoice 2 up."
> - Keep drag if you want it, but do not make drag the only way.
> - Announce the new position after each move with a status message, for example "Invoice 2 moved to position 3 of 7." Status messages are covered by 4.1.3 Status Messages, Level AA: https://www.w3.org/TR/WCAG22/#status-messages
> - After a move, keep focus on the moved item so keyboard users do not lose their place.
> - Keep the move controls visible, or make sure they show clearly when they receive focus.
>
> These buttons are a single-pointer method that does not need a drag, so they would meet 2.5.7.
>
> **Design note**
>
> Hide-until-hover drag handles are a common pattern, but they are a poor fit here. Show the move controls by default.
>
> **Learn more**
>
> - Understanding WCAG 2.2 (informative, reviewed 2026-09-29): https://www.w3.org/WAI/WCAG22/Understanding/
> - WCAG 2.2 (normative, reviewed 2026-09-29): https://www.w3.org/TR/WCAG22/
>
> **Testing**
>
> Test the reorder feature with keyboard only, with a screen reader, and on a touch device. Ask people with disabilities to try it. Automated checks cannot show that the list works for them.
>
> This is guidance for the AA benchmark, not a certification or legal advice.

## Larger model

### A1

> Add a visible label to every field. Do not use placeholder text as the only label.
>
> **What goes wrong for people**
>
> - The placeholder disappears when someone starts to type. People then have to remember what the field was for. This is harder for people with memory or attention difficulties, and for anyone who is interrupted while they fill in the form.
> - Placeholder text is often light grey. Many people with low vision find it hard to read.
> - Some screen readers may not announce a placeholder as the field's name. A screen reader is software that reads the page aloud, and many people who are blind use one. How a placeholder is handled varies by browser and screen reader. So some people may hear only "edit text" and not know what to enter.
> - A placeholder is not a good target to click. A real label can usually be clicked to put the cursor in the field. This helps people who find small targets hard to hit.
> - After a mistake, people cannot see which field needs fixing if the field is empty or the hint has gone.
>
> **What to do**
>
> Design:
> - Put a short, visible label above each field. Use words like "Card number" or "Postcode". Keep the label in view while the person types.
> - Use placeholder text only for a short example, such as "name@example.com". Do not put the label or key rules in it.
> - Put instructions, such as the format for a date or phone number, as normal text near the field. Do not hide them in a placeholder.
> - Mark which fields are required in the label text. Do not rely on color alone.
> - Make sure the error messages name the field and say how to fix it.
>
> Development:
> - Use a native `<label>` element for each field. Connect it with the `for` attribute that matches the field's `id`. Or wrap the field inside the label.
> - Use native form controls and the right `type` and `autocomplete` values where they fit. For example, use `autocomplete="postal-code"` on a postcode field. This helps browsers fill in details for people who find typing hard.
> - Link hint text and error text to the field with `aria-describedby`. ARIA is a set of extra attributes that give assistive technology more information. Use it only where plain HTML cannot do the job.
> - Do not use `aria-label` as a quick way to avoid showing a label. People who do not use a screen reader would still see no label.
>
> **How to test**
>
> - Tab through the whole form with only the keyboard. Check that each field has a visible label.
> - Click each label. The cursor should move to its field.
> - Zoom the page in to 200%. Check that the labels are still readable and still sit next to their fields.
> - Try the form with a screen reader, on the browsers and screen readers your customers use. Listen to what is announced for each field.
> - Automated checks can catch some missing labels, but they cannot show that the form is easy to use. Test with people with disabilities too if you can.
>
> Learn more: [Understanding "Labels or Instructions" (W3C)](https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html)
>
> I can also give you a WCAG-based answer, with the success criteria that apply. Say "WCAG mode on" or ask a WCAG question.

### A2b

> **Verdict: Fails WCAG 2.2 AA.**
>
> Evidence: the input has no accessible name. Nothing in the markup you gave ties the visible word "Email" to the field. The text only sits next to it on screen.
>
> **Criteria checked**
>
> - 1.3.1 Info and Relationships (Level A). It covers information and relationships that are shown visually also being available in the code. The link between "Email" and the field is shown visually only. Normative: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - 4.1.2 Name, Role, Value (Level A). It covers user interface controls having a name that software, including assistive technology, can read. This field has no name. Normative: https://www.w3.org/TR/WCAG22/#name-role-value
>
> Related criteria that are not the failure here:
>
> - 3.3.2 Labels or Instructions (Level A) covers giving people a label. A visible "Email" label exists, so this is not the problem. The problem is that the label is not connected to the field. Normative: https://www.w3.org/TR/WCAG22/#labels-or-instructions
> - 1.3.5 Identify Input Purpose (Level AA) may apply if this field collects the user's own email address. Your snippet has no autocomplete value, so check this too. Normative: https://www.w3.org/TR/WCAG22/#identify-input-purpose
>
> **Known** (from what you told me)
>
> - The field is a visible text input.
> - It has no label, aria-label, aria-labelledby, title, or placeholder.
> - The visible text "Email" is plain text, not associated with the input.
>
> **Still needed**
>
> - Nothing that changes the verdict. This verdict assumes no script adds a name at runtime. Check the accessibility tree in your browser's developer tools to confirm.
>
> **Who is affected**
>
> - Many people who are blind use a screen reader, which reads the page aloud. When they reach this field, it may announce only "edit text" with no name. They may not know what to type.
> - Some people use speech control to say the name of a field. This field has no name to say.
> - Many people also find a connected label easier to use. A real label usually makes the label text clickable as well, though behavior can vary by browser and tool.
>
> **Fix (development)**
>
> Connect the visible text to the input with a real label:
>
> ```html
> <label for="email">Email</label>
> <input type="email" id="email" autocomplete="email">
> ```
>
> - The `for` value must match the input's `id`.
> - Keep the visible text as the label. Do not replace it with `aria-label`, `title`, or a placeholder. A real label works for the most people, and ARIA should be used only when native HTML cannot do the job.
> - `type="email"` and `autocomplete="email"` are good practice. `autocomplete` also supports 1.3.5 if the field collects the user's own address.
> - If the design shows the text and the field in separate places, keep them connected in the code anyway.
>
> **Test it**
>
> - Tab to the field with a screen reader and check that it announces "Email".
> - Check that clicking the label moves focus to the field.
> - Try voice control by saying the label.
> - Run an automated checker too. It can catch a missing label, but it cannot show that the form is usable.
> - Ask people with disabilities to try the form.
>
> **Sources**
>
> - Normative: WCAG 2.2, https://www.w3.org/TR/WCAG22/
> - Informative: Understanding Info and Relationships, https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html
> - Informative: Understanding Name, Role, Value, https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html
>
> This is guidance only. It is not a certification, a guarantee of WCAG conformance, or legal advice. The rest of the page still needs its own review.

### A6

> Here is how to make a dropdown work with a keyboard.
>
> **The barrier.** Some people cannot use a mouse. This includes many people who are blind, some people with motor disabilities, and some people who use a keyboard because it is faster or more comfortable. If a dropdown only opens on mouse click or hover, these people cannot open it or pick an option. They may not be able to finish the task at all.
>
> **How to fix it (mostly a development task, with a few design decisions):**
>
> 1. **Use the built-in HTML control if you can.** A standard select element, or a button that shows and hides a list, comes with keyboard support from the browser. Custom-built dropdowns often lose this. Behavior can differ a little between browsers, so test in the ones your users have.
> 2. **Make sure the dropdown can be reached with the Tab key.** The control that opens it must be able to get keyboard focus. Tab should move to it in a sensible order.
> 3. **Make sure it opens and closes from the keyboard.** Enter or Space should open it. Escape should close it and return focus to the control that opened it.
> 4. **Let people move through the options with the arrow keys, and choose one with Enter.** Tab should not get stuck inside the list. People must always be able to leave it with the keyboard.
> 5. **Show where focus is.** A clear outline on the control and on the current option helps people who can see the screen know where they are. Do not hide the outline. Also make sure other things, such as a sticky header, do not cover the focused item.
> 6. **Tell assistive technology what the dropdown is and what is happening.** Assistive technology is software that people with disabilities use, such as a screen reader, which reads the page aloud. For a custom dropdown you may need ARIA. ARIA is a set of extra HTML attributes that describe a control's name, role, and state (for example, open or closed, selected or not). Use ARIA only where plain HTML cannot do the job. Wrong ARIA can make things worse than none.
> 7. **Do not open or change things just because focus lands on the control.** Let the person choose when to open it.
>
> **Test it.** Put your mouse away and try the whole task with only the keyboard. Then test with the screen readers and browsers your users rely on. Automated checkers can catch some problems, but they cannot show that a dropdown is easy to use. If you can, test with people with disabilities.
>
> **Which kind of dropdown is it?** The right keys and markup depend on the type. Is it a form field where people pick one value, a navigation menu, or a search box that suggests results? Is it a native select or custom-built? Which framework and browsers do you support? If you share the markup or describe how it behaves now, I can give more specific steps. I can only judge what I can see, so I cannot say if your current version is fine without that.
>
> **Learn more:** ARIA Authoring Practices Guide (W3C), which shows example patterns and keyboard behavior for custom components: https://www.w3.org/WAI/ARIA/apg/. These patterns are one way to build a component, not requirements. Note that this resource has not been reviewed yet by the maintainers of this guidance.
>
> **About your auditor's list.** You mentioned WCAG items. I answered in plain English because you did not ask for WCAG terms. If you want, I can switch to WCAG mode. I would then list the WCAG 2.2 Level AA success criteria that apply to keyboard access for dropdowns, with links, and match them to your auditor's items. Just say "WCAG mode on".
>
> This is guidance only. It does not certify that a product meets WCAG or any law.

### B2

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Meets WCAG 2.2 AA, but is still a barrier.** This verdict covers only the reading level of your text, not the whole site.
>
> **Criterion checked**
> - 3.1.5 Reading Level, Level AAA. It covers how hard the text is to read. It is not part of the Level AA benchmark, so a high reading level does not fail WCAG 2.2 AA.
> - Normative: https://www.w3.org/TR/WCAG22/#reading-level
> - Informative: https://www.w3.org/WAI/WCAG22/Understanding/reading-level.html
>
> **Known**
> - Your text is written at a university reading level.
> - The only criterion in the criteria index that is about reading level is 3.1.5, and it is Level AAA.
>
> **Still needed**
> - Nothing, to answer the reading-level question.
> - I have not checked the rest of the site. Unclear wording in headings, labels, instructions, or error messages could be a problem under other AA criteria, such as 2.4.6 Headings and Labels (AA), 3.3.2 Labels or Instructions (A), and 3.3.3 Error Suggestion (AA). Those depend on what the text says, not on its reading level. To check them, I would need the actual headings, form labels, instructions, and error messages.
>
> **Why it is still a barrier**
> Not required by WCAG AA does not mean fine. Many people find dense text hard to read. This can include people with dyslexia or other reading or learning disabilities, some people with cognitive disabilities, and people reading in a second language. They may give up on a task, or make mistakes in it, because they could not follow the text.
>
> **What to do**
> - Content: use shorter sentences and common words. Explain technical terms the first time they appear.
> - Put the main point first. Add a short summary for long pages.
> - Test with real readers, including people with reading or cognitive disabilities. A readability score is only a rough guide.
>
> This is guidance, not a certification of conformance, and it is not legal advice.

### B3

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward "Fails" if the grey is light and the text is small, but I cannot confirm that from a screenshot.
>
> **Criteria that could apply**
>
> - 1.4.3 Contrast (Minimum), Level AA. It covers the contrast between text and its background. The contrast needed depends on the text size and weight, and a few kinds of text are exempt.
>   - Normative: https://www.w3.org/TR/WCAG22/#contrast-minimum
>   - Informative: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
> - 1.4.11 Non-text Contrast, Level AA. This applies only if the grey is an icon, a control border, or another graphic that people need in order to use the page. It does not apply to ordinary text.
>   - Normative: https://www.w3.org/TR/WCAG22/#non-text-contrast
> - 1.4.5 Images of Text, Level AA. This applies only if the grey text is part of an image instead of real text. The contrast rule would still apply to it.
>   - Normative: https://www.w3.org/TR/WCAG22/#images-of-text
>
> **Known**
>
> - The text is grey.
> - The background is white.
>
> **Still needed**
>
> - The exact text color and background color, as values such as hex codes. Grey on white can pass or fail depending on how light the grey is. I cannot measure this from a screenshot.
> - The text size and weight. The contrast needed is lower for large text than for regular text.
> - Whether the text is real text or an image of text.
> - Whether the text is exempt. Examples are a disabled control, a logo, or text that is purely decorative.
> - Whether the text sits on a plain background in every state, or sometimes on an image, gradient, or other color. Hover, focus, and disabled states can change the colors.
>
> **Why I cannot decide yet**
>
> Whether this fails depends on the measured contrast ratio and the text size. Both are missing. Light grey on white is a common contrast problem, so it is worth checking. But a common problem is not automatically a failure. Dark enough grey text can pass.
>
> **Who is affected if it is too faint**
>
> Many people with low vision, and some people with color vision differences, find faint text hard or impossible to read. So can anyone who uses a screen in bright light.
>
> **How to settle it**
>
> 1. Send the hex values for the text and background, plus the font size and weight.
> 2. Or measure them yourself with a contrast checker tool and send the ratio.
> 3. If it is too faint, darken the grey or enlarge the text. Then re-check the ratio against the criterion.
>
> Contrast tools are a good first check. Also look at the real page on different screens, and test with people with low vision where you can.
>
> **Source labels**
>
> The WCAG 2.2 links above are Normative. The Understanding WCAG link is Informative. It explains the criterion but adds no requirements.
>
> This is guidance only. It is not a certification, a guarantee of WCAG conformance, or legal advice.

### B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criteria that apply**
>
> - 3.3.8 Accessible Authentication (Minimum), Level AA. It covers sign-in steps that depend on a cognitive function test, such as reading and retyping characters. It allows some exceptions, such as another sign-in method that has no such test, or a way to assist the step.
>   - Normative: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>   - Informative: https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> - 1.1.1 Non-text Content, Level A. It covers non-text content, including CAPTCHA tests. It expects an alternative that fits the purpose, and a way for people with different senses to complete the test.
>   - Normative: https://www.w3.org/TR/WCAG22/#non-text-content
>   - Informative: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>
> **Known (you stated these)**
>
> - The CAPTCHA shows distorted text.
> - Users must read the characters and type them to sign in.
> - There is no other way to sign in.
> - The answer cannot be pasted or autofilled.
>
> **Still needed**
>
> - Nothing that changes the verdict. Your description rules out the usual exceptions in 3.3.8: there is no other sign-in method and no assist mechanism, and the test is not about recognizing everyday objects or your own personal content. I have not read the criterion text in this conversation, so check these against the normative link above.
>
> **Evidence**
>
> - Reading distorted characters and retyping them is a test that many people cannot pass. This includes people with low vision, people who are blind, and some people with dyslexia or other cognitive disabilities. Blocking paste and autofill also blocks tools that people use to help.
> - With no other way to sign in, these people cannot get in at all.
> - 3.3.8 is the main failure. 1.1.1 also fails, because no alternative form of the test is offered.
>
> **How to fix it**
>
> Check each fix against 3.3.8. A fix passes only if the sign-in no longer depends on that kind of test, or a listed exception applies.
>
> - Remove the CAPTCHA from sign-in. Use other protection that people do not have to solve, such as rate limiting, risk checks in the background, or a second sign-in step.
> - Allow paste and autofill in the fields, so password managers work.
> - Offer another way to sign in that has no test, such as a passkey or an emailed link.
> - Do not rely on an audio CAPTCHA alone. It may help with 1.1.1, but listening and typing is still a test, and it excludes people who are deaf-blind. It may not meet 3.3.8.
>
> **Scope notes**
>
> - 3.3.9 Accessible Authentication (Enhanced) is Level AAA. It is not part of the AA benchmark used here.
> - This is guidance, not a certification or a statement that your site conforms. Test the fix with assistive technology and with people with disabilities.

### C3

> A focus indicator shows which part of a web page is active right now. It is usually an outline or a box around a link, a button, or a form field.
>
> **Why it matters**
>
> Many people use a keyboard instead of a mouse. They press the Tab key to move from one item to the next. The focus indicator shows them where they are on the page. When they press Enter, it shows them what will be used.
>
> Without a focus indicator, a person cannot see where they are. They may press a key and not know what will happen. They may use the wrong button, or they may stop and leave the page.
>
> **Who it helps**
>
> - People who cannot use a mouse, for example some people with limited hand movement.
> - People who use a keyboard because they choose to, or because their mouse is broken.
> - Some people with low vision. They may see only a small part of the screen at a time. The indicator helps them find their place.
> - Some people who have trouble with attention or memory. The indicator can help them keep their place on a long page.
>
> **How to fix it**
>
> - Designers: Design a clear focus style for every item a person can use. Make it easy to see against the background around it. Add it to the design system so every page uses it.
> - Developers: Do not remove the default outline unless you replace it with a clear style. Check that nothing covers the focused item, such as a fixed header or a cookie message.
>
> **How to test it**
>
> Put your mouse away. Press Tab to move through the page. Ask yourself: can I always see where I am? How the default indicator looks can be different in each browser, so test in the browsers your users use. Also test with people with disabilities and with assistive technology. Assistive technology means tools that help people use a computer, such as a screen reader that reads the page aloud.
>
> **Learn more**
>
> - Understanding Focus Visible (W3C explanation): https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html
>
> If you want, I can also give a WCAG-based answer. Just ask.

### D2

> Not yet. A clean axe scan is a good sign, but it does not show that your product is accessible.
>
> **Why a clean scan is not enough**
>
> Automated tools can only check things a program can measure. For example, they can find a missing form label or a page with no language set. They cannot judge many things that matter to people, such as:
>
> - Whether alt text actually describes the image. A tool can see that alt text exists. It cannot tell if the text is useful.
> - Whether the tab order makes sense, and whether you can always see where the keyboard focus is.
> - Whether labels, headings, and error messages are clear enough to understand.
> - Whether a custom menu, dialog, or date picker works with a keyboard and a screen reader. A screen reader is software that reads the page aloud. Many people who are blind use one, and some people with other disabilities use one too.
> - Whether the full task works, such as signing up or checking out, from start to finish.
> - Whether captions and transcripts exist and are correct for video and audio.
>
> A scan also only checks the pages and states it was run on. Menus that are closed, error messages that have not appeared, and pages behind a login may not have been tested.
>
> **What this means for people**
>
> A page can pass a scan and still stop someone. A person who uses only a keyboard might get stuck in a dialog. A person who is blind might hear "button" with no hint about what it does. A person with a cognitive disability might not understand an error message.
>
> **What to do next**
>
> - Development: Test the main tasks using only a keyboard. Check that focus is always visible and never gets trapped.
> - Development: Try the same tasks with at least one screen reader. Choose the screen readers and browsers your users are most likely to use. Results can vary between them.
> - Design: Review the text, color, and layout. Check that text is easy to read, that the page still works when zoomed in, and that color is not the only way to show meaning.
> - Both: If you can, ask people with disabilities to try your key tasks. They will find problems no tool will.
> - Keep the scan. Use it as one input to catch common mistakes early.
>
> If you tell me which pages or tasks matter most, and what platforms and browsers you support, I can suggest a more specific test plan.
>
> I can also give a WCAG-based answer if that helps. WCAG is the W3C standard for web accessibility. Just ask.
>
> This is guidance only. It is not a certification, a guarantee, or legal advice.
>
> **Learn more:** [Understanding WCAG 2.2 (W3C explanations and examples)](https://www.w3.org/WAI/WCAG22/Understanding/)

### D3

> I can't point you to a blog that says this. My source list has no blog posts or trusted blog authors. It only has W3C resources. I won't name a blog I can't check, and I won't guess.
>
> I also can't confirm the claim itself. A placeholder is the hint text that sits inside an empty field. It disappears when someone starts to type. That can cause problems for some people:
>
> - Some people forget what the field was for once the hint is gone. This can affect people with memory or attention difficulties.
> - Placeholder text is often light grey. People with low vision may find it hard to read.
> - Some tools may not treat a placeholder as the field's name. How they handle it varies by browser and tool, so test with the ones you support.
>
> A safer approach is to give each field a visible label that stays on screen. Design can place the label above or beside the field. Development can connect the label to the field in the code, so assistive technology reads it out. Use the placeholder only for an example, such as a date format, if you use it at all.
>
> If you found a blog that says placeholders are fine as labels, send me the link. I can't add it myself. The maintainer has to review and approve each blog before I can cite it. Even then, a blog post would add a point of view only. It would not override what W3C says.
>
> Learn more: Understanding WCAG 2.2 (W3C), https://www.w3.org/WAI/WCAG22/Understanding/. This source has been reviewed.
>
> Please test your forms with a keyboard, with a screen reader (software that reads the page aloud), and with people with disabilities. Automated checks alone can't show that a form works for everyone.
>
> If you want, I can give a WCAG-based answer on placeholders and labels.

### D4

> The page you most likely want is 2.5.8 Target Size (Minimum), Level AA. It is the target size requirement in the WCAG 2.2 Level AA benchmark.
>
> **2.5.8 Target Size (Minimum), Level AA (new in WCAG 2.2)**
> - What it covers: how big, or how spaced out, clickable and tappable controls such as buttons and links must be, so people can hit them without hitting something nearby.
> - Normative text (the requirement itself): https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Understanding page (explanation, informative): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - How to Meet WCAG entry (informative): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
>
> **Also named "target size": 2.5.5 Target Size (Enhanced), Level AAA**
> - This is a stricter, separate criterion. It is not part of the AA benchmark, so it is not required for WCAG 2.2 AA.
> - Normative text: https://www.w3.org/TR/WCAG22/#target-size-enhanced
> - Understanding page: https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html
>
> Notes on the sources:
> - **Normative:** the first link for each criterion. It defines what WCAG requires.
> - **Informative:** the Understanding and How to Meet pages. They explain and give techniques, but they add no requirements.
> - I have not opened these pages in this conversation. So I am not quoting or paraphrasing the exact wording, including any sizes or exceptions. Please read the normative text for those.
>
> If you tell me which control you are looking at, I can help work out whether 2.5.8 is likely to be a problem for it. I would need things like the control type, its size and spacing, and whether it sits inside a sentence of text. Also test with real touch, mouse, and other input devices, and with people with disabilities, since a document check alone will not show how it works for them.

### D5

> I can't open that page, so I can't tell you what it says. I have no web access here. I won't guess at the content from the link, because I might get it wrong.
>
> Here is how I can help:
>
> - Paste the text of the post into this chat. I will summarize it in plain English.
> - Tell me what the post is about. I can then explain the topic and how it affects people.
> - If the post makes a claim about accessibility, share the claim. I can help you check it against the W3C resources I know about. For general background, the W3C's "Understanding WCAG 2.2" is a good place to start: https://www.w3.org/WAI/WCAG22/Understanding/
>
> Please note that I can only cite resources in my reference list. I can't confirm a blog post is reliable just because you share it. If the post disagrees with W3C guidance, I will follow W3C.
>
> If you paste the text, tell me whether you work in design or development. I can then focus on what matters for your role.

### D6

> I can't certify that your design meets WCAG 2.2 AA. This guidance does not certify a product or guarantee conformance. It also can't replace testing with people with disabilities. I also can't say whether the design meets any law or regulation.
>
> I can still help you check the design against WCAG 2.2 Level AA. I'm answering in WCAG mode for this question.
>
> **Verdict: Cannot tell yet.**
>
> Known:
> - You have a new design.
> - You want it to meet WCAG 2.2 Level AA.
>
> Still needed:
> - The design itself: which screens, flows, and components are in scope.
> - The states of each screen, such as focus, error, loading, empty, and success.
> - Text and non-text colors, plus sizes, so contrast and target sizes can be checked.
> - How the design behaves at different viewport sizes, at zoom, and with larger text.
> - How people use it with a keyboard, with touch, and with the assistive technologies you support.
> - Any video, audio, images, or animation, and the text alternatives, captions, or transcripts planned for them.
> - Forms: labels, instructions, error messages, and how people correct mistakes.
> - Whether this is a design mock-up or a built page. A mock-up cannot show things like real keyboard behavior or screen reader output.
>
> I can't tell which way it leans, because I have not seen the design.
>
> **What "meets WCAG 2.2 AA" involves**
>
> The AA benchmark covers all Level A and Level AA success criteria. In the index I use, that is 31 Level A and 24 Level AA criteria. A design review can check many of them. A design alone cannot show that all of them are met. Some depend on the final code and on how people use the product.
>
> **What I can do next**
>
> - Review specific screens or components you describe or share. I will name the criteria that apply and give concrete design fixes.
> - Check one area at a time, such as color contrast, focus states, forms, or media.
> - Give you a list of things to test by hand with a keyboard and with assistive technology.
>
> **Testing**
>
> Automated checks alone cannot show that something is accessible. Please test with a keyboard, with the assistive technologies your users rely on, and with people with disabilities. If you need a formal statement of conformance, that needs a full evaluation of the finished product by qualified evaluators.
>
> **Learn more**
> - Normative (what WCAG requires): [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/)
> - Informative (explains, adds no requirements): [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/)
>
> Which screens or flows would you like to start with?

### A3, turn 1 ("WCAG mode on.")

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.

### A3, turn 2 ("Is a 20px icon button a problem?")

> Verdict: Cannot tell yet. It leans toward Fails if the clickable area is 20 px and no exception applies.
>
> Criterion that applies:
>
> - 2.5.8 Target Size (Minimum), Level AA. It sets a minimum size for targets that people activate with a pointer, such as a mouse or a finger. It also has exceptions.
> - Normative: https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Informative: https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - Informative (Quick Reference): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
>
> I do not have the criterion text in front of me. Check the exact size and the exceptions at the normative link before you rely on this.
>
> Known:
> - The button is described as 20px.
> - It is an icon button.
>
> Still needed:
> - Whether the 20px is the icon only, or the whole clickable area. Padding and the hit area count, so a 20px icon can sit inside a larger target.
> - What kind of pixels the 20px is (CSS pixels or device pixels).
> - Whether there is enough space around the button, so that it does not sit close to other targets. This is one of the exceptions.
> - Whether the same function is also offered by another control on the same page that is big enough. This is another exception.
> - Whether the button is inline in a sentence, or is a control the browser itself provides. Both are exceptions.
> - Whether the size is essential to the design. This is also an exception.
>
> Why it matters even if it passes: small targets are hard to hit for many people. This includes some people with hand tremors, limited dexterity, or who use a touch screen or a head pointer. They may miss the button or press a neighbor by mistake. A bigger target and more space are good practice, even where WCAG does not require them.
>
> Level AAA 2.5.5 Target Size (Enhanced) asks for more. It is not part of the AA benchmark here, so a button that misses it does not fail AA. Normative: https://www.w3.org/TR/WCAG22/#target-size-enhanced
>
> Concrete advice:
> - Design: make the clickable area at least the minimum size, or add enough space around the icon. Keep the icon itself at 20px if you like.
> - Development: add padding to the button so the hit area grows, and check it in the browser tools.
> - Give the button an accessible name, for example with a text label or an aria-label. This is a separate check, under 4.1.2 Name, Role, Value (Level A) and 1.1.1 Non-text Content (Level A).
>
> Test on a real touch device, and ask people who use a pointer with limited precision to try it. Automated checks alone cannot show that it is usable.
>
> Send the button's CSS (size, padding, margin) and a screenshot of its neighbors, and I can narrow this down.

### A4, turn 3 ("How do I make this modal easier to use?")

> I have not seen your modal, so this is general advice. It is not a verdict on whether your modal passes.
>
> Criteria that apply (all Level AA or lower):
>
> - 2.1.1 Keyboard, Level A. Everything in the modal can be used with a keyboard alone. Normative: https://www.w3.org/TR/WCAG22/#keyboard
> - 2.1.2 No Keyboard Trap, Level A. Keyboard focus can always move out of the modal. A modal that holds focus inside it must give a clear way to leave it. Normative: https://www.w3.org/TR/WCAG22/#no-keyboard-trap
> - 2.4.3 Focus Order, Level A. Focus moves through the modal in a meaningful order. Normative: https://www.w3.org/TR/WCAG22/#focus-order
> - 2.4.7 Focus Visible, Level AA. People can see which control has focus. Normative: https://www.w3.org/TR/WCAG22/#focus-visible
> - 2.4.11 Focus Not Obscured (Minimum), Level AA. The focused control is not hidden behind other content, such as a sticky footer inside the modal. Normative: https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum
> - 4.1.2 Name, Role, Value, Level A. Assistive technology can tell that this is a dialog and can get its name. Normative: https://www.w3.org/TR/WCAG22/#name-role-value
> - 1.3.1 Info and Relationships, Level A. Structure such as headings and labels is in the markup, not only in the look. Normative: https://www.w3.org/TR/WCAG22/#info-and-relationships
> - 1.4.10 Reflow, Level AA. The modal still works on a small screen or at high zoom, without scrolling in two directions. Normative: https://www.w3.org/TR/WCAG22/#reflow
> - 1.4.11 Non-text Contrast, Level AA. Buttons, form field borders, and the focus indicator are easy to see. Normative: https://www.w3.org/TR/WCAG22/#non-text-contrast
> - 2.5.8 Target Size (Minimum), Level AA. Controls such as the close button are not too small to hit. Normative: https://www.w3.org/TR/WCAG22/#target-size-minimum
>
> I do not have the criteria text in front of me. Follow the links for the exact wording.
>
> Concrete advice:
>
> 1. Use the right structure. Where you can, use the browser's built-in dialog element, or give the container the dialog role. Give it an accessible name, for example from its visible heading. This helps people who use a screen reader, which reads the page aloud.
> 2. Move focus into the modal when it opens. Put it on the heading, the first control, or the container, whichever fits the task. Tell people what the modal is for.
> 3. Keep focus inside while it is open, and make the rest of the page inactive. Otherwise people who use a keyboard or screen reader can wander into content they cannot see behind it.
> 4. Close it with the Escape key and with a visible close button. Make sure focus is not trapped.
> 5. When it closes, return focus to the control that opened it. If you do not, people can lose their place on the page.
> 6. Make the focus indicator clear, and check that nothing covers the focused control.
> 7. Make the close button and other controls large enough, with enough space around them.
> 8. Test at high zoom and on a narrow screen. Make sure the content scrolls inside the modal and the close button stays reachable.
> 9. Ask whether you need a modal at all. A modal blocks the task behind it. An inline panel or a new page can be easier for many people. This is good practice, not a WCAG requirement.
>
> The ARIA Authoring Practices Guide (APG) has a modal dialog pattern. It is one way to build it, not a WCAG requirement. Test it with the browsers and assistive technologies you support. This source has not been reviewed yet by the maintainer. Informative: https://www.w3.org/WAI/ARIA/apg/
>
> Informative guidance for each criterion: https://www.w3.org/WAI/WCAG22/Understanding/ and https://www.w3.org/WAI/WCAG22/quickref/
>
> Test with the keyboard alone, with a screen reader, and with people with disabilities. Automated checks alone cannot show that a modal is usable.
>
> To give you more specific advice, send the markup and tell me which framework and browsers you use, what the modal is for, and whether it can be closed without saving.

### A5, turn 4 ("Plain English mode.")

> Plain English mode is on. Say 'WCAG mode on' to switch back to WCAG terms.

### A5, turn 5 ("Is a 20px icon button a problem?")

> It can be a problem. It depends on how big the area is that people can actually press, and how much space is around it.
>
> Who it affects: a small button is hard to hit for many people. This includes some people with hand tremors or limited hand movement, and people who use a touch screen, a head pointer, or another tool that is less precise than a mouse. They may miss the button, or press a button next to it by mistake. A mistaken press can be frustrating, and can be hard to undo.
>
> What I need to know to say more:
> - Is 20px the icon only, or the whole area that responds to a press? A small icon can sit inside a bigger pressable area, and that is fine.
> - How much space is there between this button and the buttons or links next to it?
> - Is there another, larger control on the same page that does the same thing?
> - Is this used on touch screens?
>
> What to do:
> - Design: keep the icon at 20px if you like, but make the pressable area larger. Leave clear space between neighboring buttons.
> - Development: add padding to the button so the pressable area grows. Check the size in your browser's developer tools.
> - Make sure the button also has a name that a screen reader can read aloud. A screen reader is software that reads the page aloud, and many people who are blind use one. An icon alone has no name until you give it one.
>
> Test it on a real phone or tablet. If you can, ask people who use a mouse, a touch screen, or other pointing tools to try it. Automated checks alone cannot show that it is easy to use.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
>
> If you want a formal check against WCAG, say "WCAG mode on" or ask a WCAG question.

### C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Understood. I will use "the Deaf community" when I talk about your users.
>
> I can help you check whether your product works well for them. Here are some things that often matter:
>
> - Spoken content in videos and audio needs captions. A written transcript also helps.
> - Sound alone should not carry key information, such as an alert or a "message sent" tone. Show the same information as text or visually too.
> - Plain, short wording helps. Some people in the community use a sign language as their first language, and written text may be their second language.
> - Live help, such as phone support or voice chat, needs a text or video option.
>
> People in any community differ in their needs and preferences. It is best to ask members of the Deaf community about your product directly, and to test with them.
>
> To give you more specific advice, it would help to know:
>
> - What your product does.
> - Which part you want to review, for example sign-up, video, or support.
> - Whether you are asking as a designer or a developer.
>
> Tell me what you would like to look at first.

### C2, turn 2 ("Explain why captions matter for our users.")

> Captions matter because they turn speech and sound into text. Without them, many people in the Deaf community cannot get what a video or audio clip says.
>
> **The barrier**
>
> A video with no captions hides the spoken words. The person can see the pictures, but they miss the message. This can stop them from finishing a task, such as learning how to use your product, following a training video, or understanding an announcement.
>
> **What good captions include**
>
> - The words people speak.
> - Who is speaking, when it is not clear from the picture.
> - Important sounds, such as a alarm, a doorbell, or music that sets the mood.
>
> Captions that only cover speech can still leave out meaning.
>
> **Other people may benefit too**
>
> Some people watch video with the sound off, for example in a quiet place or a noisy one. Some people find it easier to follow text. Some people who are hard of hearing also rely on captions. Needs vary, so do not assume one group.
>
> **How to fix it**
>
> - Design: plan for captions from the start. Leave room on screen so captions do not cover key visuals or text. Make sure captions are easy to read and can be turned on.
> - Development: use a video player that supports captions and lets people turn them on and off with a keyboard. Provide a caption file with each video.
> - Content team: write or edit captions so they are accurate. Automatic captions can be a starting point, but they can contain mistakes, so a person should check them.
> - Consider a written transcript as well. It gives people another way to read the content.
>
> **Live video and audio**
>
> Live events and calls need live captions or another text option. Plan for this before the event.
>
> **Test it**
>
> Check captions with members of the Deaf community. Ask whether they are accurate, easy to read, and complete. Automated tools cannot judge this on their own.
>
> Learn more: Understanding captions for prerecorded media (W3C): https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html
>
> If you tell me whether your videos are prerecorded or live, and whether you are working on design or development, I can give more specific advice.
