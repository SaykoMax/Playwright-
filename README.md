Based on your screenshots and the NVDA Speech Viewer:

NVDA reads the book title twice (e.g., "Machines of Thought cover" followed by "Machines of Thought").

NVDA also reads the original crossed-out price (e.g., "$18.00"), even though it is only meant to be a visual indication of a discount.


These are two separate accessibility issues.


---

Issue 1: Book title announced twice

Field	Details

Page	Shop All Books
Success Criteria	2.4.4 – Link Purpose (In Context)
Conformance Level	A
Issue Summary	Book title is announced twice by screen readers.
Issue & Users Impacted	NVDA announces the book title once as part of the cover image alternative text (e.g., "Machines of Thought cover") and again as the visible book title. This causes redundant information, making navigation verbose and increasing cognitive load for screen reader users.
Source Code Example	html<br><a href="/book/123"><img src="cover.jpg" alt="Machines of Thought cover"></a><br><a href="/book/123">Machines of Thought</a>
Recommendation to Fix	If the image and title link to the same destination, wrap both within a single link or mark the image as decorative (alt="") when the adjacent text already provides the book title. This prevents duplicate announcements by screen readers.



---

Issue 2: Crossed-out (original) price announced

Field	Details

Page	Shop All Books
Success Criteria	1.3.1 – Info and Relationships
Conformance Level	A
Issue Summary	Original strikethrough price is announced without context by screen readers.
Issue & Users Impacted	NVDA announces both the current price and the crossed-out original price (e.g., "$12.99 $18.00") without indicating that the second value is the previous price. Screen reader users may not understand which price is current and which is discounted, leading to confusion.
Source Code Example	html<br><span>$12.99</span><br><del>$18.00</del>
Recommendation to Fix	Provide accessible context for both prices. For example, expose them as "Current price: $12.99. Original price: $18.00." Alternatively, hide the decorative strikethrough styling from assistive technologies and provide an accessible label that clearly identifies the current and original prices.


Note

If the old price is intentionally provided to users (to show a discount), do not hide it from screen readers. Instead, ensure it is announced with context such as "Original price $18.00" and "Current price $12.99", rather than just reading two numbers. This makes the pricing understandable for screen reader users.



If NVDA does not announce the validation errors after clicking Create Account, this is a WCAG 4.1.3 – Status Messages (Level AA) failure. If the errors are also not associated with the individual fields, it may additionally fail WCAG 3.3.1 – Error Identification.

Use this format in your Excel:

Field	Details

Page	Create Account
Success Criteria	4.1.3 – Status Messages
Conformance Level	AA
Issue Summary	Validation error messages are not announced to screen reader users after form submission.
Issue & Users Impacted	When the user activates the Create Account button with invalid or empty required fields, a validation summary is displayed visually (e.g., "Please fix the following: First name: Invalid, Last name: Invalid..."). However, NVDA does not announce the appearance of this message automatically because it is not exposed as a live region or status message. Screen reader users may not realize that the form submission failed or that validation errors have appeared, making it difficult to identify and correct the errors.
Source Code Example	html<br><div class="error-summary">Please fix the following: ...</div>
Recommendation to Fix	Ensure the validation summary is announced automatically by wrapping it in a live region such as role="alert" or aria-live="assertive". Additionally, associate each error message with its corresponding input using aria-describedby and set aria-invalid="true" on invalid fields. Example:<br><br>html<br><div role="alert" aria-live="assertive">Please fix the following: First name is required...</div>


If NVDA also does not announce the error when focus moves to each invalid field, report an additional issue for WCAG 3.3.1 – Error Identification.
