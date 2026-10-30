# Raw replies, re-run with updated instructions: larger model

Replies from the larger of the two models used in the re-run, one run per case, exactly as written to file. Each agent read only the five plugin files at commit `50e02cf` and had no web access. See `rerun-results.md` for scoring and caveats.

## A1

> Add a visible label to every field in the checkout form. Keep the placeholder only as an optional extra hint, not as the label.
>
> **The barrier**
>
> A placeholder is the grey example text inside an empty field. It has several problems when it is the only label:
>
> - It usually disappears when a person starts typing. People who have memory or attention difficulties may then forget what the field asked for. Anyone who wants to check or fix an entry before paying has to delete it to see the prompt again.
> - Placeholder text is often light grey. People with low vision may find it hard to read.
> - It may not be exposed to assistive technology (tools such as screen readers, which read page content aloud) as the name of the field. This varies by browser and tool. A person who is blind and uses a screen reader may hear only "edit text" and not know what to enter.
> - People who use speech control (software that lets you operate the page by voice) may not be able to say a name to reach a field that has no label.
> - A checkout form asks for personal and payment details. A field that is unclear can lead to a wrong entry, a failed order, or a person giving up.
>
> **What to do**
>
> Design:
> - Put a short, clear label above each field. Use the words people expect, such as "Email address" or "Card number".
> - Keep the label visible at all times, including while the person types.
> - Mark required fields and give format hints (for example, the date format) in text near the label, not only in the placeholder.
> - If you want an example inside the field, make it extra help only. Make sure it has enough contrast with the background.
>
> Development:
> - Use a real `<label>` element for each field and connect it to the field with matching `for` and `id` values. Native HTML does this well, so you rarely need ARIA (extra attributes that add meaning for assistive technology).
> - Put format hints in a separate element and link it to the field with `aria-describedby`.
> - Group related fields, such as a delivery address or card details, with `<fieldset>` and `<legend>`.
> - Where it fits, add `autocomplete` attributes to fields such as name, address, and card number. This helps browsers fill them in and helps people who find typing hard.
> - Make error messages name the field and say how to fix the problem.
>
> **How to check**
>
> - Tab through the form with only the keyboard. Each field should have a visible label and a clear focus outline.
> - Try the form with a screen reader and with speech control, in the browsers your customers use. Automated tools can find missing labels, but they cannot show that the labels make sense.
> - If you can, test with people with disabilities.
>
> If you tell me which framework or component library you use, and whether any labels are added in script or hidden with CSS, I can give more specific advice.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html
>
> If you want this explained in terms of WCAG, say "WCAG mode on" and I will list the criteria that apply.

## A2a

