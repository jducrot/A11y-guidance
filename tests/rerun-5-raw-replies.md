# Raw replies, re-run 5

Replies exactly as each agent wrote them to file, one run per case. Each agent read only the six plugin files at commit `09aa4fa` and had no web access. C2 was run as two turns in one conversation. See `rerun-5-results.md` for scoring and caveats.


## Smaller model

### A2a

> WCAG mode, for this question.
>
> **Verdict: Cannot tell yet.** It leans toward Fails if the field has no other accessible name and no other instructions.
>
> **Criteria that could apply** (all are in scope for the WCAG 2.2 AA benchmark)
>
> - 3.3.2 Labels or Instructions, Level A. https://www.w3.org/TR/WCAG22/#labels-or-instructions. Covers whether labels or instructions are given when the page asks for input.
> - 4.1.2 Name, Role, Value, Level A. https://www.w3.org/TR/WCAG22/#name-role-value. Covers whether software, such as a screen reader, can read the name of each control.
> - 1.4.3 Contrast (Minimum), Level AA. https://www.w3.org/TR/WCAG22/#contrast-minimum. Covers the color contrast of text. This applies to placeholder text if it counts as text on the page.
> - 1.3.5 Identify Input Purpose, Level AA. https://www.w3.org/TR/WCAG22/#identify-input-purpose. Applies only if the field asks for a common personal detail, such as a name or email address. I did not check the list of purposes it refers to, because that list is not in the files I read.
>
> **Known**
> - The field has no visible label. Placeholder text is the only text shown for it.
> - The field asks the user for information.
> - This is a web page. (Implied by the question.)
>
> **Still needed**
> - The markup. Does the field have a label element, aria-labelledby, aria-label, or title? Only the markup shows its accessible name.
> - Whether other text on the page explains the field, such as nearby instructions.
> - Whether the placeholder text meets a 4.5:1 contrast ratio, and whether the page relies on it as text.
> - What the field asks for, which decides whether 1.3.5 applies.
>
> **Why the placeholder is the open question for 3.3.2 and 4.1.2**
>
> 3.3.2 says: "Labels or instructions are provided when content requires user input." The criteria text defines a label as "text or other component with a text alternative that is presented to a user to identify a component within web content." It also notes that "A label is presented to all users whereas the name may be hidden and only exposed by assistive technology."
>
> A placeholder is shown to users, but it often disappears once the person starts typing. The criteria text does not say whether a placeholder counts as a label or as instructions. Settle that with the markup and the page before giving a final verdict.
>
> 4.1.2 says: "the name and role can be programmatically determined." A placeholder alone may or may not give the field a name in software. That depends on the markup, which I cannot see.
>
> **Suggested fix**
>
> Add a visible label above the field and connect it to the input in the code. A visible, lasting label meets 3.3.2 for this field, and it gives the field a name for 4.1.2. The placeholder can stay as an example, as long as the label stays visible.
>
> **Testing**
>
> Test the form with a screen reader and with the keyboard, and with people with disabilities. Automated checks can flag a missing name, but they cannot show that the field is usable.
>
> **Sources**
> - Normative: the WCAG 2.2 criteria text quoted above, from the W3C.
> - Informative: the Understanding pages linked from the criteria index. I did not open them in this conversation, so I have not quoted them.
>
> If you share the markup for the field, I can give a verdict.
>
> **In plain English**
>
> Some people who are blind use a screen reader, which reads the page aloud. With no label in the code, the reader may say only "edit text," so the person cannot tell what to type. People with low vision may not see light gray placeholder text. People with cognitive disabilities may lose the hint once they start typing, because the placeholder often disappears. A visible label above the field helps all of these people. Design should add the label, and development should connect it to the field.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Cannot tell yet.** It leans toward Fails.
>
> **Criteria that could apply**
>
> 1. **3.3.8 Accessible Authentication (Minimum), Level AA.** New in WCAG 2.2.
>    - Normative: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>    - Understanding: https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
>    - The criterion says: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:" followed by four options: Alternative, Mechanism, Object Recognition, and Personal Content.
>    - Covers login steps that ask the person to do a cognitive task, such as solving a puzzle.
>
> 2. **1.1.1 Non-text Content, Level A.** The CAPTCHA item in the list of exceptions applies here.
>    - Normative: https://www.w3.org/TR/WCAG22/#non-text-content
>    - Understanding: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>    - The CAPTCHA item says: "If the purpose of non-text content is to confirm that content is being accessed by a person rather than a computer, then text alternatives that identify and describe the purpose of the non-text content are provided, and alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
>
> Not part of this answer: 3.3.9 Accessible Authentication (Enhanced) is Level AAA, so it is outside the AA benchmark.
>
> **Known**
>
> - The login asks users to solve a puzzle CAPTCHA. (You stated this.)
> - The puzzle is a cognitive function test. The criterion's definition lists "solving of puzzles".
> - No alternative to the puzzle is offered. (You stated this.) So the "Alternative" option in 3.3.8 is not met.
> - No alternative forms of the CAPTCHA for other senses are offered. (Implied by "no alternative".)
> - Solving the puzzle is required to log in. (Implied by "asks users to solve". Correct me if the puzzle is optional.)
>
> **Still needed**
>
> - What kind of puzzle it is. If it asks users to recognize objects, such as picking all the bicycles, the "Object Recognition" option in 3.3.8 may apply. A slider or jigsaw puzzle does not qualify.
> - Whether the step has a mechanism that helps the user complete the puzzle. This is a way to assist with the puzzle itself, not just a way to sign in another way.
> - Whether the puzzle uses content the user gave the website (the "Personal Content" option).
> - For 1.1.1: whether the CAPTCHA has a text alternative that identifies and describes its purpose. The second part of the CAPTCHA item is known to be missing, so the CAPTCHA exception does not cover this puzzle as written.
>
> **Why it leans toward Fails**
>
> If the puzzle is not object recognition, has no assisting mechanism, and no other sign-in method is offered, 3.3.8 is not met. The login step would then be a barrier for people with cognitive disabilities, for example people who have trouble with memory, reasoning, or attention, and for some people who use assistive technology that cannot solve visual puzzles.
>
> **Concrete fix**
>
> - Add another sign-in method that does not depend on a cognitive function test. Check each option against the definition before you rely on it. Typing a code from an email or text message counts as "transcription" in the definition, so it may not be an alternative on its own. Options such as a passkey, or a sign-in method that lets the browser or a password manager fill in the details, are worth testing against the criterion.
> - Use a method that does not ask people to solve puzzles or remember and type details.
> - Make the CAPTCHA step easy to get past for people who cannot solve it, and add a way for them to sign in another way. This change is for the login flow, so development should make it, with design deciding the sign-in options.
>
> **Testing**
>
> Test the login flow with assistive technology such as a screen reader, and with people who have cognitive, visual, and motor disabilities. Automated checks cannot show that this step is accessible.
>
> **Source labels**
>
> - Normative: the success criteria text for 3.3.8 and 1.1.1, from the W3C WCAG 2.2 Recommendation.
> - Informative: the Understanding pages linked above.
>
> This is guidance, not a certification or a conformance guarantee. It is not legal advice.
>
> If you tell me the kind of puzzle, whether a password manager or passkey is available, and whether there is any other sign-in method, I can give a verdict.

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.** The drag-and-drop list fails success criterion 2.5.7 Dragging Movements (Level AA). It also likely fails 2.1.1 Keyboard (Level A), for the same reason.
>
> **Criteria that apply**
>
> - **2.5.7 Dragging Movements**, Level AA. Normative: https://www.w3.org/TR/WCAG22/#dragging-movements
> - **2.1.1 Keyboard**, Level A. Normative: https://www.w3.org/TR/WCAG22/#keyboard
>
> **Criterion wording (2.5.7, from the W3C text)**
>
> "All functionality that uses a dragging movement for operation can be achieved by a single pointer without dragging, unless dragging is essential or the functionality is determined by the user agent and not modified by the author."
>
> **Known**
>
> - Reordering the list works only by dragging.
> - There is no other way to reorder items.
> - Your team builds the list, so the browser does not set the behavior. (Implied by "our list." Tell me if that is wrong.)
> - I read "no other way" to include the keyboard, so keyboard users cannot reorder either. (Implied. Tell me if a keyboard method exists.)
>
> **Still needed**
>
> - Nothing for the verdict.
>
> **Exceptions checked**
>
> - Essential: does not apply. Reordering can be done another way, such as move buttons, so dragging is not essential.
> - User agent control: does not apply. Your team controls the behavior.
>
> **Who is affected**
>
> - People with limited hand control, tremor, or limited dexterity may find dragging hard or impossible.
> - People who use a keyboard or a screen reader cannot reorder items at all, because no other method exists.
>
> **Concrete fix**
>
> 1. Add a "Move up" and a "Move down" button to each item. Design should place them where people can see them. Development should use real button elements.
> 2. Give each button a name that says which item it moves, for example "Move Invoice 3 up". Screen reader users need this.
> 3. After each move, announce the new position, for example "Moved to position 3 of 8". Use a status message so it is announced without moving focus. Keep focus on the moved item's button.
> 4. Keep drag and drop as an extra. Do not let it be the only way.
> 5. Check that the buttons are at least 24 by 24 CSS pixels (Target Size (Minimum), 2.5.8, Level AA), or meet one of its exceptions.
>
> This fix satisfies 2.5.7, because one click reorders an item without dragging. It also helps with 2.1.1, when the buttons are native buttons that work with the keyboard.
>
> **Sources**
>
> - Normative: the WCAG 2.2 text for 2.5.7 and 2.1.1 (links above).
> - Informative: Understanding 2.5.7: https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html
> - Informative: How to Meet WCAG, 2.5.7 entry: https://www.w3.org/WAI/WCAG22/quickref/#dragging-movements
> - Informative: Understanding 2.1.1: https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html
>
> I have not opened these pages in this conversation. The links come from the plugin's criteria index.
>
> **Testing**
>
> - Try the reorder with a mouse click only, with the keyboard only, and with a screen reader.
> - Ask people with motor disabilities, and people who use a keyboard or a screen reader, to test the new buttons. Automated checks will not catch this problem.
>
> This is a guidance verdict based on the facts you gave. It is not a certification or a formal conformance audit.

