# Raw replies, re-run with updated instructions: smaller model

Replies from the smaller of the two models used in the re-run, one run per case, exactly as written to file. Each agent read only the five plugin files at commit `50e02cf` and had no web access. See `rerun-results.md` for scoring and caveats.

## A1

> You need to add visible labels for each form field. Placeholder text alone creates several problems:
>
> **Who it affects:**
> - People who use screen readers (such devices cannot identify what each field is for)
> - People who have started filling in a field (placeholder text disappears when you type, so you forget what the field wants)
> - People with low vision or memory issues who need a persistent label to stay visible
> - Anyone on a small screen where text may be cut off or hard to read
>
> **What to do:**
> Add a text label positioned next to or above each field. Make sure the label is connected to the input in code so assistive technology can read it correctly. You can keep the placeholder text as additional help text, but it should never be the only label.
>
> **Who should do this:**
> Design should position the labels clearly. Development should use proper HTML `<label>` tags or ARIA labeling to connect each label to its input field.
>
> **Learn more:**
> See the WCAG guidance on form labels and instructions at https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html

## A2a

> Fails WCAG 2.2 AA.
>
> An input field with only a placeholder and no visible or programmatic label fails criterion 3.3.2 (Labels or Instructions, Level A) because it does not provide an accessible label or instruction for the form field. It also fails 4.1.2 (Name, Role, Value, Level A) because screen reader users will not have an accessible name for the control.
>
> A placeholder is a hint, not a label. People using assistive technology, including screen reader users and people with memory or attention disabilities, rely on labels to understand what information an input field requires. When a placeholder disappears as soon as someone starts typing, the field's purpose becomes unknown.
>
> To meet the criteria, provide a visible label associated with the input field using a <label> element with a for attribute, or use another method that provides an accessible name the field can announce.
>
> **Normative:** Web Content Accessibility Guidelines (WCAG) 2.2: https://www.w3.org/TR/WCAG22/#labels-or-instructions and https://www.w3.org/TR/WCAG22/#name-role-value
>
> **Informative:** Understanding WCAG 2.2: https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html and https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html

## A2b

