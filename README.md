Yes, this is a valid accessibility issue.

From your screenshots:

The page displays "Enter the 6-digit code we sent to sc@fc.com" after the email is submitted.

NVDA does not announce this updated instruction when the page changes.

This means the newly displayed status/instruction is not being exposed to assistive technologies.


Success Criterion

WCAG 4.1.3 – Status Messages (Level AA)

Field	Details

Success Criterion	4.1.3 – Status Messages (Level AA)
Issue Summary	OTP instruction message is not announced by screen readers after the Send Code action.
Issue & User Impact	After activating Send Code, the page updates to display "Enter the 6-digit code we sent to sc@fc.com". This change is visible but is not announced by screen readers. Users relying on assistive technologies may not realize that the verification step has started or know which email address received the code, making the authentication process difficult to complete.
Recommendation	Ensure the OTP instruction is announced automatically using an ARIA live region or move keyboard focus to the newly displayed content.
Sample Fix Code	```html


<div id="otp-message" role="status" aria-live="polite">
  Enter the 6-digit code we sent to sc@fc.com
</div>
``` |Alternative (if immediate announcement is required):

<div id="otp-message" role="alert">
  Enter the 6-digit code we sent to sc@fc.com
</div>

Why this is happening

From the code you shared, the page contains only regular <div> and <p> elements for the updated content. They are not inside an aria-live region and focus is not moved to the new content, so NVDA has no reason to announce it automatically.

This is best reported as a WCAG 4.1.3 – Status Messages failure.