### C1

> Many people who are blind use a screen reader. A screen reader is software that reads the page aloud, or sends the text to a braille display (a device that shows text as raised dots). Not everyone who is blind uses one, and how they use a site depends on their browser, their screen reader, and their settings.
>
> Here is how a site can work for people who use a screen reader:
>
> - **Moving with the keyboard.** Many of these people move through the page with the keyboard instead of a mouse. They use keys to jump from link to link, button to button, and field to field. Every control must work with the keyboard alone.
> - **Jumping by headings.** Many screen reader users move from heading to heading to scan a page. Headings need to be real heading tags, in a sensible order, and they need to describe the section below them.
> - **Hearing what each control does.** The screen reader reads the name of each button, link, and form field. If a button has no name, it may be read only as "button", so the person cannot tell what it does. Icon-only buttons are a common problem.
> - **Hearing images.** Images that carry meaning need a short text description. Decorative images should be hidden from the screen reader, so they do not add noise.
> - **Hearing changes.** When something changes on the page, such as an error message, a "saved" message, or a count of search results, the screen reader may not read it out unless the page is built to announce it. Otherwise the person may never know it happened.
> - **Filling in forms.** Each field needs a label that is tied to that field. Errors should be written in words, near the field, with a clear way to fix them.
> - **Understanding links and titles.** A clear page title helps the person know where they are when they open a page. Link text should make sense on its own, for example "Download the 2026 price list", not "Click here".
>
> What to do:
>
> For design:
> - Use clear headings and plain labels.
> - Write button and link text that says what will happen.
> - Show error messages in words, next to the field, and say how to fix the problem.
> - Do not rely on color, position, or the shape of an icon alone to explain something.
>
> For development:
> - Use real links for going to another page and real buttons for actions. Custom controls built from plain containers often lose their name and their keyboard behavior, so they need extra work to match.
> - Give every form field a label. Give every meaningful image a text alternative, and hide decorative images from assistive technology.
> - Make every feature work with the keyboard, and keep the keyboard focus visible and not hidden behind other content.
> - Announce status messages and errors, so the screen reader can read them without the person having to move to them.
>
> How to test:
> - Turn on a screen reader and try to finish one key task using only the keyboard. Notice what the screen reader says at each step.
> - Test with people who are blind or who use screen readers every day. Automated checking tools catch some problems, but they cannot show whether the site is usable.
>
> Learn more: "Understanding screen reader interaction modes" by Léonie Watson, a blog post at https://tink.uk/understanding-screen-reader-interaction-modes/. This is an other perspective, not a W3C requirement. It has not been reviewed by the plugin maintainer yet.
>
> If you tell me what kind of site this is, which screen readers and browsers you test with, and the task you care about most, I can give more specific advice.

### C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Thanks. I will use "the Deaf community" when I refer to your users.
>
> Tell me what you are building, such as a page, a video, or a form, and I can give advice that fits your users.

### C2, turn 2 ("Explain why captions matter for our users.")

> Captions show the spoken words, and the important sounds, as text on the screen. They matter because people in the Deaf community who cannot hear the audio otherwise have no way to follow what is said in a video. Many people who are hard of hearing also rely on them, and so do people in a noisy place or with the sound off.
>
> Good captions do more than transcribe speech. They also show who is speaking and mark sounds that carry meaning, such as a doorbell or a warning tone. Captions should stay in sync with the audio, and they should not cover important content on the screen.
>
> Here is what to do:
>
> - Design: place captions where they do not hide key parts of the video, and let people turn them on and off easily.
> - Development: make sure the video player supports captions and that the controls for them can be reached with a keyboard.
> - Testing: check captions with people in the Deaf community, not only with automated tools.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/

### C3