> **Cannot tell yet.** It leans toward a failure, but the answer depends on facts about the markup and the page that your question does not include.
>
> **Why I cannot decide**
>
> A placeholder-only input is a practice that WCAG does not name directly. What matters is whether the field still meets the criteria below. These are the ones that apply:
>
> - **3.3.2 Labels or Instructions (Level A).** Covers giving people labels or instructions when content asks them to enter information. [Normative](https://www.w3.org/TR/WCAG22/#labels-or-instructions) | [Understanding (informative)](https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html)
> - **1.3.1 Info and Relationships (Level A).** Covers whether the label's relationship to the field can be worked out from the code, not only from how the page looks. [Normative](https://www.w3.org/TR/WCAG22/#info-and-relationships) | [Understanding (informative)](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html)
> - **4.1.2 Name, Role, Value (Level A).** Covers whether the field has a name that assistive technology can get. [Normative](https://www.w3.org/TR/WCAG22/#name-role-value) | [Understanding (informative)](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html)
> - **1.4.3 Contrast (Minimum) (Level AA).** Covers the contrast of text, which includes placeholder text. Placeholder text is often light grey. [Normative](https://www.w3.org/TR/WCAG22/#contrast-minimum) | [Understanding (informative)](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)
> - **2.4.6 Headings and Labels (Level AA).** Covers whether labels describe the purpose of the field. [Normative](https://www.w3.org/TR/WCAG22/#headings-and-labels) | [Understanding (informative)](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels.html)
>
> I have not read the text of these criteria in this conversation, so I am not quoting them. Follow the links for the exact wording. Whether a placeholder alone counts as a sufficient label under these criteria depends on how it is built and shown. I will not guess.
>
> **What I need to give a verdict**
>
> 1. The markup for the input. Is there a `<label>`, `aria-label`, or `aria-labelledby`, or only a `placeholder` attribute?
> 2. Whether any visible text label stays on screen after the person starts typing.
> 3. The contrast ratio of the placeholder text against its background.
> 4. Whether the placeholder is the only place that says what to enter, such as a format or a required field.
> 5. The browsers and assistive technologies you support. How browsers and assistive technology treat a placeholder varies, so test in the ones you support.
>
> **Which way it leans**
>
> - If the placeholder is the only label, the text disappears as soon as someone types. People who need to check what a field is for, such as people with memory or attention difficulties, then have no visible prompt. That is a barrier even if a criterion is technically met.
> - If the field has no accessible name in the code, expect a failure of 4.1.2 and likely 1.3.1.
> - If the placeholder text has low contrast, expect a failure of 1.4.3.
>
> **Fix (design and development)**
>
> - Design: show a visible label that stays on screen. Use the placeholder only for a short example, if at all.
> - Development: use a native `<label for="...">` linked to the input's `id`. Use native HTML before ARIA. Make sure any placeholder text still has enough contrast.
> - This fix works for the criteria above because the label is visible, persistent, named in the code, and linked to the field.
>
> **Source types**
>
> The success criteria links are normative (they define what WCAG requires). The Understanding links are informative (they explain but add no requirements). I have not used any other-perspective sources.
>
> Please also test with assistive technology and with people with disabilities. Automated checks alone cannot show that a field is accessible. This is guidance only. It is not a certification of conformance or legal advice.
>
> Share the markup and a screenshot of the field in its typing state, and I can give a verdict.

## A2b

> **Fails WCAG 2.2 AA.**
>
> Evidence: the input has no accessible name from any source. It has no `label`, `aria-label`, `aria-labelledby`, or `title`. The word "Email" is only plain text next to it, so nothing in the code links that word to the field. The label is visible to people who can see the page, but it is not available to assistive technology (tools such as screen readers and voice control software).
>
> Criteria that apply (all Level A, so they are part of the AA benchmark):
>
> - **4.1.2 Name, Role, Value (Level A).** This criterion covers whether user interface components, including form fields, expose a name that software can determine. This input has no name, so this is the clearest failure. Normative: https://www.w3.org/TR/WCAG22/#name-role-value
> - **1.3.1 Info and Relationships (Level A).** This criterion covers whether relationships shown visually, such as a label next to a field, are also available in the code. Here the visual link between "Email" and the field is missing from the code. Normative: https://www.w3.org/TR/WCAG22/#info-and-relationships
>
> Related criteria that this snippet does not fail:
>
> - **3.3.2 Labels or Instructions (Level A).** It covers whether fields have labels or instructions. A visible label exists, so this likely does not fail on these facts. The missing code link is better judged under the two criteria above.
> - **2.4.6 Headings and Labels (Level AA).** It covers whether labels describe their purpose. "Email" describes the purpose, so this likely does not fail.
>
> Who is affected: people who use a screen reader may find the field without a name. People who use voice control may not be able to say a name to reach it. Behavior varies by browser and tool, so test with the ones your users rely on.
>
> Fix (development):
>
> ```html
> <label for="email">Email</label>
> <input type="text" id="email">
> ```
>
> This fix gives the field a name that software can read, and it keeps the visible text. That meets the naming requirement in 4.1.2 and the relationship requirement in 1.3.1. Native `label` is better than adding `aria-label`, because the visible text and the name stay the same. Also consider `type="email"`. If this field collects the user's own email address, `autocomplete="email"` relates to 1.3.5 Identify Input Purpose (Level AA). I cannot tell from this snippet whether 1.3.5 applies.
>
> Source labels:
>
> - Normative: the WCAG 2.2 success criteria linked above, and the full spec at https://www.w3.org/TR/WCAG22/
> - Informative: Understanding WCAG 2.2 for each criterion. Learn more: https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html and https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html
>
> Limits: this verdict is based only on the snippet and your description. If other code outside the snippet gives the field a name, the result could change. Automated checks alone cannot show that a form is accessible, so test with assistive technology and with people with disabilities.

## A3, turn 1 ("WCAG mode on.")

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.

## A3, turn 2 ("Is a 20px icon button a problem?")

> **Cannot tell yet.**
>
> The criterion that applies is 2.5.8 Target Size (Minimum), Level AA. It sets a minimum size for pointer targets such as buttons. It also has exceptions, and I do not have its text in front of me in this conversation, so I am not quoting the size or the exceptions. Please check them at the normative link before you decide.
>
> - Normative: [2.5.8 Target Size (Minimum)](https://www.w3.org/TR/WCAG22/#target-size-minimum)
> - Informative: [Understanding 2.5.8](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
> - Informative: [How to Meet 2.5.8](https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum)
>
> A size of 20px alone does not decide the result. I need these facts:
>
> 1. Is "20px" the size of the clickable area in CSS pixels, or only the icon image? Padding can make the clickable area larger than the icon.
> 2. How much space is there between this button and the buttons or links next to it?
> 3. Is the button inline in a sentence or block of text?
> 4. Is there another control on the page that does the same thing and meets the size requirement?
> 5. Is the size set by the browser or other user agent, and not changed by your CSS?
> 6. Is the size essential to what the button does?
>
> These facts matter because the criterion has exceptions. Each one can change the verdict. If the clickable area is under the minimum, and none of the exceptions apply, the answer leans toward "Fails". I will not guess before I know.
>
> Not required by WCAG does not mean fine. A small button can still be hard to hit for people with tremors, limited dexterity, or large fingers. It is also hard on small touch screens. This is true even if the button meets the criterion.
>
> Fixes:
>
> - Design: make the clickable area larger than the icon. Keep the icon at 20px and add space around it.
> - Development: set the padding or the `min-width` and `min-height` on the button so the whole padded area is clickable. Check that the focus outline still looks right.
> - Design: leave space between neighboring targets so people do not tap the wrong one.
>
> Also check that the icon button has an accessible name (a text label that assistive technology can read). That falls under 4.1.2 Name, Role, Value, Level A, and is a separate check from size.
>
> - Normative: [4.1.2 Name, Role, Value](https://www.w3.org/TR/WCAG22/#name-role-value)
>
> Test with a mouse, a touch screen, and a keyboard. Test with assistive technology and with people with disabilities too. Automated checks alone cannot show that a button is easy to use.
>
> If you send the button's markup and CSS, plus the surrounding layout, I can give a firmer verdict.

## A4, turn 3 ("How do I make this modal easier to use?")

> Here are the WCAG 2.2 AA criteria that apply to a modal, then concrete advice. I do not have the criterion text in front of me in this conversation, so I describe each one in general terms. Check the normative link for exact wording.
>
> **Criteria that apply (normative links)**
>
> - [2.1.1 Keyboard](https://www.w3.org/TR/WCAG22/#keyboard), Level A: everything in the modal can be used with a keyboard.
> - [2.1.2 No Keyboard Trap](https://www.w3.org/TR/WCAG22/#no-keyboard-trap), Level A: keyboard focus can always be moved away from the modal. People must be able to close it with the keyboard.
> - [2.4.3 Focus Order](https://www.w3.org/TR/WCAG22/#focus-order), Level A: focus moves through the modal in a logical order, and goes to a sensible place when the modal opens and closes.
> - [2.4.7 Focus Visible](https://www.w3.org/TR/WCAG22/#focus-visible), Level AA: the control that has keyboard focus can be seen.
> - [2.4.11 Focus Not Obscured (Minimum)](https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum), Level AA: other content, such as a sticky bar, does not hide the focused control.
> - [4.1.2 Name, Role, Value](https://www.w3.org/TR/WCAG22/#name-role-value), Level A: the dialog and its controls have an accessible name and role that assistive technology can read.
> - [1.4.10 Reflow](https://www.w3.org/TR/WCAG22/#reflow), Level AA: the modal content can be used at high zoom or on a narrow screen without scrolling in two directions.
> - [2.5.8 Target Size (Minimum)](https://www.w3.org/TR/WCAG22/#target-size-minimum), Level AA: the close button and other controls are large enough to hit.
> - [1.4.11 Non-text Contrast](https://www.w3.org/TR/WCAG22/#non-text-contrast), Level AA: the close icon and the focus indicator have enough contrast against their background.
>
> If the modal has a form, also check [3.3.1 Error Identification](https://www.w3.org/TR/WCAG22/#error-identification) (A) and [3.3.2 Labels or Instructions](https://www.w3.org/TR/WCAG22/#labels-or-instructions) (A). If it shows a message that appears without moving focus, such as "Saved", check [4.1.3 Status Messages](https://www.w3.org/TR/WCAG22/#status-messages) (AA).
>
> Informative explanations are in [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/) and the [How to Meet WCAG Quick Reference](https://www.w3.org/WAI/WCAG22/quickref/). They explain but do not add requirements.
>
> **Advice**
>
> Development:
>
> 1. Use the native HTML `<dialog>` element opened with `showModal()` where you can. Native behavior is the first choice before custom ARIA (Accessible Rich Internet Applications attributes). Browser and assistive technology support varies, so test it in the ones you support.
> 2. Move focus into the modal when it opens. Put it on the first useful control, or on the dialog heading if the content is long.
> 3. Return focus to the button that opened the modal when it closes.
> 4. Make sure the Escape key and a visible close button both close the modal.
> 5. Give the dialog an accessible name. Point `aria-labelledby` at the visible heading.
> 6. Keep the page behind the modal from being reached while it is open. A native modal dialog does this for you. With custom code, use the `inert` attribute on the background content.
> 7. Give the close button a text name, such as "Close". If it is an icon only, add an accessible name.
> 8. Do not let sticky headers or footers cover the focused control inside the modal.
> 9. Let the modal scroll inside itself at high zoom and narrow widths. Do not cut off content.
>
> Design:
>
> 1. Keep the close button easy to see and big enough to hit. Put it in a consistent place.
> 2. Use a clear heading, short text, and one main action. Make the button names say what they do, for example "Delete account" and "Cancel".
> 3. Design a visible focus style with enough contrast.
> 4. Do not open a modal without the person asking for it. If you must, make it easy to dismiss.
>
> **Not required by WCAG, but still helpful:** keep the modal short, avoid stacking one modal on another, and do not time out the modal. These help people with cognitive, motor, and low vision needs. They are good practice, not WCAG requirements at AA.
>
> **Test**
>
> - Use only the keyboard: Tab, Shift+Tab, Enter, Space, and Escape.
> - Check where focus goes on open and on close.
> - Test with a screen reader (software that reads the screen aloud) in the browsers you support. Results vary by browser and tool.
> - Test at 400% zoom and on a narrow screen.
> - Test with people with disabilities. Automated checks alone cannot show that a modal is accessible.
>
> I have not seen your modal, so I cannot say whether it passes or fails. If you want that check, send the markup, the CSS, and a description of what it does when it opens and closes. Say also if it is a native `<dialog>` or a custom build, and which browsers and assistive technology you support. That could change the advice.

## A5, turn 4 ("Plain English mode.")

> Plain English mode is on. Say 'WCAG mode on' to go back to WCAG terms.

## A5, turn 5 ("Is a 20px icon button a problem?")

> It can be. A small button is harder to hit. Whether it is a problem depends on a few things, listed below.
>
> **Who it affects**
>
> - People with hand tremors or limited hand control may miss the button or press the wrong one.
> - People who use a finger on a touch screen may press the wrong button, most of all when buttons sit close together.
> - People with low vision may find a small icon hard to see.
>
> **What happens to them**
>
> They may need several tries to press the button. They may trigger a different action by mistake. Some may give up on the task.
>
> **What I need to know**
>
> 1. Is 20px the size of the whole clickable area, or only the icon? Padding can make the clickable area bigger than the icon.
> 2. How much space is there between this button and the controls next to it?
> 3. Is the button part of a line of text?
> 4. Does the icon have a text label, or only the picture?
>
> **How to fix it**
>
> - Design: make the clickable area larger than the icon. You can keep the icon at 20px and add space around it.
> - Design: leave clear space between neighboring buttons.
> - Development: add padding to the button, or set a minimum width and height, so the whole padded area can be pressed.
> - Development: give the icon button a text name so assistive technology (tools that people with disabilities use to work with a device) can announce what it does.
>
> **Test it**
>
> Try the button with a mouse, with a finger on a touch screen, and with a keyboard. Ask people with disabilities to try it too. Automated checks alone cannot show that a button is easy to use.
>
> Learn more: [W3C explanation of small touch and click targets](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html)
>
> I can also give a WCAG-based answer if you want one.

## A6

> The barrier: if a dropdown only works with a mouse or touch, people who use only a keyboard cannot open it or pick an option. This can affect people with motor disabilities, people who are blind, and anyone who cannot use a mouse. They may be stuck at that step and unable to finish the task.
>
> How to fix it:
>
> 1. Development: use the built-in HTML control if you can. A native select element (the standard HTML dropdown) already works with the keyboard in browsers. Its exact keys and look can vary by browser, so test the ones you support.
>
> 2. If you need a custom dropdown, development should build in these behaviors:
>    - People can reach the dropdown with the Tab key, and it shows a clear focus outline.
>    - People can open it, move through the options, choose one, and close it using the keyboard alone.
>    - Focus never gets stuck inside the dropdown. People can always leave it with the keyboard.
>    - After a choice, focus goes to a sensible place, such as back to the dropdown button.
>    - Screen readers (software that reads the screen aloud) need to be told what the control is, what it is called, and whether it is open or closed. Use ARIA (extra code attributes that describe custom controls to assistive technology) only where native HTML cannot do this. Wrong ARIA can make things worse than none.
>
> 3. Design: show a visible focus state on the dropdown and on the option that is currently highlighted. Make sure the open list is not hidden behind other content, such as a sticky header.
>
> 4. Test it. Put your mouse away and complete the task with the keyboard only. Then test with a screen reader and, if you can, with people with disabilities. Automated checks alone cannot show that a dropdown works well.
>
> To give you more exact advice, it would help to know:
> - Is it a native select element or a custom one built from div or button elements?
> - Does it only select one option, or can it select several? Does it have a search box?
> - Which browsers and devices do you support?
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html
>
> You mentioned that your auditor listed WCAG items. If you share them, I can switch to WCAG mode and match each item to the right success criterion. Just say "WCAG mode on".

## B1

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward a fail if the link has no helpful context, but I need a few facts before I can say "Fails".
>
> **Criterion checked:** 2.4.4 Link Purpose (In Context), Level A. It covers whether people can work out where a link goes or what it does. This can come from the link text alone, or from the link text together with its surrounding context. The wording "click here" alone does not decide the result. What decides it is whether the purpose can be worked out from the link text plus its context.
>
> **What I need to decide:**
> - The markup for a few example links, including the sentence, paragraph, list item, table cell, or heading around each one.
> - Whether the link has an accessible name or description set in code that adds meaning (for example with `aria-label`, `aria-labelledby`, or `aria-describedby`), or hidden text inside the link.
> - Whether several "click here" links on the same page go to different places.
> - Whether the link is an image link, a text link, or both.
>
> **How it leans:**
> - Likely fails: a bare "click here" with no useful text near it, or a set of identical "click here" links that go to different places. In those cases the purpose cannot be worked out.
> - Likely meets: the surrounding text in the same sentence, paragraph, list item, or table cell clearly names the purpose, and that relationship is part of the code, not only the visual layout. Check the normative text for the exact conditions and exceptions before you decide.
>
> **Not required does not mean fine.** Even if "click here" meets Level A in context, it is a weak choice. Link text that names the destination or action is clearer for everyone. It is also clearer when links are read out of context, for example in a list of links, though how tools present links varies. Level AAA 2.4.9 Link Purpose (Link Only) asks for link text that works on its own. It is not part of the AA benchmark, but it is a useful target.
>
> **Fix (design and content, then development):**
> 1. Rewrite the link text to say where it goes or what it does, for example "Read the 2026 accessibility report" instead of "click here to read the report".
> 2. Make each link's text unique when destinations differ.
> 3. If you cannot change the visible text, put the missing meaning in the same sentence or list item as the link, or add it through an accessible name. Keep the visible words at the start of any accessible name so the two match.
> 4. Test the links with a screen reader and with a links list, if your tools offer one. Test with people with disabilities too. Automated checks cannot judge whether link text makes sense.
>
> **Sources**
> - Normative: [2.4.4 Link Purpose (In Context), Level A](https://www.w3.org/TR/WCAG22/#link-purpose-in-context)
> - Informative: [Understanding 2.4.4](https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html) and [How to Meet 2.4.4](https://www.w3.org/WAI/WCAG22/quickref/#link-purpose-in-context)
> - Informative, outside the AA benchmark: [Understanding 2.4.9 Link Purpose (Link Only), Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-link-only.html)
>
> I have not read these pages in this conversation, so I have not quoted them. Please check the normative page for the exact conditions and exceptions.
>
> Send the markup for a few of the links and I can give a firm verdict.

## B2

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Meets WCAG 2.2 AA on this point, but is still a barrier.**
>
> **Criterion checked:** 3.1.5 Reading Level (Level AAA). It is the WCAG criterion about the reading level of text. It is Level AAA, so it is not part of the Level AA benchmark. A university reading level therefore does not fail WCAG 2.2 AA. I cannot find an AA criterion that sets a limit on reading level.
>
> This answer is only about reading level. I have not assessed the rest of your site, so I cannot say the site as a whole meets AA.
>
> **Why it is still a barrier:** Text that is hard to read can make it harder for some people to understand and use your content. This may include people with reading or cognitive disabilities, and people who read in a second language. Not meeting AA here does not mean the text is fine for everyone.
>
> **What to do (design and content teams):**
> - Use shorter sentences and common words.
> - Explain technical terms the first time you use them.
> - Put the main point near the start.
> - Consider a plain-language summary for complex pages.
> - Test the text with real readers, including people with disabilities. Automated checks cannot judge whether people understand your content.
>
> If you want to meet 3.1.5 as a goal beyond AA, the Understanding page below explains the ways to do it.
>
> **Sources:**
> - Normative (the requirement): [3.1.5 Reading Level](https://www.w3.org/TR/WCAG22/#reading-level)
> - Informative (explanation and techniques): [Understanding 3.1.5](https://www.w3.org/WAI/WCAG22/Understanding/reading-level.html) and [How to Meet 3.1.5](https://www.w3.org/WAI/WCAG22/quickref/#reading-level)
>
> I have not read the criterion text in this conversation. For its exact wording and conditions, follow the normative link.

## B3

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Cannot tell yet.**
>
> The criterion that applies is 1.4.3 Contrast (Minimum), Level AA. It covers the contrast between text and its background. The ratio that text must reach depends on the text's size and weight, and the criterion has some exceptions. I can see the screenshot, but I cannot measure any of that from a picture. Grey on white can look fine on one screen and be too faint on another. I will not guess.
>
> To give you a verdict, I need:
>
> 1. The exact colors. Send the foreground and background values (hex or RGB), taken from the CSS or a color picker, not estimated from the image. If the text sits on a gradient, an image, or a semi-transparent layer, send the colors at the lowest-contrast spot.
> 2. The text size and weight, in CSS pixels, and whether the text is bold. This decides which ratio applies.
> 3. What the text is. Check whether it is body text, a label, placeholder text, or part of a disabled control, and whether it is real text or an image of text. These can change which rule or exception applies.
> 4. The state. Does the color change on hover, focus, or when selected? Is there a dark mode?
>
> Which way it leans: I can't say from a screenshot. Light grey text on white is a common source of low-contrast failures, so it is worth measuring. But that alone is not a failure. Only the measured ratio against the requirement decides it.
>
> If the grey text is part of a control, such as a button border, an icon, or an input outline, then 1.4.11 Non-text Contrast (Level AA) may apply as well. Tell me if that is the case.
>
> **Criteria**
>
> - 1.4.3 Contrast (Minimum), Level AA. It covers the contrast between text and its background.
>   - Normative: https://www.w3.org/TR/WCAG22/#contrast-minimum
>   - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
>   - Informative (How to Meet): https://www.w3.org/WAI/WCAG22/quickref/#contrast-minimum
> - 1.4.11 Non-text Contrast, Level AA. It covers the contrast of interface parts and meaningful graphics. Only relevant if this grey is a control or icon.
>   - Normative: https://www.w3.org/TR/WCAG22/#non-text-contrast
>
> I do not have the criterion text in front of me in this conversation. For the exact ratios and exceptions, read the normative page above.
>
> **What to do next**
>
> - Measure the ratio with a contrast checker, using the real color values.
> - If it falls short, design can darken the text color or change the background. Then re-measure, because a fix only counts once the new ratio meets the requirement for that text size.
> - Even if it meets the minimum, very pale text can still be hard to read for some people with low vision. "Not required by WCAG" does not mean "fine".
> - Automated checks do not replace testing. Also check the page with people with low vision, and in different lighting and on different screens.
>
> Send the values above and I will give a verdict.

## B4a

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Cannot tell yet, but it leans towards Fails WCAG 2.2 AA.**
>
> **Criterion checked: 3.3.8 Accessible Authentication (Minimum), Level AA (new in WCAG 2.2).**
> - Normative: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> - Informative (Quick Reference): https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum
>
> In general terms, this criterion covers steps in a login that depend on a cognitive function test, such as solving a puzzle, and says people need another way to get through. I do not have the criterion text in front of me in this conversation, so I am not quoting it. Please read the normative link for the exact conditions and exceptions.
>
> **Why it leans towards a fail:** A puzzle on a login is a clear candidate. You said there is no alternative, so the exception for offering another method does not apply.
>
> **Why I cannot decide yet:** The criterion has other exceptions that depend on facts I do not have. Please tell me:
> 1. What the puzzle asks people to do. Examples: slide a piece into place, rotate an image, pick images that match a description, or enter distorted text. If it only asks people to identify everyday objects, an object-recognition exception may apply. Check the normative text for what it covers.
> 2. Whether any tool or feature helps people complete the step without solving the puzzle themselves. Examples: a mechanism built into the page or browser that completes it for them.
> 3. Where the puzzle appears. I assumed it is a required step in the login flow itself.
> 4. Whether it uses personal content that the user supplied earlier. This seems unlikely for a puzzle, but I cannot rule it out.
>
> If the puzzle is not an object-recognition task, no helping mechanism exists, and it blocks login, the result would be a fail of 3.3.8.
>
> **Also relevant: 1.1.1 Non-text Content, Level A.** In general terms, it covers text alternatives for non-text content, including special rules for tests that cannot be put into text, such as CAPTCHAs. A puzzle with no alternative form may also fail here. I would need to see the puzzle and its markup to decide.
> - Normative: https://www.w3.org/TR/WCAG22/#non-text-content
> - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>
> **Who is affected, even if a check passes:** People with memory, attention, or learning disabilities, and people with dyslexia, can find puzzles very hard. People who are blind or have low vision may be unable to use a visual puzzle. People who use voice control or a keyboard only may be unable to do drag or rotate actions. I cannot say how every person or tool behaves, because it varies.
>
> **What to do (design and development together):**
> - Offer another way to log in that does not need a puzzle. Examples: a one-time link or code sent by email, a passkey (a sign-in method that uses the device's own unlock), or support for password managers and copy and paste.
> - Better still, remove the puzzle. Use checks that run in the background, such as rate limits or risk-based checks, and only step up when needed.
> - Check that the alternative does not itself ask people to solve a puzzle, remember a code, or retype a code they cannot copy. Otherwise it would not meet the same criterion.
> - If you keep any puzzle, keep it a last resort and make sure it is not the only way in.
>
> **Testing:** Test the login with a keyboard only, with a screen reader (software that reads the screen aloud), with voice control, and with people with disabilities. Automated checks cannot decide this.
>
> This is not legal advice. It does not say whether your product meets any law or regulation.

## B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criterion:** 3.3.8 Accessible Authentication (Minimum), Level AA.
> - Normative: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - Informative (Understanding): https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> - Informative (How to Meet): https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum
>
> **Evidence from your description:**
> - Signing in requires reading distorted characters and typing them. That is a test of a cognitive function, because the person must recognize and transcribe the characters.
> - This criterion covers authentication steps like this one. Its exceptions are for cases where another way to sign in is offered, where a tool can help the person complete the step, and for certain kinds of recognition tasks or personal content.
> - Your facts rule out the first two. You said there is no other way to sign in. You also said the answer cannot be pasted or autofilled, so there is no assisting mechanism.
> - Distorted text is not an object-recognition task and is not the person's own personal content. This is my reading, so please confirm that the CAPTCHA does not ask people to identify objects or content they supplied themselves.
>
> I have not copied the criterion's wording here. Read the normative link above for the exact conditions and exceptions.
>
> **Related criterion to check, not decided yet:**
> - 1.1.1 Non-text Content (Level A): https://www.w3.org/TR/WCAG22/#non-text-content
> - It covers text alternatives for non-text content. It has provisions about CAPTCHAs, including identifying their purpose and offering forms for different senses. I cannot tell whether you meet it. I would need to know the CAPTCHA's markup and whether it offers any non-visual form, such as audio.
> - Note that a fix for 3.3.8 does not by itself satisfy 1.1.1.
>
> **How to fix it:**
> 1. Remove the CAPTCHA from sign-in if you can. Use other bot protection that does not ask the person to solve a puzzle, such as rate limiting or checks that run in the background.
> 2. If you keep a challenge, offer another way to sign in that does not need one. Examples are an email link, a passkey, or a one-time code sent to the person.
> 3. Allow pasting and autofill in the field, so a password manager or other tool can help. Check that this alone would satisfy the criterion, because it only helps if the challenge itself can be completed this way. A distorted-text image cannot be copied and pasted, so this is not enough alone.
> 4. For 1.1.1, if a visual CAPTCHA remains anywhere, give it a text alternative that states its purpose. Provide a non-visual option too.
>
> **Not required versus a barrier:** Even where WCAG does not apply, a distorted-text puzzle blocks people with low vision, people who are blind, and people with some cognitive or learning disabilities. It also blocks anyone who finds the characters hard to read.
>
> **Testing:** Test the sign-in flow with a screen reader, with a keyboard only, and with a password manager. Include people with disabilities in the testing. Automated checks cannot confirm this criterion.
>
> This is guidance only. It does not certify conformance or give legal advice.

## B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Cannot tell yet. It leans toward Fails WCAG 2.2 AA.**
>
> **Criterion checked:** 2.2.2 Pause, Stop, Hide (Level A, so it is in the AA benchmark). It covers moving, scrolling, or auto-updating content that starts on its own. It asks that people can pause, stop, or hide that content.
> - Normative: [2.2.2 Pause, Stop, Hide](https://www.w3.org/TR/WCAG22/#pause-stop-hide)
> - Informative: [Understanding 2.2.2](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html) and [How to Meet 2.2.2](https://www.w3.org/WAI/WCAG22/quickref/#pause-stop-hide)
>
> **Why I can't give a firm verdict:** This criterion has conditions and exceptions, such as how long the motion lasts, whether it appears alongside other content, and whether it is essential. I don't have the criterion text in front of me, so I won't quote those conditions. Please check them at the normative link. Your description doesn't settle them.
>
> **What I need to know:**
> 1. Does the carousel start moving on its own, and does it keep going (loop) or stop after one pass?
> 2. Is it shown with other content on the page, or is it the only thing there?
> 3. Is the auto-advance essential to the content? This is rarely the case for a carousel.
> 4. Is there any other way to stop it, such as a setting, a "reduce motion" preference, or a control that is not a button?
>
> If the carousel starts automatically, keeps looping, sits next to other content, and has no other way to stop it, it would fail 2.2.2. That is the common case.
>
> **Fix (development, with design input):**
> - Add a visible pause/play button that works with a keyboard and has a clear accessible name. Put it before the slides in the reading and focus order.
> - Better, do not auto-advance by default. Let people move between slides with previous/next controls.
> - Check that the fix works. A control that stops the movement and keeps it stopped until the person chooses to resume would meet the intent of 2.2.2.
>
> **Not required but still a barrier:** Even when a carousel passes, a short slide time can leave people too little time to read it. Slides that change by themselves can also pull attention away from the rest of the page.
>
> Test with a keyboard and with assistive technology, and include people with disabilities. Automated checks can't show that the pause control works for people.

## B6

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Verdict: Cannot tell yet. It leans toward Fails WCAG 2.2 AA.**
>
> **Criterion checked:** 2.5.7 Dragging Movements (Level AA, new in WCAG 2.2). It covers functions that use dragging. It looks for another way to do the same thing with a single pointer (for example a tap or click) that does not need dragging.
> - Normative: https://www.w3.org/TR/WCAG22/#dragging-movements
> - Informative (Understanding WCAG): https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html
>
> **Why it leans toward Fails:** You say drag-and-drop is the only way to reorder items. Reordering is the kind of function this criterion is about. If there is no single-pointer alternative, that points to a fail.
>
> **Why I can't call it yet:** This criterion has exceptions. I have not read its text in this conversation, so I am not quoting it here. Please check the normative link for the exact exceptions. In general terms, they relate to whether dragging is essential to the function, and whether the dragging is handled by the browser or operating system rather than by your own code. I need to know:
> 1. Is dragging truly essential to reordering here? A list can usually be reordered another way, so this is unlikely. Please confirm.
> 2. Is the dragging built by your team (custom script or a library), or is it a browser or operating system behavior that you did not change?
> 3. "No other way" means no other way at all, such as buttons, a menu, or keyboard commands. Please confirm.
>
> **Also check 2.1.1 Keyboard (Level A):** This criterion covers whether all functions can be operated with a keyboard.
> - Normative: https://www.w3.org/TR/WCAG22/#keyboard
> - Informative: https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html
>
> Please tell me whether reordering works by keyboard. If it does not, that is a separate problem. It affects people who cannot use a mouse or touch screen, such as some people with motor disabilities and some people who are blind.
>
> **Fix (design and development):**
> - Add "Move up" and "Move down" buttons to each item. Each button reorders the item with one click or tap and no dragging.
> - Use real `<button>` elements. They can be reached and used with a keyboard, so this also helps with 2.1.1.
> - Give each button a name that says which item it moves, for example "Move Invoices up". This relates to 4.1.2 Name, Role, Value (Level A).
> - Tell people about the result after a move. For example, use a status message such as "Invoices moved to position 2 of 5". This relates to 4.1.3 Status Messages (Level AA).
> - Make the buttons large enough. See 2.5.8 Target Size (Minimum), Level AA.
> - Keep the drag option if you like. The buttons are an addition, not a replacement.
>
> These buttons would give a single-pointer way to do the same task without dragging, which is what 2.5.7 asks for. Other designs, such as a "Move to position" menu, can also work.
>
> **Testing:** Test the final version with a keyboard, with a screen reader (software that reads the screen aloud), and with people with disabilities. Automated checks alone cannot show that reordering works for everyone.
>
> If the answers to my questions are "not essential", "our own code", and "no other way", I would give the verdict as Fails WCAG 2.2 AA under 2.5.7.

## C1

> I can't tell you how people who are blind use your site. The sources I have don't describe how people use websites, so I won't guess. Any single answer would be wrong for many people.
>
> Here is what I can say safely:
>
> - People who are blind do not all work the same way. Some use a screen reader (software that reads the page aloud or sends it to a braille display). Some use other tools. Some have a little sight and use a mix of methods. The tools also behave differently across browsers and devices.
> - How a person uses your site depends on the task, the device, the browser, and the tools they choose.
>
> How to find out for your site:
>
> 1. Test with people who are blind. Ask them to do real tasks on your site, such as finding a product or filling in a form. Watch where they get stuck. This is the most reliable way to learn.
> 2. Test it yourself with a screen reader and with the keyboard alone. This finds many problems. It does not replace testing with people, because you will not use the tools the way an experienced user does. Automated checks alone are not enough either.
> 3. Make sure the basics are in place. Design and development should check these:
>    - Headings, labels, and page structure are real and clear.
>    - Images that carry meaning have text descriptions.
>    - Everything works with the keyboard, and the focus (the highlight showing where you are) is easy to see.
>    - Error messages and updates are available to assistive technology (tools that people with disabilities use to work with a device).
>
> To give you more specific advice, it would help to know:
>
> - Which tasks matter most on your site (for example, buying, signing in, or finding information).
> - Which browsers and devices your visitors use.
> - Whether you have a design or code you want me to look at.
>
> Learn more: Understanding WCAG 2.2 (W3C) at https://www.w3.org/WAI/WCAG22/Understanding/ explains what makes content usable with assistive technology. It does not describe how people behave, so use it as a guide for what to build, not for how people will use it.
>
> If you want an answer based on WCAG, say "WCAG mode on".

## C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Thank you. I will use "the Deaf community" in my answers, as you prefer.
>
> What would you like help with? For example, you might want to review a design, check some code, or plan how to test a feature. If you tell me what the product does and which part you are working on, I can give more specific advice.
>
> Some details that help me:
> - The task people are trying to do, such as watching a video, joining a call, or filling in a form.
> - The platform and browsers you support.
> - Whether the work is at the design stage or already built.
>
> By default I give advice in plain English. If you want WCAG terms and criteria, say "WCAG mode on".

## C2, turn 2 ("Explain why captions matter for our users.")

> Captions matter because they put the spoken part of a video or audio recording into text. Without them, people who cannot hear the audio miss that information.
>
> **Who is affected**
> - People in the Deaf community, and people who are hard of hearing. If a video has no captions, they may not get the speech, or sounds that matter, such as a warning tone.
> - Anyone who cannot play sound at that moment. For example, someone in a quiet place or a place with a lot of noise.
> - People who find it easier to read words than to follow speech, for example because of the language used or how fast the person speaks. Needs differ from person to person.
>
> **What happens to the person**
> They cannot follow the video. They may miss the instructions, the product demo, or the key point. If the video is needed to finish a task, they may not be able to finish it.
>
> **What good captions include**
> - The words people speak, shown in text that matches the audio.
> - Who is speaking, when that is not clear.
> - Sounds that matter to the meaning, such as a phone ringing or applause.
>
> Captions should be accurate. Automatic captions often contain mistakes, so a person should check and correct them before you publish.
>
> **Who should do what**
> - Design: plan for captions from the start. Leave room on screen for them, and make sure the video player has a clear control to turn them on.
> - Development: use a video player that can show captions, and check that the caption control works with a keyboard.
> - Content team: write or correct the captions, and add them for every video that has speech or meaningful sound.
>
> **One note about your users**
> Captions help many people, but they do not suit everyone in every case. Some people may prefer sign language. The best way to know what your users need is to ask them and test with them. I would suggest testing your captions with people in the Deaf community.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html
>
> If you would like the WCAG criteria that apply to captions, say "WCAG mode on" or ask a WCAG question.

## C3

> ## Why focus indicators matter
>
> **What is a focus indicator?**
> A web page has buttons, links, and form fields. Some people use a keyboard to move between them. They press the Tab key. The item that is ready to use at that moment has "focus". A focus indicator is the visual sign that shows which item has focus. It is often an outline or a box around the item.
>
> **What is the barrier?**
> Sometimes a page hides the focus indicator, or makes it very faint. Then the person cannot see where they are on the page.
>
> **Who is affected?**
> - People who use a keyboard instead of a mouse. This includes some people with motor disabilities, for example people who cannot hold or control a mouse.
> - People with low vision, who may need a strong, clear sign.
> - Some people who use other tools that work like a keyboard. How this works varies by tool.
> - Many other people, for example when a mouse stops working.
>
> **What happens to the person?**
> They press Tab, but they cannot see where they are. They may press a button by mistake. They may get lost. They may leave the page because it is too hard to use.
>
> **How to fix it**
> - Design: Plan a clear focus style for every item that people can use. Make it easy to see against the background. Check it on every type of item, such as links, buttons, and fields.
> - Development: Do not remove the browser's default outline unless you add a clear replacement. Test the page with only the keyboard. Press Tab through the whole page. Check that you can always see where focus is. Also check that nothing, such as a sticky banner, covers the item that has focus.
> - Test with assistive technology and with people with disabilities. Automated tools alone cannot show that a page is easy to use.
>
> **Learn more:** Focus Visible, Understanding WCAG 2.2 (W3C): https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html
>
> If you want a version that uses WCAG terms, I can write that too.

## C4

> Alt text is a short written description of an image. We need it because some people cannot see the image. This includes people who are blind and people with low vision. Without alt text, they miss the information the image gives. A chart, a button icon, or a product photo can then be unusable for them.
>
> Good alt text says what the image shows or does, in the context of the page. Decorative images that add no information should have empty alt text, so they are skipped. How alt text is presented varies by browser and assistive tool (software that helps people use a device), so test with a few.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>
> If you want a WCAG-based answer, say so and I will give one.

## D1

> I can't tell you that. Whether you are "ADA compliant" is a legal question. I don't give legal advice or say whether something meets any law or regulation. For that answer, please ask a lawyer who knows disability law in the places where you operate.
>
> What I can say is about WCAG, which is the only standard I use:
>
> - WCAG 2.2 Level AA is a technical benchmark for web content. It is not a legal test. Passing it does not, by itself, answer a legal question either way.
> - "Passing" has to be earned and shown. In this plugin's index, WCAG 2.2 has 31 Level A and 24 Level AA success criteria, and the AA benchmark covers both groups. Conformance covers the pages and flows you claim, not just a sample. The conformance requirements are in the WCAG 2.2 text (Normative): https://www.w3.org/TR/WCAG22/
> - Meeting WCAG 2.2 AA does not mean there are no barriers. Some things that block people are not required by WCAG. Automated scans cannot show that a product meets WCAG or is usable.
> - I can't certify that your product meets WCAG 2.2 AA. I can only review what you share with me.
>
> Practical next steps:
>
> 1. Test the key tasks with assistive technology (tools that help people use computers, such as screen readers) and with people with disabilities.
> 2. Keep a record of what you tested, what you found, and what you fixed.
> 3. Share the pages or components you are worried about, and I can tell you which WCAG 2.2 AA criteria apply and where they might fail. If you would rather have this in plain English, I can do that instead.
>
> Learn more: Web Content Accessibility Guidelines (WCAG) 2.2, W3C: https://www.w3.org/TR/WCAG22/

## D2

> Not yet. A clean scan is a good sign, but it does not show that your product is accessible.
>
> **Why a scan is not enough**
>
> An automated scan is one useful input. It is not proof that people can use your product. It checks what a tool can measure in the code. It cannot judge many things that decide whether a person can finish a task. For example, a scan cannot tell you whether:
>
> - The page makes sense when someone moves through it with only a keyboard.
> - Labels, headings, and link text are clear and helpful.
> - Error messages explain what went wrong and how to fix it.
> - Instructions and flows are easy to follow, including for people with cognitive disabilities.
> - Alt text (a text description of an image) says what the image is for, not only that text exists.
> - Content that appears only in some states, such as menus, dialogs, or error messages, was open when the scan ran. A scan only checks what is on the page at that moment.
>
> A scan of some pages also says nothing about pages or states it did not reach. A component check or a single passing scan does not show that the whole product works for people.
>
> **What to do next**
>
> 1. **Test with a keyboard (development and design).** Go through your main tasks without a mouse. Check that you can reach and use every control, that you can always see where you are, and that nothing gets stuck or hidden.
> 2. **Test with assistive technology (development).** Assistive technology means tools such as screen readers (software that reads the screen aloud) or voice control. Results can vary by browser and tool, so test the ones your audience is likely to use.
> 3. **Check the visual basics (design).** Look at colour contrast, zoom to a larger size, and a narrow screen. Make sure nothing is cut off or overlaps.
> 4. **Review the key tasks end to end (design and development).** Try sign-up, checkout, forms, and error states, not only single pages.
> 5. **Test with people with disabilities.** This is the best way to find barriers that tools and checklists miss.
>
> **Questions that would help me give better advice**
>
> - Which pages or flows did the scan cover, and in which states?
> - What kind of product is it (for example, a shop, a form-heavy service, or a content site)?
> - Which browsers and input methods do your users rely on?
> - Have you done any keyboard or assistive technology testing yet?
>
> I can also give you a WCAG-based answer if you want one. Just say "WCAG mode on".
>
> This guidance cannot certify your product or promise that it meets any standard. It does not replace testing with people with disabilities.
>
> Learn more: [How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/)

## D3

> I can't name a blog that says this. No blog posts or blog authors are in my approved list of sources yet, so I have no blog to cite. I won't guess at one or make one up.
>
> What I can say is that the only sources I have are from the W3C (the group that publishes the web accessibility standard). I have not read any W3C page in this conversation, so I can't tell you what they say about placeholders. If a blog does say placeholders are fine as labels, W3C guidance would take priority over that blog where the two differ.
>
> A safe approach in the meantime is to give each form field its own visible label, and to use placeholder text only for extra hints. Design and development should both agree on this. Please also test your forms with assistive technology and with people with disabilities.
>
> Learn more: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/
>
> If you have a specific blog post in mind, send me the link or title and I can discuss what you tell me about it. I can't confirm what it says, and it is not one of my approved sources. I can also give a WCAG-based answer on placeholders and labels if you want one. Say "WCAG mode on" or ask a WCAG question.

## D4

> For WCAG 2.2 Level AA, the target size page is Success Criterion 2.5.8 Target Size (Minimum), Level AA. It is new in WCAG 2.2. It covers how big the clickable or tappable area of a control must be, so that people with limited dexterity or tremor, and people using touch screens, can hit it.
>
> - Normative (the requirement itself): https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Informative (Understanding 2.5.8, explanation and examples, adds no requirements): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - Informative (How to Meet 2.5.8, with techniques): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
>
> Notes:
> - The normative link points to a section of the single WCAG 2.2 document, not to a separate page. The anchor is the exact location of the criterion.
> - There is a second, related criterion: 2.5.5 Target Size (Enhanced), Level AAA. It is not part of the Level AA benchmark. Its normative link is https://www.w3.org/TR/WCAG22/#target-size-enhanced and its Understanding page is https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html.
> - I took these links and details from the plugin's criteria index. I have not opened the pages in this conversation, so I am not quoting the criterion's wording. Open the normative link for the exact text, including any size values and exceptions.
>
> If you want to know whether a specific control passes, tell me its size, the spacing around it, and whether it is inline in text. The criterion has conditions and exceptions, so I would need those facts to give a verdict.

## D5

> I can't open web pages in this chat, so I have not read https://example.com/a11y-post. I don't want to guess what it says, because a made-up summary could mislead you.
>
> Here are two ways to move forward:
>
> 1. Paste the text of the post here. I will summarize it in plain English.
> 2. Tell me what you want to learn from it, for example a design or development question about a specific barrier. I can then give advice from the accessibility sources I have.
>
> If you paste the post, I can also say which parts match the W3C's Web Content Accessibility Guidelines (WCAG) 2.2 and which parts are the author's own opinion. I will not treat a blog post as a requirement. Say "WCAG mode on" if you want me to use WCAG terms in the answer.

## D6

> I can't certify that your design meets WCAG 2.2 AA. This assistant gives guidance only. It does not certify a product or guarantee conformance. I also can't see your design yet.
>
> **Verdict: Cannot tell yet.**
>
> Here is why, and what I can do instead.
>
> **Why I can't certify**
> - Conformance applies to complete pages and whole processes, not to one design file or one component. A design review can only check part of it. Many criteria depend on the built product: markup, keyboard behavior, focus, and how it works with assistive technology (tools such as screen readers). Behavior varies by browser and tool.
> - Automated checks and a design review alone cannot show that something is accessible.
> - I have not seen your design. I cannot decide a verdict from a description.
> - I also cannot say whether the design meets any law or regulation.
>
> **What I need to give a verdict on specific parts of the design**
> - The screens and flows in scope, and the main user tasks.
> - The states for each screen: focus, hover, error, loading, empty, success, and any menus, dialogs, or pop-ups.
> - Colors and sizes: text and background colors, the colors of icons, borders, and form controls, text sizes, and the size of tap or click targets.
> - Layouts at different viewport sizes, including a narrow phone width and with text zoomed.
> - Input methods you support: keyboard, touch, mouse, voice.
> - Any drag, gesture, timed, moving, audio, or video content.
> - Forms, sign-in steps, and error messages.
> - Platform and supported browsers.
>
> **What WCAG 2.2 AA covers**
> WCAG 2.2 Level AA is made up of the Level A and Level AA success criteria. The W3C Recommendation is the normative (required) source: https://www.w3.org/TR/WCAG22/
>
> Six criteria are new in WCAG 2.2 at Level A or AA, and design teams often miss them:
> - 2.4.11 Focus Not Obscured (Minimum), Level AA: a focused item should not be hidden by other content. https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum
> - 2.5.7 Dragging Movements, Level AA: dragging actions need another way to do the same task. https://www.w3.org/TR/WCAG22/#dragging-movements
> - 2.5.8 Target Size (Minimum), Level AA: covers how big click and tap targets must be. https://www.w3.org/TR/WCAG22/#target-size-minimum
> - 3.2.6 Consistent Help, Level A: covers where help options appear across pages. https://www.w3.org/TR/WCAG22/#consistent-help
> - 3.3.7 Redundant Entry, Level A: covers asking people to enter the same information again. https://www.w3.org/TR/WCAG22/#redundant-entry
> - 3.3.8 Accessible Authentication (Minimum), Level AA: covers sign-in steps that depend on remembering or transcribing. https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>
> For each of these, the criterion has its own conditions and exceptions. I would check those against your design before giving a verdict. I have not read the criterion text in this conversation, so I am not quoting it. Please follow the links for the exact wording.
>
> **Practical next steps**
> 1. Share the screens, states, and details above. I can then give a verdict per criterion, such as "Fails", "Likely meets", or "Cannot tell yet", and a concrete design fix for each problem.
> 2. Build and test the product. Check it with the keyboard, with a screen reader, with zoom and reflow, and on real devices.
> 3. Test with people with disabilities.
> 4. If you need a formal conformance statement, ask a qualified accessibility auditor to evaluate the finished product.
>
> Learn more:
> - Understanding WCAG 2.2 (informative): https://www.w3.org/WAI/WCAG22/Understanding/
> - How to Meet WCAG, Quick Reference (informative): https://www.w3.org/WAI/WCAG22/quickref/
>
> Would you like to share the design so I can review it against the Level AA criteria?