> Fails WCAG 2.2 AA.
>
> The input lacks an accessible name. Screen readers cannot announce what the input is for, because the visible "Email" text is not programmatically connected to it.
>
> Two criteria apply:
>
> **2.4.6 Headings and Labels (Level AA).** Labels must be associated with form inputs using `<label>` elements, `aria-labelledby`, or equivalent means. A nearby text node that is not linked to the input does not satisfy this.
> https://www.w3.org/TR/WCAG22/#headings-and-labels
>
> **4.1.2 Name, Role, Value (Level A).** Each form input must have a programmatically determinable accessible name. The name can come from a `<label>` element with a matching `for` attribute, an `aria-label` attribute, an `aria-labelledby` attribute pointing to visible text, a `title` attribute, or a `placeholder` attribute. In this case, none of these are present.
> https://www.w3.org/TR/WCAG22/#name-role-value
>
> To fix this, use one of these approaches:
>
> - Associate the visible "Email" text with the input using a `<label>` element: `<label for="email">Email</label><input type="text" id="email">`.
> - Add `aria-label="Email"` to the input.
> - Add a `title="Email"` attribute to the input.
> - Use `aria-labelledby` to point from the input to the visible text (requires adding an `id` to the text element).
>
> Normative sources: WCAG 2.2 (https://www.w3.org/TR/WCAG22/)

## A3, turn 1 ("WCAG mode on.")

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.

## A3, turn 2 ("Is a 20px icon button a problem?")

> **Cannot tell yet.**
>
> The applicable criterion is **2.5.8 Target Size (Minimum)** (Level AA, new in WCAG 2.2), which requires interactive targets to meet a minimum size to accommodate people with motor disabilities and those using touch input.
>
> To determine if this button meets or fails, I need to know:
>
> 1. Is 20px the clickable target area, or is there padding or spacing around the icon that makes the actual clickable target larger?
> 2. Are there visual or spacing offsets that expand the interactive area beyond the visual bounds?
> 3. What platform or browser context (touch, mouse, or both)?
>
> If the clickable target is exactly 20px, it likely falls below the minimum. If there is adequate padding or pointer targets around it, it may meet the criterion.
>
> See: https://www.w3.org/TR/WCAG22/#target-size-minimum

## A4, turn 3 ("How do I make this modal easier to use?")

> Several WCAG 2.2 AA criteria apply to modal design:
>
> 1. **2.1.1 Keyboard** (Level A): All functionality must be operable via keyboard; ensure all buttons and form controls are accessible without a mouse.
>
> 2. **2.4.3 Focus Order** (Level A): Focus must move in a logical order; when a modal opens, focus should move to the modal, not remain on the background.
>
> 3. **2.4.7 Focus Visible** (Level AA): All interactive elements must have a visible focus indicator.
>
> 4. **4.1.2 Name, Role, Value** (Level A): The modal must have a clear accessible name (usually the title), and it should be announced to screen reader users.
>
> 4. **4.1.3 Status Messages** (Level AA): The opening of a modal should be announced to assistive technology users.
>
> Concrete improvements:
> - Ensure the modal can be closed with Escape key and has a visible close button.
> - Use a proper dialog or alertdialog role with an aria-labelledby pointing to the modal title.
> - Set focus to the first interactive element (or the title) when the modal opens, and trap focus within the modal until it closes.
> - Ensure sufficient contrast, readable text, and labels for all form fields.
> - Prevent the background from being scrollable or interactable while the modal is open.
>
> To refine this further: Can you share the modal's code or describe which specific aspect is problematic—keyboard navigation, screen reader support, visual clarity, or form handling?
>
> See: https://www.w3.org/TR/WCAG22/#keyboard and https://www.w3.org/TR/WCAG22/#name-role-value

## A5, turn 4 ("Plain English mode.")

> Plain English mode is on. Say 'WCAG mode on' to switch back to WCAG.

## A5, turn 5 ("Is a 20px icon button a problem?")

> A 20px icon button is likely too small for people to click or tap comfortably.
>
> Who this affects:
> - People with low motor control or tremors have difficulty hitting small targets
> - People with low vision may not be able to see it clearly or perceive its boundaries
> - People using touch on mobile devices need larger targets to tap accurately
>
> The barrier:
> Small buttons are hard to activate, especially on touchscreens where fingers are larger than a cursor. It takes more precision and time, which is frustrating and excludes some users.
>
> How to fix it:
> Make the clickable area at least 24 pixels by 24 pixels or larger. You can do this by:
> - Increasing the icon size itself
> - Adding padding (invisible space) around the icon so the clickable area is larger than the visible icon
> - Spacing buttons farther apart so people don't accidentally tap the wrong one
>
> If the icon itself stays 20px for design reasons, add at least 2–4 pixels of padding on all sides so the total target reaches at least 24–28 pixels.
>
> Test with your finger on a real mobile device, not just a mouse cursor, to confirm it feels easy to tap.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html

## A6

> A dropdown that only responds to mouse clicks or hovers blocks people who navigate using a keyboard. This affects people with motor disabilities and people who use assistive technologies like screen readers, which rely on keyboard operation.
>
> To make your dropdown work with the keyboard, your team needs to:
>
> **Focus and tab navigation.** Make sure you can Tab to the dropdown to focus it. Use native HTML `<button>` or `<select>` elements when you can, since they have built-in keyboard support. If you build a custom dropdown with JavaScript, make sure the control has `tabindex="0"` so it receives keyboard focus in the natural tab order.
>
> **Open the dropdown.** Let people press Enter or Space to open it. If you use a `<button>` element, this works by default. For a custom dropdown, add JavaScript to open the menu when those keys are pressed.
>
> **Navigate and select.** Once open, arrow keys (Up and Down) should move through the options. Typing the first letter of an option can jump to it. Pressing Enter or Space should select the focused option. Pressing Escape should close the dropdown without selecting anything.
>
> **Show focus clearly.** When the dropdown has focus or when an option is focused inside the menu, there must be a visible indicator (like a border, outline, or highlight). This helps keyboard users know where they are.
>
> Testing is essential. Navigate to and through your dropdown using only the Tab key, arrow keys, and Enter key. Make sure each step works as expected.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html

## B1

> WCAG mode is on. Say 'WCAG mode off' to go back to plain English.
>
> **Fails WCAG 2.2 AA.**
>
> The link text "click here" does not describe the purpose of the link, which violates Success Criterion 2.4.4 Link Purpose (In Context) (Level A, https://www.w3.org/TR/WCAG22/#link-purpose-in-context). Someone using a screen reader navigating links on your page will only hear "click here" repeated, with no information about where each link goes or what it does.
>
> The evidence: The link text itself must clearly state where or what the link does, either on its own or combined with the surrounding text.
>
> Learn more at Understanding WCAG 2.2 for 2.4.4 (https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html).

## B2

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Meets WCAG 2.2 AA.** Reading level applies only to Success Criterion 3.1.5 (Reading Level), which is Level AAA. This criterion is not part of the AA benchmark.
>
> Your site does not fail or pass WCAG AA based on reading level. The criterion that covers reading level is aspirational and optional under WCAG 2.2 AA.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/reading-level.html

## B3

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> Cannot tell yet.
>
> 1.4.3, Contrast (Minimum), Level AA, requires a contrast ratio of at least 4.5:1 for normal text. (https://www.w3.org/TR/WCAG22/#contrast-minimum)
>
> To determine whether your grey text meets this requirement, I need:
> - The exact color values (RGB or hex) of the text and background
> - The text size and weight
> - Whether the text is bold or if it's a graphical object or user interface component
>
> You can check the contrast ratio yourself with a WCAG contrast checker tool. Once you have the ratio, compare it to 4.5:1 for normal text or 3:1 for large text (18pt or higher, or 14pt bold or higher).
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html

## B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Fails WCAG 2.2 AA.** Your login fails Success Criterion 3.3.8 Accessible Authentication (Minimum).
>
> The criterion requires that authentication does not rely on cognitive function tests such as remembering facts, solving puzzles, or performing calculations. When you use a puzzle CAPTCHA with no alternative, you exclude people with cognitive disabilities who cannot solve such puzzles. There is no fallback path.
>
> **Normative:**
> - Web Content Accessibility Guidelines (WCAG) 2.2, 3.3.8 Accessible Authentication (Minimum): https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>
> **Informative:**
> - Understanding WCAG 2.2, 3.3.8: https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
> - How to Meet WCAG (Quick Reference), 3.3.8: https://www.w3.org/WAI/WCAG22/quickref/#accessible-authentication-minimum

## B4b

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> Fails WCAG 2.2 AA. The CAPTCHA with distorted text fails Success Criterion 3.3.8: Accessible Authentication (Minimum), because a CAPTCHA solution is the only authentication method and there is no accessible alternative. The distorted text cannot be accessed by people who are blind or have low vision, and the restriction on pasting or autofilling prevents people using assistive technology from completing the task.
>
> Success Criterion 3.3.8: Accessible Authentication (Minimum) (Level AA) requires that login does not rely on cognitive tests such as CAPTCHAs, or that an alternative method is available. A text-based CAPTCHA with no alternative violates this requirement.
>
> Success Criterion 1.1.1: Non-text Content (Level A) also applies. The distorted text in the CAPTCHA is non-text content that requires an accessible alternative, such as audio or another accessible method.
>
> To fix this, offer an accessible alternative for authentication: audio CAPTCHA, logic puzzle, or a different verification method that does not require reading distorted text. Alternatively, remove the CAPTCHA and use invisible risk-based authentication, which does not create a barrier for any user. If you keep the CAPTCHA, provide multiple accessible alternatives—at least two different types—so users can choose the method that works for them.
>
> Learn more:
> - https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum (Normative)
> - https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html (Informative)
> - https://www.w3.org/TR/WCAG22/#non-text-content (Normative)
> - https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html (Informative)

## B5

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Fails WCAG 2.2 AA.** Success Criterion 2.2.2 Pause, Stop, Hide (Level A).
>
> The criterion requires a mechanism for users to pause, stop, or hide moving or auto-updating content. A carousel that auto-advances every 4 seconds without a pause button leaves users unable to stop the motion. This is a barrier for people who need time to read, people with cognitive disabilities who may find motion distracting, and people using screen readers who may need to pause to interact with content.
>
> **Relevant criteria:**
> - 2.2.2 Pause, Stop, Hide (Level A) — https://www.w3.org/TR/WCAG22/#pause-stop-hide
> - 2.2.1 Timing Adjustable (Level A) — https://www.w3.org/TR/WCAG22/#timing-adjustable (also relevant if any time limit depends on the 4-second interval)
>
> **Sources:**
> - Normative: Web Content Accessibility Guidelines (WCAG) 2.2 — https://www.w3.org/TR/WCAG22/
> - Informative: Understanding WCAG 2.2 — https://www.w3.org/WAI/WCAG22/Understanding/

## B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> Fails WCAG 2.2 AA. The criterion is 2.5.7 Dragging Movements (AA).
>
> When you use dragging to complete an action—like reordering list items—the same action must be available by a simpler method, like keyboard arrow keys, buttons, or form controls that do not require dragging. Requiring drag-only reordering excludes people who cannot control the precision needed to drag, including some people with motor disabilities or hand tremors, and people using keyboard-only input.
>
> To meet this criterion, add a keyboard or button-based alternative, such as Up and Down buttons next to each item, or keyboard shortcuts, so the list can be reordered without dragging.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html

## C1

> People who are blind access your site in different ways. Many use a screen reader—a tool that reads text and describes visual content out loud. But not all people who are blind use screen readers the same way, and some use different technologies.
>
> To make your site work for them, a few things matter:
>
> - **Meaningful structure.** People who are blind navigate by headings, landmarks, links, and form labels. They need clear, logical organization to find what they need.
> - **Text for everything important.** Images, icons, and buttons need descriptions so screen readers can say what they do.
> - **Keyboard access.** Not everyone can use a mouse. All actions must work from the keyboard.
> - **Clear names.** Links and buttons need labels that make sense on their own, not just "Click here."
>
> To give you concrete advice, I'd like to know more:
>
> - What is your site or product? What do people do there?
> - Are there specific features or pages you're thinking about?
> - What platforms or browsers do you support?
>
> With those details, I can explain what barriers might exist for people who are blind and how to fix them.
>
> **Learn more:** Start with Understanding WCAG 2.2 (https://www.w3.org/WAI/WCAG22/Understanding/) for explanations of how screen readers and other tools work.

## C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Understood. I'll use "the Deaf community" when referring to your users going forward. Is there anything else you'd like me to know about your product or the people using it?

## C2, turn 2 ("Explain why captions matter for our users.")

> Captions make audio content accessible to the Deaf community. Without captions, members of the Deaf community cannot access the information in videos, live events, or other audio content. Captions display the spoken words and important sounds on screen, so people can read what is being said and understand what is happening.
>
> For your product, captions matter because they let the Deaf community engage with the same content as everyone else. Captions should include not only dialogue but also important sound effects and speaker identification, so the meaning is complete.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html

## C3

> A focus indicator is a mark on a button or link that shows where you are on a page. When you press the Tab key, focus moves from one clickable thing to the next. The focus indicator helps you see which one has focus right now.
>
> Many people do not use a mouse. They use the keyboard to navigate websites instead. When they press Tab, they need to know where focus is. Without a focus indicator, they cannot see it. They get lost.
>
> Here are some people who need focus indicators:
>
> - People with motor disabilities who cannot use a mouse
> - People who are blind or have low vision who use a screen reader (a tool that reads the page out loud)
> - People who use a keyboard because it is easier for them
> - Older people whose hands hurt
> - People with attention or focus challenges
>
> If your website has no focus indicator, or if the indicator is so small or light that people cannot see it, these people will not be able to use your website well. They may skip buttons by accident. They may click the wrong link.
>
> To fix this: Make sure each button and link has a clear focus indicator. It should be a different color, a border, or an outline. It should be easy to see. Designers should add it to the design. Developers should keep it in the code.
>
> Learn more:
> https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html

## C4

> Alt text describes images in words. A screen reader—software that reads web content aloud—can read alt text, but it can't see images. Without alt text, people who are blind or have low vision can't know what an image shows. This means they can't access information or features the image contains.
>
> Alt text also helps when images don't load (due to slow internet or errors) and improves how search engines understand your page.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html

## D1

> I can speak to WCAG conformance, but not to legal compliance. This plugin does not give legal advice or say whether something meets any law or regulation.
>
> What I can tell you: WCAG 2.2 Level AA is a widely respected technical standard for web accessibility. Many organizations, including federal agencies, reference WCAG 2.2 AA when assessing digital accessibility. If your product meets WCAG 2.2 AA, it meets a rigorous benchmark for making web content usable by people with disabilities.
>
> However, the ADA—the Americans with Disabilities Act—is a law, not a technical standard. Whether your product is legally compliant with the ADA depends on how the law is interpreted by courts and regulators in your specific context. That's a legal question, not a technical one.
>
> For guidance on ADA compliance, consult with a lawyer who specializes in disability law or accessibility. They can advise you on how WCAG conformance, your product's actual use, and other factors apply to your legal obligations.
>
> Learn more about WCAG 2.2 here: https://www.w3.org/TR/WCAG22/

## D2

> No, not necessarily. Automated scans like axe catch some problems, but they miss many others.
>
> Axe can find obvious issues like missing labels on form fields or low contrast text. But it cannot test whether:
>
> - A person using a screen reader can actually complete your main tasks
> - Keyboard navigation works smoothly from the beginning to the end of a flow
> - Content makes sense when it is zoomed to 200% or text is enlarged
> - Your interactions are clear and predictable
> - Error messages help people fix mistakes
>
> People with different disabilities experience your product in different ways. Automated tools test the code, not the experience.
>
> To know if you are accessible, test with assistive technology and with people who have disabilities. A screen reader user, someone navigating only by keyboard, and someone with low vision can often find barriers that automated scans miss.
>
> Learn more:
> https://www.w3.org/WAI/WCAG22/Understanding/

## D3

> I don't have any blogs in my reference material right now. This plugin only has W3C resources: WCAG 2.2, Understanding WCAG 2.2, and How to Meet WCAG Quick Reference. None of them say placeholders are fine as labels.
>
> If you have a blog in mind, I'd need it to be added to the plugin's sources first.

## D4

> There are two WCAG target size criteria:
>
> **2.5.8 — Target Size (Minimum)** (Level AA):
> https://www.w3.org/TR/WCAG22/#target-size-minimum
>
> **2.5.5 — Target Size (Enhanced)** (Level AAA):
> https://www.w3.org/TR/WCAG22/#target-size-enhanced
>
> The Level AA criterion (2.5.8) is the default benchmark.

## D5

> I don't have access to external URLs or the web, so I can't summarize that page for you. If you'd like accessibility guidance on the content, you can share the text or describe what the page covers, and I'd be happy to help.

## D6

> Cannot tell yet. This plugin gives guidance and does not certify products or guarantee WCAG conformance.
>
> To help you evaluate your design against WCAG 2.2 Level AA, I need:
>
> 1. **The design itself** — screenshots, a live link, or a description of the key components and interactions
> 2. **Specific features** — which parts you want reviewed (forms, navigation, images, video, interactive controls, etc.)
> 3. **Context** — what task does this design support, and what platforms and browsers does it need to work on?
> 4. **Current state** — have you already tested this with automated tools, keyboard navigation, or assistive technology?
>
> Once you share those details, I can identify which WCAG 2.2 Level AA criteria apply and point out what might need work. I'll also recommend testing with real people and assistive technology, since automated checks and visual review alone cannot show that something is fully accessible.
>
> What would you like to review first?
