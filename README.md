This is a valid WCAG 4.1.3 – Status Messages (Level AA) issue because applying filters updates the displayed books, but screen reader users are not informed that the results have changed.

Use the following report format:

Field	Details

Page	Shop
Success Criteria	4.1.3 – Status Messages
Conformance Level	Level AA
Issue Summary	Applying filters updates the book results visually, but the change is not announced to assistive technologies.
Issue & Users Impacted	When users apply filters such as Genre, Format, or Tags (New, BestSeller, Classic, Award Winning), the product list updates immediately. However, no status message is announced to screen readers indicating the number of matching books or that the results have changed. Sighted users can visually recognize the updated content, whereas screen reader users receive no notification and may not realize that the filter has been applied successfully. This creates an inconsistent user experience and makes it difficult for users relying on assistive technologies to understand the outcome of their action.
Source Code Example	html<br><select aria-label="Filter by genre">...</select><br><select aria-label="Filter by format">...</select><br><button aria-pressed="false">BestSeller</button><br><!-- Product list updates but no aria-live region exists -->
Recommendation to Fix	Add an ARIA live region that announces the result of every filtering action. Whenever filters are applied, update the live region with a message such as "4 books found", "Results updated", or "No books match the selected filters." This ensures screen reader users receive the same feedback as sighted users without moving keyboard focus.
Sample Fix Code	html<br><div id="filter-status" role="status" aria-live="polite" aria-atomic="true"></div><br><script><br>function announceFilterResults(count) {<br>  const status = document.getElementById('filter-status');<br>  status.textContent = count === 0<br>    ? 'No books match the selected filters.'<br>    : `${count} book${count > 1 ? 's' : ''} found after applying filters.`;<br>}<br></script>


This is the appropriate WCAG criterion for the behavior shown in your screenshots, assuming NVDA or another screen reader does not announce the updated results after a filter is applied.