If the Orders page content is loaded dynamically and NVDA does not announce that the page has changed (e.g., it doesn't read "Your orders" or indicate that the orders have loaded), you can report it under WCAG 4.1.3 – Status Messages (Level AA).

Field	Details

Success Criterion	WCAG 4.1.3 – Status Messages (Level AA)
Issue Summary	Orders page content is not announced to screen reader users after navigation.
Issue & User Impact	After navigating to the Orders page, the application dynamically updates the displayed content, but no status message is announced to screen readers. Users relying on assistive technologies are not informed that the Orders page has loaded and may not realize new content is available, causing confusion and reducing usability.
Recommendation	Announce the page update using an ARIA live region or move focus to the page heading (<h1>) so the new content is automatically announced by screen readers.
Sample Fix Code	```html


<h1 id="orders-heading" tabindex="-1">Your orders</h1><div role="status" aria-live="polite">
  Orders page loaded. 1 order found.
</div><script>
document.getElementById('orders-heading').focus();
</script>This format is suitable if your application is an SPA (React, Angular, Vue, etc.) where the page changes without a full page reload and NVDA does not announce the updated content.




This is also a WCAG 4.1.3 – Status Messages (Level AA) issue because the cart count changes dynamically (e.g., from 4 to 5 items) but the change is not announced to screen reader users.

Field	Details

Success Criterion	WCAG 4.1.3 – Status Messages (Level AA)
Issue Summary	Updated cart item count is not announced to screen reader users after adding a product to the cart.
Issue & User Impact	When a user activates the Add to cart button on the Product Details page, a visual toast message ("Northern Lights Atlas added to cart") appears and the cart badge updates from 4 to 5 items. However, the updated cart count is not announced by screen readers. Users relying on assistive technologies may not know that the cart quantity has changed, reducing confidence that the action was completed successfully.
Recommendation	Use an ARIA live region (role="status" or aria-live="polite") to announce the updated cart count whenever the badge value changes. The announcement should include both the product addition and the new total number of items in the cart.
Sample Fix Code	```html


<!-- Hidden live region --><div id="cart-status"
     role="status"
     aria-live="polite"
     aria-atomic="true"
     class="sr-only">
</div><!-- Cart badge --><a href="/cart" aria-label="Cart, 5 items">
  <span id="cart-count">5</span>
</a><script>
function updateCart(productName, count) {
  document.getElementById("cart-count").textContent = count;
  document.querySelector('a[href="/cart"]')
    .setAttribute("aria-label", `Cart, ${count} items`);

  document.getElementById("cart-status").textContent =
    `${productName} added to cart. Cart now contains ${count} items.`;
}
</script>**Expected NVDA announcement:**
> "Northern Lights Atlas added to cart. Cart now contains 5 items."

This ensures screen reader users receive the same feedback that sighted users get from the visual cart badge update.




This is a semantic structure issue and should be reported under WCAG 1.3.1 – Info and Relationships (Level A) because tabular data is created using generic <div> elements instead of semantic table markup.

Field	Details

Success Criterion	WCAG 1.3.1 – Info and Relationships (Level A)
Issue Summary	Orders data is visually presented as a table but is built using <div> elements instead of semantic table markup.
Issue & User Impact	The Orders page displays structured tabular information such as Order ID, Placed On, Items, Total, Product Details, Payment, and Shipping. However, the content is constructed using generic <div> elements rather than semantic <table>, <thead>, <tbody>, <tr>, <th>, and <td> elements. As a result, screen readers cannot identify row and column relationships, announce column headers, or allow users to efficiently navigate the data using table navigation commands. This makes the order details difficult to understand for users of assistive technologies.
Recommendation	Use semantic HTML table elements for tabular data. Define column headers using <th> elements with the appropriate scope attribute and place data within <td> cells. This enables assistive technologies to correctly interpret and announce the table structure.
Sample Fix Code	```html


<table>
  <thead>
    <tr>
      <th scope="col">Order</th>
      <th scope="col">Placed On</th>
      <th scope="col">Items</th>
      <th scope="col">Total</th>
    </tr>
  </thead>  <tbody>
    <tr>
      <td>#BG-24037</td>
      <td>Jul 16, 2026, 05:49 PM</td>
      <td>2</td>
      <td>$47.98</td>
    </tr><tr>
  <td>Northern Lights Atlas</td>
  <td>Henrik Sól</td>
  <td>Qty: 1</td>
  <td>$34.00</td>
</tr>

  </tbody>
</table>
``` |Expected Behavior:

Screen readers announce "Table with X rows and Y columns."

Users can navigate by rows and columns using screen reader table commands.

Column headers (Order, Placed On, Items, Total) are announced along with each corresponding cell, providing the correct context for the order information.




This should be reported under WCAG 4.1.2 – Name, Role, Value (Level A) because the custom checkbox is built with a <div> instead of a native checkbox, making it inaccessible to keyboard and assistive technology users.

Field	Details

Success Criterion	WCAG 4.1.2 – Name, Role, Value (Level A)
Issue Summary	"Remember me" checkbox is implemented using a <div> instead of a native checkbox, making it inaccessible.
Issue & User Impact	The Remember me option is created using a generic <div> element rather than a native <input type="checkbox">. As a result, the control is not keyboard accessible, cannot receive focus, does not respond to the Spacebar key, and its checked/unchecked state is not conveyed to assistive technologies. Screen reader and keyboard-only users may be unable to interact with or determine the state of the checkbox.
Recommendation	Use a native <input type="checkbox"> with an associated <label>. If a custom checkbox is required, implement role="checkbox", tabindex="0", aria-checked, and support keyboard interaction using the Spacebar. Native HTML controls are strongly recommended.
Sample Fix Code	```html
<label for="remember-me">	
<input	


type="checkbox"
id="remember-me"
name="remember-me">

Remember me </label>

**If a custom control is unavoidable:**
```html
<div
  role="checkbox"
  tabindex="0"
  aria-checked="false"
  id="rememberMe">
  Remember me
</div>

<script>
const checkbox = document.getElementById("rememberMe");

checkbox.addEventListener("keydown", (e) => {
  if (e.code === "Space") {
    e.preventDefault();
    const checked =
      checkbox.getAttribute("aria-checked") === "true";
    checkbox.setAttribute("aria-checked", !checked);
  }
});
</script>
``` |

**Expected Behavior:**
- The **Remember me** checkbox receives keyboard focus.
- Pressing the **Spacebar** toggles the checkbox state.
- Screen readers announce the control as **"Remember me, checkbox, checked/not checked."**


