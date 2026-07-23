Yes. If selecting Featured, Price: Low to High, or Price: High to Low updates the displayed books but NVDA does not announce that the sort has changed or that the results have been updated, then this is also a WCAG 4.1.3 – Status Messages (Level AA) issue.

Use the following report format:

Field	Details

Page	Shop
Success Criteria	4.1.3 – Status Messages
Conformance Level	Level AA
Issue Summary	Changing the sort option updates the book listing visually, but no status message is announced to screen reader users.
Issue & Users Impacted	When users select a sorting option such as Featured, Price: Low to High, or Price: High to Low, the product list is reordered immediately. However, no accessible status message is provided to notify screen reader users that the sorting operation has completed or that the displayed results have changed. Sighted users can recognize the updated order visually, whereas users relying on assistive technologies receive no feedback and may not know whether the selected sort option has been applied successfully.
Source Code Example	html<br><select aria-label="Sort"><br>  <option value="featured">Featured</option><br>  <option value="price-asc">Price: Low to High</option><br>  <option value="price-desc">Price: High to Low</option><br></select><br><!-- Product list updates visually but no aria-live region exists -->
Recommendation to Fix	Provide an ARIA live region that announces the result whenever the sorting option changes. The announcement should clearly indicate the selected sort order and that the results have been updated, for example, "Results sorted by Price: Low to High.", "Results sorted by Featured.", or "Results sorted by Price: High to Low." This ensures screen reader users receive the same feedback as sighted users without requiring a change in keyboard focus.
Sample Fix Code	html<br><select id="sort" aria-label="Sort"><br>  <option value="featured">Featured</option><br>  <option value="price-asc">Price: Low to High</option><br>  <option value="price-desc">Price: High to Low</option><br></select><br><div id="sort-status" role="status" aria-live="polite" aria-atomic="true"></div><br><script><br>document.getElementById('sort').addEventListener('change', function () {<br>  document.getElementById('sort-status').textContent = 'Results sorted by ' + this.options[this.selectedIndex].text + '.';<br>});<br></script>
