If the star icons are intentionally decorative (aria-hidden="true") and NVDA announces "4.5" (and ideally the review count), then that alone is not an accessibility issue. Decorative stars are correctly hidden from assistive technologies.

However, if NVDA only announces "4.5" and does not convey that it is a rating, then users may not understand what the number represents. That becomes a Name, Role, Value issue.

You can report it as follows:

Field	Details

Page	Book Details
Success Criteria	4.1.2 – Name, Role, Value
Conformance Level	A
Issue Summary	Rating information is not announced with sufficient context to screen reader users.
Issue & Users Impacted	The visual star icons are hidden from assistive technologies using aria-hidden="true", which is appropriate for decorative content. However, NVDA announces only "4.5" without identifying it as the book's rating (e.g., "Rating 4.5 out of 5"). Screen reader users may not understand what the numeric value represents, reducing the clarity of the information.
Source Code Example	html<br><span aria-hidden="true">★★★★★</span><br><span>4.5</span><br><span>(845 reviews)</span>
Recommendation to Fix	Provide an accessible name for the rating, such as "Rating: 4.5 out of 5 stars, based on 845 reviews." This can be achieved using aria-label, visually hidden text, or by ensuring the text exposed to assistive technologies includes the context. Example:<br><br>html<br><div aria-label="Rating 4.5 out of 5 stars, based on 845 reviews">★★★★★ <span aria-hidden="true">4.5</span></div>


Important: If NVDA actually announces "4.5 out of 5, 845 reviews" or "Rating 4.5 out of 5", then this passes WCAG and should not be reported. The issue only exists if NVDA truly announces just "4.5" with no context.