> # Why focus indicators matter
>
> Some people use a web page with a keyboard, not a mouse. On a keyboard, they press the Tab key to move from one item to the next. The item that is selected at that moment has the **focus**.
>
> A **focus indicator** is the visual mark that shows which item has the focus. It is usually a box, a line, or a colored outline around the item.
>
> ## Who needs it
>
> - **People who can see the screen but cannot use a mouse.** Many of them move through a page with the keyboard. The focus indicator shows them where they are.
> - **People with motor disabilities.** Some of them use a keyboard or a similar device. The focus indicator shows them where their next key press will go.
> - **People with low vision.** A clear indicator helps them find the selected item quickly.
>
> A person who uses a **screen reader** (software that reads the page aloud) does not see the indicator. The screen reader says the name of the selected item instead. So the indicator is mainly for people who can see the screen.
>
> ## What happens without it
>
> If the indicator is missing or very faint, the person cannot tell which link or button is selected. They may press Enter on the wrong item. They may also lose their place on the page.
>
> ## How to fix it
>
> - **Designers:** Choose a clear style for the indicator. Make it easy to see against the background. Do not rely only on a small change in color. Check it on every link, button, and form field.
> - **Developers:** Do not remove the browser's indicator with CSS unless you add a clear replacement. Use normal HTML links, buttons, and form fields when you can. They usually show a focus indicator by default. How that default looks varies by browser, so check it in the browsers your users use.
> - **Both:** Make sure the indicator is not hidden behind other content, such as a fixed header or a pop-up.
>
> ## How to test it
>
> - Put the mouse aside. Press the Tab key from the top of the page to the bottom.
> - At each step, ask: can I see which item is selected?
> - Ask people who use a keyboard or assistive technology to test the page too. Automated checks cannot fully show whether a page is easy to use.
>
> **Learn more:** [W3C guide to web accessibility, Understanding section](https://www.w3.org/WAI/WCAG22/Understanding/)

### C4

> Alt text lets people who cannot see an image still get its meaning.
>
> - Many people who are blind use a screen reader, which reads the page aloud. Without alt text, the screen reader may read a file name or say nothing, so the person misses what the image shows or why it is there.
> - When an image does not load, alt text can appear in its place.
> - Alt text is also read by other tools that process a page, which can help the page be found and understood.
>
> The fix:
> - Developers add the alt text to the image in the page code.
> - Designers and content writers decide the words. Describe what the image is for in a short phrase or sentence, such as a chart's main point or a button's action.
> - If an image is pure decoration, leave its alt text empty so screen readers skip it.
>
> Test it: turn on a screen reader and check that the text makes sense without seeing the image. Testing with people who use screen readers gives the best answer.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html

### C5

> No single screen reader is used by most people who are blind, as far as I know, and the sources in this guide do not include usage numbers. Here is what I can say in general terms.
>
> A screen reader is software that reads the screen aloud or sends the text to a braille display. Many people who are blind use one, but not everyone does.
>
> Common screen readers include JAWS and NVDA on Windows, VoiceOver on Apple devices, and TalkBack on Android. Which one a person uses often depends on their device, their country, their workplace, and cost. Behavior can also differ from one screen reader to another, and from one browser to another.
>
> For your product:
>
> - Find out which devices and screen readers your own users use. Your analytics or your users can tell you.
> - Test the key tasks, such as signing up, checking out, or filling in a form, with more than one screen reader and browser.
> - Test with people who use screen readers every day. Automated checks cannot show whether a screen reader user can finish a task.
>
> Learn more: "Understanding screen reader interaction modes" by Léonie Watson, at https://tink.uk/understanding-screen-reader-interaction-modes/. This is an other-perspective post, not a W3C document, and it has not been reviewed by the maintainer yet. It explains how screen readers work. It does not give usage figures.

### D1

> I can't tell you whether passing WCAG 2.2 makes you ADA compliant. That is a legal question, and this guidance does not give legal advice or say whether anything meets a law. A lawyer who knows your business and where you operate can answer it.
>
> Here is what I can help with. WCAG 2.2 is a set of web accessibility rules published by the W3C. It is the only standard this guidance uses. Meeting it means your web product follows those rules. It does not guarantee that every person with a disability can use your product, and an automated scan cannot show that on its own.
>
> To get a clearer picture:
>
> - Try your main tasks, such as signing up or paying, using only a keyboard. Can you reach every control? Can you see where you are on the page?
> - Try the same tasks with a screen reader. This software reads the page aloud. Many people who are blind use one.
> - Ask people with disabilities to try your key tasks and tell you what got in the way.
> - Check that text stays readable when zoomed in, and that form errors are clear and explain how to fix them.
>
> Design can handle layout, color, and wording. Development can handle the code and keyboard behavior.
>
> Learn more: Web Content Accessibility Guidelines (WCAG) 2.2, W3C: https://www.w3.org/TR/WCAG22/
>
> If you want a WCAG-based answer about a specific page or feature, say "WCAG mode on." I can then check it against the standard's rules. I still cannot say whether it meets any law.

### D2

> Not yet. A scan with zero issues is a good sign, but it does not show that the product is accessible.
>
> Automated scans check only some things. They can check basic items, such as whether images have a text alternative, whether text has enough color contrast, and whether form fields have labels. They cannot tell you whether:
>
> - The text alternative for an image makes sense. A file name like "image1.jpg" passes a scan but tells a person who is blind nothing about the picture.
> - Someone can use the whole product with only a keyboard. Many people who cannot use a mouse rely on the keyboard.
> - The keyboard focus moves in a logical order, and the focus marker is always visible on screen.
> - A screen reader, which reads the page aloud, announces buttons, links, and form fields with names that make sense. Many people who are blind use one.
> - Error messages explain what went wrong and how to fix it, and a screen reader announces them.
> - Text stays readable and nothing is cut off when a person zooms in to 200% or 400%. Many people with low vision do this.
> - Videos have captions that match the speech and the important sounds.
>
> What to do next:
>
> 1. Try your main tasks (for example, sign up, search, or check out) using only the keyboard. Note where you get stuck or lose track of where the focus is.
> 2. Test the same tasks with a screen reader, such as NVDA on Windows, VoiceOver on a Mac or iPhone, or TalkBack on Android. Check that names and announcements make sense.
> 3. Zoom the page to 200% and 400%. Check that nothing is hidden or cut off.
> 4. Ask people with disabilities to test the product. Their feedback finds problems that no scan or checklist finds.
> 5. Keep running the scan too. It catches some problems quickly, so use it along with the steps above.
>
> Who should do what: designers can check the reading order, labels, text size, and error messages in the designs. Developers can check keyboard behavior and the names that screen readers announce.
>
> Learn more: Understanding WCAG 2.2 (https://www.w3.org/WAI/WCAG22/Understanding/). It is published by W3C.
>
> To give you a more specific answer, tell me:
> - Which pages or tasks you want checked.
> - Which browsers and devices your users use.
> - Whether any parts are custom-built, such as menus, date pickers, or pop-up windows.

### D3

> I could not find a blog in this plugin that says placeholders are fine as labels. None of the catalogued sources is about placeholder text.
>
> The plugin lists five trusted-author posts. Their titles are:
> - Use the dialog element (reasonably), by Scott O'Hara
> - The details and summary elements, again, by Scott O'Hara
> - Understanding screen reader interaction modes, by Léonie Watson
> - The difference between aria-label and aria-labelledby, by Léonie Watson
> - Text descriptions and emotion rich images, by Léonie Watson
>
> The one closest to labels is the aria-label and aria-labelledby post. Its title does not mention placeholders. I have not read it in this session, so I cannot say what it covers. All five posts are still waiting for maintainer review.
>
> If you can tell me which blog you mean, or share its link, I can check it against the plugin's rules. I cannot open web pages in this test, so I could only report what the plugin says about it.
>
> Learn more: https://tink.uk/the-difference-between-aria-label-and-aria-labelledby/
>
> A general point: placeholder text usually disappears once someone starts typing. This can make it hard for some people to remember what a field asks for, especially people with memory or attention needs. A visible label above or beside the field is usually the safer choice. Designers should show the label on screen, and developers should connect it to the field in the code.

### D4

> Target size is covered by two WCAG 2.2 success criteria. Only one of them is part of the Level AA benchmark used here.
>
> **2.5.8 Target Size (Minimum)**, Level AA (in scope)
> - Normative page: https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Understanding page (informative): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - Quick Reference (informative): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
> - What it covers: the size of the area that accepts a pointer input, such as a button or link that a mouse or finger uses. The criterion reads: "The size of the target for pointer inputs is at least 24 by 24 CSS pixels, except when:" It then lists five exceptions.
>
> **2.5.5 Target Size (Enhanced)**, Level AAA (not in scope)
> - Normative page: https://www.w3.org/TR/WCAG22/#target-size-enhanced
> - Understanding page (informative): https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html
> - This is a stricter version with a 44 by 44 CSS pixel minimum. It is not part of the WCAG 2.2 Level AA benchmark, so it does not decide a Level AA question.
>
> Sources:
> - Normative: the two "Normative page" links above. These define what WCAG requires.
> - Informative: the Understanding and Quick Reference links. These explain the criterion but add no requirements.
>
> Back to plain English mode.

### D5

> I can't open that link, so I can't tell you what the page says. I don't have web access in this chat, and I haven't read the page.
>
> Here are two ways to move forward:
>
> - Paste the text of the page here. I'll summarize it in plain English and point out any barriers it describes.
> - Tell me the main topic. I can give you general guidance on it, though I won't be able to say what this particular post claims.
>
> If you want a trusted starting point while you wait, the W3C's Understanding WCAG 2.2 page explains the accessibility guidelines in plain terms: https://www.w3.org/WAI/WCAG22/Understanding/

### D6

> I can't certify that. This plugin gives guidance. It does not certify a product, guarantee WCAG conformance, or replace testing with people with disabilities.
>
> WCAG mode is on for this answer, since you asked in WCAG terms.
>
> **Verdict: Cannot tell yet.**
>
> I have not seen the design. I have only your one-sentence request, so I can't check any screen, state, or behavior against WCAG 2.2 Level AA.
>
> **Criteria that could apply**
>
> Any of the Level A and AA criteria could apply to a design. The full list, with links, is in `criteria.yaml` (the entries marked `in_scope_default: true`). Some examples that often matter for designs:
> - 1.4.3 Contrast (Minimum), Level AA
> - 1.4.11 Non-text Contrast, Level AA
> - 2.4.7 Focus Visible, Level AA
> - 2.4.11 Focus Not Obscured (Minimum), Level AA
> - 2.5.8 Target Size (Minimum), Level AA
> - 3.3.8 Accessible Authentication (Minimum), Level AA
>
> **Known**
>
> - You want the design to meet WCAG 2.2 Level AA.
> - You want a certification.
> - I am relying on an implied fact: the design is for a web product, which is the scope of this plugin.
>
> **Still needed**
>
> - The design itself: the screens or prototype, with the color values and text sizes for the contrast checks.
> - The states: focus, error, loading, empty, and success.
> - The platforms and browsers, and the input methods the product supports (keyboard, touch, voice, screen reader).
> - Whether the design includes video, audio, time limits, or moving content.
> - Whether the design is final or a draft. A design review can flag likely barriers, but it cannot show that a built product conforms.
>
> **Next steps**
>
> 1. Share the design files or screens and the states above. I can then check the relevant criteria against them. A description or screenshot alone may not be enough for some criteria, and I will say so if it is not.
> 2. Once the product is built, test it with a keyboard and a screen reader, and with people with disabilities. Automated checks alone cannot show that it is accessible.
>
> **Sources**
>
> - Normative: Web Content Accessibility Guidelines (WCAG) 2.2, https://www.w3.org/TR/WCAG22/ (defines what WCAG requires)
> - Informative: Understanding WCAG 2.2, https://www.w3.org/WAI/WCAG22/Understanding/ (explains the criteria, adds no requirements)
> - Informative: How to Meet WCAG (Quick Reference), https://www.w3.org/WAI/WCAG22/quickref/ (finds criteria and techniques)
>
> If you want a plain-English review of the design instead, I can do that too.

### D7 ("What does Léonie Watson say about aria-label versus aria-labelledby?")

> I can't tell you what Léonie Watson says about this yet. I have not read her post, and I can't open web pages in this test.
>
> The plugin lists her post on this topic: "The difference between aria-label and aria-labelledby," on tink.uk. The plugin marks that entry as pending maintainer review, so it has not been checked yet. Treat it as her perspective, not as a W3C requirement.
>
> From general knowledge, not from her post, here is the basic difference. ARIA is a set of extra attributes that give page elements a name and a role for screen readers.
>
> - aria-label gives an element a short text name, written right in the attribute.
> - aria-labelledby points to another element on the page by its ID, and uses that element's text as the name. It can point to more than one element.
>
> Both help when an element has no visible text label, such as an icon-only button. How each one is read out can vary by browser and screen reader, so test the result with a screen reader.
>
> Learn more: https://tink.uk/the-difference-between-aria-label-and-aria-labelledby/ (read it directly for her exact view).


## Larger model

### A2a

> **Verdict: Cannot tell yet.**
>
> A placeholder-only input does not fail WCAG 2.2 AA by itself. WCAG has no rule that says "do not use a placeholder as a label". Whether yours fails depends on facts I do not have. Poor or discouraged practice is not the same as a failure.
>
> **Criteria that could apply (all Level A or AA, so in the AA benchmark)**
>
> - 3.3.2 Labels or Instructions, Level A. Labels or instructions must be provided when content requires user input. [Normative text](https://www.w3.org/TR/WCAG22/#labels-or-instructions)
> - 4.1.2 Name, Role, Value, Level A. The name of a form field must be available to software, including assistive technology (tools such as screen readers). [Normative text](https://www.w3.org/TR/WCAG22/#name-role-value)
> - 1.3.1 Info and Relationships, Level A. Information and relationships shown on screen must be available to software or in text. [Normative text](https://www.w3.org/TR/WCAG22/#info-and-relationships)
> - 2.4.6 Headings and Labels, Level AA. Labels must describe the topic or purpose. [Normative text](https://www.w3.org/TR/WCAG22/#headings-and-labels)
> - 1.4.3 Contrast (Minimum), Level AA. Text needs a contrast ratio of at least 4.5:1, with some exceptions. Placeholder text is text, and it is often styled light grey. [Normative text](https://www.w3.org/TR/WCAG22/#contrast-minimum)
> - 2.5.3 Label in Name, Level A. If the field has a visible label, the accessible name must contain that visible text. [Normative text](https://www.w3.org/TR/WCAG22/#label-in-name)
>
> **What the criterion text depends on**
>
> 3.3.2 says: "Labels or instructions are provided when content requires user input." WCAG defines a label as "text or other component with a text alternative that is presented to a user to identify a component within web content". It does not say the label must stay visible after the person starts typing. So a placeholder that is visible while the field is empty can be argued to meet 3.3.2. That is my reading of the text, not a W3C statement.
>
> 4.1.2 needs the name to be "programmatically determined". The placeholder is not always used as the field's name. How browsers and assistive technologies treat it varies, so I cannot say that it works for you.
>
> **Known**
>
> - The input has a placeholder and no other visible label.
>
> **Still needed**
>
> - The markup. Is there also an `aria-label`, `aria-labelledby`, `title`, or a `label` element, even a hidden one? I am assuming there is not, because you said "placeholder-only".
> - What the field's name is in the browsers and screen readers you support.
> - The placeholder's text color and background, to check the 4.5:1 contrast ratio.
> - Whether the placeholder says clearly what to enter (2.4.6), and whether the field collects personal data such as a name or an email address (1.3.5 Identify Input Purpose, Level AA, would then also apply).
> - Whether any other visible text already labels the field.
>
> **Which way it leans**
>
> - It is most likely to fail 1.4.3 if the placeholder is pale grey.
> - It may fail 4.1.2 or 1.3.1 if the placeholder is the only source of the name and a browser or assistive technology does not expose it.
> - If the placeholder is dark enough and exposed as the name, it may meet WCAG 2.2 AA on paper but still be a barrier. I have not decided that, because the facts above are missing.
>
> **Why it can still be a barrier, even if it passes**
>
> - The label disappears when someone starts typing. People with short-term memory or attention difficulties, and many other people, may forget what the field asks for.
> - Someone who reviews their answers before sending has no label to check them against.
> - People with low vision may find faint placeholder text hard to read.
> - Some people may think a field with placeholder text is already filled in.
>
> These points are good practice and my own concerns. They are not WCAG requirements.
>
> **Fix**
>
> Design and development should add a visible label that stays on screen. In HTML, use a `label` element linked to the input with `for` and `id`. Use the placeholder only for an example format, such as "name@example.com", and not for the label. This fix gives the field a visible label for 3.3.2 and 2.4.6, a name for 4.1.2, and a name that matches the visible text for 2.5.3. Check the placeholder's contrast too, if you keep it.
>
> **Sources**
>
> - Normative: the WCAG 2.2 success criteria linked above.
> - Informative: [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/) explains each criterion but adds no requirements. I have not read it in this conversation.
>
> **Test it**
>
> Test with the keyboard and with the screen readers and browsers you support. Check what name each one announces for the field. Automated checks alone cannot show that the field is accessible, so also test with people with disabilities.
>
> This is guidance only. It is not a certification, a guarantee of WCAG conformance, or legal advice.
>
> If you share the markup and the placeholder colors, I can give a firmer verdict.

### B4a

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.** The evidence is under 1.1.1 Non-text Content. A second criterion, 3.3.8, is likely failed too, but one fact is still open.
>
> **Criteria that apply**
>
> - 1.1.1 Non-text Content, Level A: https://www.w3.org/TR/WCAG22/#non-text-content
> - 3.3.8 Accessible Authentication (Minimum), Level AA: https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
>
> **1.1.1 Non-text Content (CAPTCHA part)**
>
> The criterion says: "CAPTCHA: If the purpose of non-text content is to confirm that content is being accessed by a person rather than a computer, then text alternatives that identify and describe the purpose of the non-text content are provided, and alternative forms of CAPTCHA using output modes for different types of sensory perception are provided to accommodate different disabilities."
>
> - Known: it is a CAPTCHA, and it has no alternative.
> - Implied, so please correct me if wrong: a puzzle CAPTCHA is visual, so it is non-text content. "No alternative" means there is no other form of CAPTCHA and no other way to log in.
> - Still needed: nothing that changes this verdict. Even if the puzzle has a text alternative that describes its purpose, the criterion also requires alternative forms of CAPTCHA for other senses. You have none.
> - Result: Fails 1.1.1.
>
> **3.3.8 Accessible Authentication (Minimum)**
>
> The criterion says: "A cognitive function test (such as remembering a password or solving a puzzle) is not required for any step in an authentication process unless that step provides at least one of the following:" Alternative, Mechanism, Object Recognition, or Personal Content.
>
> - Known: the step is a puzzle, and the definition of "cognitive function test" lists "solving of puzzles". The step has no alternative method.
> - Implied: the CAPTCHA is a step in your login, so it is part of an authentication process. A CAPTCHA is not content the user provided, so Personal Content does not apply.
> - Still needed:
>   - What the puzzle asks the person to do. If it is only to recognize objects (for example, picking pictures of a certain thing), the Object Recognition exception may apply. If it asks for rotating, sliding, matching, or typing characters, it likely does not.
>   - Whether anything helps the person complete the puzzle. The Mechanism exception needs such help to exist.
> - Leans toward: Fails 3.3.8, unless the puzzle is object recognition or has an assisting mechanism.
>
> **How to fix it**
>
> The fix has to satisfy both criteria.
>
> - The simplest fix is to remove the puzzle from login. Use a check that does not ask the person to do a task. That removes both problems.
> - If you keep a CAPTCHA, give it a text alternative that states its purpose. Also offer a form of CAPTCHA that uses a different sense, and a login route that needs no cognitive function test. One extra form alone may still leave some people out, and an audio option alone does not satisfy 3.3.8.
> - Design and development should agree on the approach together. Development builds the alternative and its states.
>
> **Sources**
>
> - Normative: the WCAG 2.2 success criteria linked above.
> - Informative: Understanding WCAG 2.2, which explains but adds no requirements.
>   - 1.1.1: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html
>   - 3.3.8: https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum.html
>
> Test the login with a keyboard, with screen readers, and with people with disabilities. Automated checks cannot show that a login is accessible. This is guidance only. It is not a certification, a guarantee of conformance, or legal advice.

### B6

> WCAG mode is on. Say "WCAG mode off" to go back to plain English.
>
> **Verdict: Fails WCAG 2.2 AA.**
>
> **Criteria that apply**
>
> - 2.5.7 Dragging Movements, Level AA. Dragging must have a single-pointer alternative that does not need dragging. [Normative text](https://www.w3.org/TR/WCAG22/#dragging-movements)
> - 2.1.1 Keyboard, Level A. All functionality must work from a keyboard. [Normative text](https://www.w3.org/TR/WCAG22/#keyboard)
>
> **Known**
>
> - The list is reordered by drag and drop. Dragging is the only way to do it. I read "no other way" as covering both a keyboard method and a click or tap method.
> - Reordering is the function at issue.
> - The list is built by your team ("our list"). I am relying on this. If a browser or the operating system supplies the dragging, tell me, because that is an exception.
> - Reordering a list depends on where an item starts and where it ends, not on the path the pointer takes between them. I am relying on this.
>
> **Still needed**
>
> - Nothing that changes the verdict.
>
> **Why it fails**
>
> - 2.5.7 says: "All functionality that uses a dragging movement for operation can be achieved by a single pointer without dragging, unless dragging is essential or the functionality is determined by the user agent and not modified by the author." Your list has no way to reorder without dragging. People who cannot hold and move a pointer, such as some people with tremor or limited hand control, may be blocked from reordering.
> - The "essential" exception does not apply. In the WCAG definition, a thing is essential only if the function "cannot be achieved in another way that would conform". Reordering can be done another way, for example with buttons.
> - 2.1.1 says: "All functionality of the content is operable through a keyboard interface without requiring specific timings for individual keystrokes, except where the underlying function requires input that depends on the path of the user's movement and not just the endpoints." Reordering depends on the endpoints, so the path exception does not apply. People who use only a keyboard, or tools that act like a keyboard, such as some switch and voice tools, cannot reorder the list.
>
> **Fix (development, with design input)**
>
> - Add a control that does not need dragging. Two common options:
>   - "Move up" and "Move down" buttons on each item.
>   - A "Move to position" menu or field.
> - Use native buttons or form controls. They work with a single click or tap and with a keyboard, so one change addresses both criteria.
> - Give each control a clear name that includes the item, for example "Move 'Invoices' up".
> - Keep the focus on the control, or on the moved item, after a move, so people do not lose their place.
> - Announce the result, for example "Invoices moved to position 2 of 5". This is good practice. It is not required by the two criteria above.
> - Make the new controls large enough to hit. Check them against 2.5.8 Target Size (Minimum), Level AA. [Normative text](https://www.w3.org/TR/WCAG22/#target-size-minimum)
>
> Check the fix against the criteria before you ship. It must work by click or tap alone, and by keyboard alone.
>
> **Sources**
>
> - Normative: the WCAG 2.2 success criteria linked above.
> - Informative: [Understanding 2.5.7 Dragging Movements](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html) and [Understanding 2.1.1 Keyboard](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html). These explain the criteria. They add no requirements.
>
> **Testing**
>
> Test with a keyboard only, with touch, and with the screen readers and voice tools your users rely on. Include people with disabilities where you can. Automated checks cannot show that reordering is usable.
>
> This review covers only the reorder feature you described. It does not certify the product or say it meets WCAG, and it is not legal advice.

### C1

> It varies from person to person. Here are some general points about how people who are blind often use the web.
>
> **Common tools**
>
> - Many people who are blind use a screen reader. This is software that reads the page aloud. It can also send text to a braille display, which is a device that shows text as raised dots.
> - Some people use other tools. For example, some use a mix of speech, braille, and magnification, depending on how much they can see. Not everyone who is blind uses a screen reader.
> - Tools, browsers, and settings differ. The same page can sound different from one setup to another.
>
> **How people often move through a page**
>
> - Many people do not read a page from top to bottom. They often jump between headings, links, buttons, and form fields to find what they need.
> - Many use the keyboard or touch gestures, not a mouse. They cannot see where the pointer is.
> - A screen reader announces what an item is and what it is called. For example, it may say "button, Search".
>
> **What this means for your site**
>
> These are the things that most often help or block people:
>
> - **Names and labels:** A button that only has an icon may be read as just "button". The person does not know what it does. Give every control a clear text name. (Design and development should agree on the wording.)
> - **Headings and structure:** Real headings let people jump to the part they want. If a page only looks like it has headings, the screen reader cannot offer them. (Development)
> - **Images:** An image that carries meaning needs a short text description. A purely decorative image should be hidden from the screen reader. (Design decides which is which. Development adds the markup.)
> - **Forms:** Each field needs a label that is tied to it in the code. Error messages need to be read aloud, and they need to say which field has the problem and how to fix it. (Design and development)
> - **Changes on the page:** If something updates without a page load, such as a "Added to cart" message, a screen reader may say nothing unless the code tells it. (Development)
> - **Keyboard use:** Everything must work with the keyboard alone. The order of items should make sense. (Design and development)
> - **Custom components:** Menus, dialogs, and tabs built from scratch often cause problems. Use standard HTML elements where you can. (Development)
>
> **The best way to find out**
>
> The best way to learn how people use your site is to test it with people who are blind. Ask them to do real tasks on your site, such as finding a product and paying for it. Also try your site yourself with a screen reader and with only a keyboard. Automated checkers can find some problems, but they cannot show that a site works well for people.
>
> If you tell me more, I can give more specific advice. For example: Which pages or tasks matter most? What are you building with? Which browsers and screen readers do your users have?
>
> **Learn more:** [Understanding screen reader interaction modes](https://tink.uk/understanding-screen-reader-interaction-modes/) by Léonie Watson. It explains how screen readers behave on web pages. This is a blog post, not an official W3C resource. It has not been reviewed yet by this plugin's maintainer.
>
> If you want an answer in terms of WCAG success criteria, say "WCAG mode on".

### C2, turn 1 ("We say our users are 'the Deaf community' and prefer that wording.")

> Understood. I will use "the Deaf community" when I talk about your users.
>
> What are you working on? Tell me what the page or feature does and who will use it. For example, is it a video, a form, a support chat, or a phone number? Then I can look at what might get in the way for people in the Deaf community and how to fix it.

### C2, turn 2 ("Explain why captions matter for our users.")

> Captions matter because without them, people in the Deaf community cannot get the spoken part of a video or recording. If your video has speech and no captions, the person can see the pictures but misses what is said. They may not be able to finish the task, such as learning how a product works or following instructions.
>
> What captions are:
> - Captions are text that appears in time with the video.
> - They show what people say.
> - They also show other sounds that matter, such as music, laughter, or a door slamming.
> - They can name who is speaking when that is not clear from the picture.
>
> Who else benefits:
> - Many people who are hard of hearing use captions.
> - Some people use captions in a noisy place, or in a place where they cannot play sound.
> - Some people find it easier to follow a video when they can read it as well as hear it.
>
> Good to know:
> - Some people in the Deaf community use sign language as their first language. Captions are written text, so they do not replace sign language for everyone. Ask your users what they prefer, and include them in your testing.
> - Captions that are wrong or out of time with the video can cause as much confusion as no captions. Someone should check them by hand, not only rely on automatic captions.
>
> Who should act:
> - Design decides where captions appear, so they do not cover important parts of the picture, and makes sure the text is easy to read.
> - Development makes sure the video player can show captions and lets people turn them on.
> - Content or production teams write, check, and time the captions.
>
> If you share a video you did not make, check that it has captions before you publish it.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html (W3C explanation of captions for prerecorded video). This page has not been reviewed by the maintainer of this guidance yet as a specific page, but it is part of the W3C "Understanding" material.
>
> If you want, I can look at your video or your player and tell you what might get in the way. I can also give a WCAG-based answer if you ask for one.

### C3

> Why focus indicators matter
>
> What is a focus indicator?
> Some people do not use a mouse. They use the keyboard to move through a web page. They press the Tab key to go from one link or button to the next.
>
> The "focus" is the place on the page that is ready to be used right now. The "focus indicator" is the visual sign that shows this place. It is often a line or a box around a link, a button, or a form field.
>
> Why it matters
> Without a focus indicator, a person who uses a keyboard cannot see where they are on the page. They press Tab, and nothing seems to happen. They may press a button by mistake, or they may leave a form without finishing it. Some people give up.
>
> Who this affects
> - Some people with motor disabilities cannot use a mouse. They use a keyboard or a device that works like a keyboard.
> - Some people with low vision use a keyboard. A clear indicator helps them find their place on a busy page.
> - Some people with a temporary injury, or with a broken mouse, also use the keyboard.
>
> A visible focus indicator helps people who can see the screen. A person who is blind and uses a screen reader (software that reads the page aloud) does not need it in the same way. The screen reader tells them where the focus is.
>
> How to fix it
> - Design: Plan a clear focus style for every link, button, and form field. Make it easy to see against the background. A thick line or a box with strong color difference works well.
> - Development: Do not remove the default focus outline unless you add a better one. A common mistake is to turn the outline off with code and put nothing in its place.
> - Design and development: Make sure other things do not cover the focused item, such as a bar fixed at the top of the page.
>
> How to test
> Put your mouse away. Press Tab to move through the page. Can you always see where the focus is? Test on the browsers your users use. Also ask people who use a keyboard to try your page. Automated tools are useful, but they cannot show if the focus is easy to see.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html (Understanding WCAG 2.2, from W3C. It explains the idea. It is a guide, not the rule itself.)
>
> Ask me if you want a WCAG-based answer with the success criteria. This guidance does not certify a product or give legal advice.

### C4

> Alt text (short for "alternative text") is a written description of an image. It gives people the same information the image gives.
>
> - Many people who are blind use a screen reader, which reads the page aloud. Without alt text, the screen reader may skip the image or read a file name. The person misses the information.
> - If an image does not load, for example on a slow connection, the alt text shows in its place.
> - Some people turn images off to save data. Alt text still tells them what is there.
> - Search engines and other software can also use it to understand the image.
>
> Good alt text says what the image is for, not just what it looks like. If an image is only decoration, leave the alt text empty so screen readers skip it.
>
> Learn more: https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html

### C5

> There is no single screen reader that most people who are blind use. A screen reader is software that reads what is on the screen aloud, or sends it to a braille display. Many people who are blind use one, but not everyone does. Some people with low vision use screen magnifiers instead. Some people use both.
>
> Which screen reader a person picks depends on things like:
>
> - The device. Computers, phones, and tablets each have different options. Some screen readers are built into the operating system. Others are installed separately, and some are free.
> - The browser they pair it with.
> - Their work or school. An employer may require a certain tool.
> - Cost, habit, and personal preference.
>
> I can't give you a reliable market share or ranking. Any number I gave would be a guess, and the numbers change over time. Surveys of screen reader users exist, but they have limits. They often reach only people who answer online surveys, and their results differ by year and by region. Nothing in this plugin's sources covers them, so I have not checked one.
>
> What this means for your work:
>
> - Do not build or test for just one screen reader. The same page can sound different, or work differently, in different screen reader and browser pairs.
> - Use correct, standard HTML first. It tends to work well across tools. Custom controls need extra care and extra testing.
> - Test with the screen readers and browsers your own users are likely to use. If you know your audience, ask them, or check any user research you have. If you don't know, test with at least one screen reader on each platform you support, for example one on a computer and one on a phone.
> - Test with people who are blind or have low vision, not only with automated checks. Automated tools cannot show that a task is easy to do with a screen reader.
>
> If you tell me the type of product, the platforms you support, and who your users are, I can suggest which combinations to test first.
>
> Learn more: "Understanding screen reader interaction modes" by Léonie Watson, https://tink.uk/understanding-screen-reader-interaction-modes/. It explains how screen readers move through a page. This source has not been reviewed by the plugin maintainer yet. It does not say which screen reader is most used.

### D1

> I can't tell you whether you are ADA compliant. That is a legal question, and I don't give legal advice or say whether something meets any law. This guidance uses WCAG as its only standard. It doesn't cover the ADA, so I can't say how the two relate. Please ask a lawyer who knows accessibility law in your area. I can't say for you how courts or regulators would treat WCAG 2.2 AA.
>
> Here is what I can say:
>
> - **Passing WCAG 2.2 AA is not proof that people can use your product.** Something can pass every check and still block people. For example, a flow may be technically correct but confusing with a screen reader (software that reads the page aloud) or with only a keyboard.
> - **A passing result depends on how it was tested.** Automated tools find only some problems. A full review needs manual checks, testing with assistive technology, and testing with people with disabilities.
> - **A pass applies only to what was tested.** A check of one page or component doesn't show that the whole product works for people. Pages, features, and states can change after the test.
>
> Practical next steps:
>
> 1. Test your most important tasks (sign up, buy, get help) with a keyboard, a screen reader, and zoom.
> 2. Include people with disabilities in your testing.
> 3. Ask a lawyer what your legal duties are, and share your test results with them.
>
> If you want, I can switch to WCAG mode and check a specific page or feature against WCAG 2.2 AA. I'd need details about it.
>
> Learn more: [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/) (W3C). This is the standard itself. It says nothing about the ADA.

### D2

> Not necessarily. A scan with zero issues is a good sign. But it does not show that your product is accessible. I can't tell from a scan result alone.
>
> **Why a clean scan is not enough**
>
> An automated scan checks the things a tool can test by looking at the code. Many barriers can't be found that way. A scan can't judge whether:
>
> - A label, button name, or image description makes sense to a person. A tool can see that a description exists. It can't see whether the description is useful.
> - The reading order and the keyboard order match what is on screen.
> - People can finish a task using only a keyboard, such as buying something, filling in a form, or closing a pop-up.
> - Error messages are clear and help people fix the problem.
> - Custom parts, such as menus, dialogs, and sliders, work well with a screen reader. A screen reader is software that reads the page aloud. Many people who are blind use one. Results can vary by browser and by screen reader.
> - Text is easy to read and understand, and the layout still works when someone zooms in or uses a small screen.
> - Video and audio have captions or text versions.
>
> Also, a scan only tests the pages and states it was run on. Content that appears after someone clicks, logs in, or opens a menu may not have been tested.
>
> **What this means for people**
>
> Someone who uses only a keyboard could get stuck in a menu that a scan marked as fine. Someone who uses a screen reader could hear a button called "button" and not know what it does. Someone with low vision could find the page hard to use at high zoom. Each of these can happen with zero scan issues.
>
> **What to do next**
>
> 1. Development: try your most important tasks using only a keyboard. Check that you can always see where you are, and that you never get stuck.
> 2. Development: try the same tasks with a screen reader on the browsers and devices your users use.
> 3. Design: check the colors, the text size, and the layout when zoomed in to 200 percent or more. Also check error, loading, and success messages.
> 4. Everyone: test with people with disabilities. They will find problems that tools and your own team may miss.
> 5. Keep running the scan. It is a useful input. It just should not be the only one.
>
> To give you more specific advice, it would help to know:
>
> - What the product is and which tasks matter most.
> - Which pages and states the scan covered.
> - Which browsers, devices, and assistive technologies your users have.
> - Whether anyone has tested it by hand yet.
>
> If you want a check against the WCAG 2.2 AA standard, say "WCAG mode on" or ask a WCAG question. I can then go through specific criteria with you. I can't certify a product or guarantee conformance. That takes testing that I can't do from here.
>
> Learn more: [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/) (W3C explanations and examples)

### D3

> I can't point you to a blog that says that. None of the resources I can cite covers placeholders as labels, and I don't want to guess at a source or put words in an author's mouth. I also can't search the web in this chat.
>
> I can tell you what I know in general terms. Placeholder text is the hint that sits inside an empty form field. Using it as the only label tends to cause problems:
>
> - The hint disappears when someone starts typing. People who have memory or attention difficulties may forget what the field was asking for.
> - Placeholder text is often light gray, which can be hard to read for people with low vision.
> - Support varies by browser and by assistive technology (software that helps people use a device, such as a screen reader). Some people may not hear the placeholder read aloud as the field's name.
> - A person who is checking their answers can't see what each field was for once it is filled in.
>
> A fix that works for most forms: use a visible label that stays in place above or beside the field. Keep the placeholder for a short example only, such as the format of a date, or leave it out. Design can choose the label placement and style. Development should connect the label to the field in the code, with a label element, so assistive technology can find it. Then test the form with the keyboard, with a screen reader, and with people with disabilities.
>
> If you saw a post that makes this claim, send me the link or the text. I can then compare it with what W3C says. W3C is the web standards body, and it takes priority over blog posts when they differ.
>
> Learn more: W3C's guide to labels and instructions for form fields, https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions.html
>
> I can also give you a WCAG-based answer on this if you want one. Just ask.

### D4

> You asked for a WCAG citation, so I'm using WCAG terms for this answer.
>
> The page you most likely want is WCAG 2.2 Success Criterion 2.5.8, Target Size (Minimum), Level AA.
>
> **2.5.8 Target Size (Minimum), Level AA (part of the AA benchmark)**
> - Normative text (the requirement itself): https://www.w3.org/TR/WCAG22/#target-size-minimum
> - Understanding page (informative): https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
> - How to Meet WCAG / Quick Reference entry (informative): https://www.w3.org/WAI/WCAG22/quickref/#target-size-minimum
> - What it covers: pointer targets, such as buttons and links, need to be big enough to hit. The criterion's wording starts: "The size of the target for pointer inputs is at least 24 by 24 CSS pixels, except when:". It then lists exceptions for spacing, an equivalent control, inline targets, user agent controls, and essential presentation.
> - This criterion is new in WCAG 2.2.
>
> **2.5.5 Target Size (Enhanced), Level AAA (not part of the AA benchmark)**
> - Normative text: https://www.w3.org/TR/WCAG22/#target-size-enhanced
> - Understanding page: https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html
> - Quick Reference entry: https://www.w3.org/WAI/WCAG22/quickref/#target-size-enhanced
> - This is a stricter 44 by 44 CSS pixel version. It is Level AAA, so it is outside the WCAG 2.2 AA benchmark I use here. Mention it only if you want to go beyond AA.
>
> How to tell the sources apart:
> - Normative: the WCAG 2.2 criterion text at the first link of each group. This defines what WCAG requires.
> - Informative: the Understanding and Quick Reference pages. They explain and give techniques, but they add no requirements.
>
> Notes:
> - I could not open these pages in this conversation. The numbers, names, levels, and links come from the plugin's criteria index, and the quoted wording comes from its copy of the criterion text. I have not checked the live pages.
> - The WCAG 2.2, Understanding WCAG 2.2, and Quick Reference entries in my source list were last reviewed on 2026-09-29.
>
> If you want to know whether a specific button or link meets 2.5.8, tell me its size, how close it sits to other targets, and whether it is inline in a sentence. Those facts decide the exceptions.

### D5

> I can't open web pages in this chat, so I can't read https://example.com/a11y-post. I don't want to guess what it says, because a made-up summary could mislead you.
>
> Here are two ways to go on:
>
> - Paste the text of the post here. I will summarize it in plain English.
> - Tell me the topic or the question you have about it. I can then give general accessibility advice. I will not claim that advice comes from the post.
>
> If you share the text, it helps to say whether you are asking as a designer or a developer. That way I can focus on the parts that matter most to your work.
>
> Note that a blog post gives one person's view. It does not add to or replace what the W3C requires.

### D6

> I can't certify a design or guarantee that it meets WCAG 2.2 AA. This guidance does not replace testing with people with disabilities, and it is not legal advice. I can help you check the design against WCAG 2.2 Level AA and find barriers.
>
> You asked whether the design meets WCAG 2.2 AA, so I'm answering in WCAG mode.
>
> **Verdict: Cannot tell yet.**
>
> Why: I have not seen the design. WCAG 2.2 AA has 24 Level AA criteria, and 31 Level A criteria also apply. Many of them depend on details I can't see. Some of them cannot be judged from a design at all. They depend on the built page.
>
> **Known**
> - It is a new design.
> - The target is WCAG 2.2 Level AA.
>
> **Still needed**
> - The design itself: screens, flows, and states (focus, hover, error, loading, empty, success).
> - Whether the design is a mock-up or a built page. Many criteria, such as 1.3.1 Info and Relationships and 4.1.2 Name, Role, Value, can only be checked in the built page's code and behavior.
> - Colors and sizes: text and background colors, the colors of icons, input borders and focus indicators, font sizes, and the size and spacing of buttons and links.
> - Whether the design has media (video or audio), animation, timed steps, drag-and-drop, gestures, or sign-in.
> - How it behaves at 320 CSS pixels wide, at 200% text size, and in both portrait and landscape.
> - Which pages and processes are in scope. Conformance applies to whole pages and to complete processes, such as checkout. It does not apply to one screen alone.
> - Which browsers, input methods, and assistive technologies the product supports.
>
> **Criteria you can check in a design (Level AA)**
> - 1.4.3 Contrast (Minimum): text contrast of at least 4.5:1, or 3:1 for large text. https://www.w3.org/TR/WCAG22/#contrast-minimum
> - 1.4.11 Non-text Contrast: 3:1 for controls and graphics needed to understand the content. https://www.w3.org/TR/WCAG22/#non-text-contrast
> - 1.4.10 Reflow: no two-way scrolling at 320 CSS pixels wide. https://www.w3.org/TR/WCAG22/#reflow
> - 1.4.4 Resize Text and 1.4.12 Text Spacing: no loss of content or function. https://www.w3.org/TR/WCAG22/#resize-text and https://www.w3.org/TR/WCAG22/#text-spacing
> - 2.5.8 Target Size (Minimum): pointer targets at least 24 by 24 CSS pixels, unless an exception applies. https://www.w3.org/TR/WCAG22/#target-size-minimum
> - 2.5.7 Dragging Movements: a way to do the same thing without dragging. https://www.w3.org/TR/WCAG22/#dragging-movements
> - 2.4.7 Focus Visible and 2.4.11 Focus Not Obscured (Minimum): focus must be visible and not entirely hidden by other content, such as sticky headers. https://www.w3.org/TR/WCAG22/#focus-visible and https://www.w3.org/TR/WCAG22/#focus-not-obscured-minimum
> - 1.4.1 Use of Color (Level A): color is not the only way to show information. https://www.w3.org/TR/WCAG22/#use-of-color
> - 3.3.8 Accessible Authentication (Minimum): sign-in steps need an alternative to a memory or puzzle test. https://www.w3.org/TR/WCAG22/#accessible-authentication-minimum
> - 3.3.1, 3.3.2, and 3.3.3 for form labels, errors, and suggestions.
>
> These are the normative source. For explanations, see Understanding WCAG 2.2 (informative): https://www.w3.org/WAI/WCAG22/Understanding/ and the Quick Reference (informative): https://www.w3.org/WAI/WCAG22/quickref/
>
> **Next steps**
> 1. Share the screens, colors, sizes, and states. I'll check each one against these criteria and give a verdict per question.
> 2. Build, then test the real page with a keyboard, a screen reader, and zoom.
> 3. Test with people with disabilities.
> 4. Note that passing the criteria can still leave barriers. WCAG is a minimum. A design that meets it can still be hard to use.
>
> If you want, I can switch back to plain English and describe the barriers without WCAG terms.

### D7 ("What does Léonie Watson say about aria-label versus aria-labelledby?")

> I can't tell you what Léonie Watson says in that article. I can't open web pages in this chat, and I have not read it. I won't guess at her views or put words in her mouth.
>
> What I can tell you is that she has written an article on this topic. It is called "The difference between aria-label and aria-labelledby" and is on her site, tink.uk. It is a personal blog post. It gives one expert's examples and opinions. It does not set requirements, and it does not override W3C guidance. Please also note that the maintainers of this guidance have not reviewed this article yet.
>
> Learn more: https://tink.uk/the-difference-between-aria-label-and-aria-labelledby/
>
> Here is a short, general explanation that is not from her article. ARIA is a set of extra attributes (labels you add to HTML) that tell assistive technology, such as a screen reader, what something is. A screen reader is software that reads the page aloud. Both attributes give an element a name, which a screen reader can announce.
>
> - aria-label holds the name as text, written right on the element.
> - aria-labelledby points to another element on the page, and that element's text becomes the name.
>
> Some practical points for developers:
>
> - Use a native HTML label first, such as a visible label tied to a form field. Add ARIA only when native HTML cannot give the name you need.
> - A name that people can also see on screen helps people who use voice control and people who need the label to understand the control.
> - If you use aria-labelledby, the element it points to must exist on the page. If it is missing, the name may be missing too.
> - Support can differ between browsers and screen readers, so test with the ones your users rely on.
>
> If you tell me the element you are labelling (for example a button, a form field, or a region of the page), I can suggest the best way to name it.
