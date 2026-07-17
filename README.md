Use the following Excel report format for WCAG 2.1.1 – Keyboard.

Field	Details

Page	Sign In
Success Criteria	2.1.1 – Keyboard
Conformance Level	A
Issue Summary	The Remember me checkbox and Sign in button are not keyboard accessible using the Tab key.
Issue & Users Impacted	When navigating the Sign In page using the Tab key, keyboard focus skips the Remember me checkbox and Sign in button, preventing users from accessing these controls without a mouse. As a result, keyboard-only users and screen reader users cannot interact with the checkbox or submit the sign-in form, making the authentication process inaccessible.
Source Code Example	html<br><input type="checkbox" id="remember-me" tabindex="-1"><br><button tabindex="-1">Sign in</button><br><br>or any implementation where these controls are removed from the keyboard tab order.
Recommendation to Fix	Ensure the Remember me checkbox and Sign in button are keyboard accessible and included in the natural tab order. Remove any tabindex="-1" or other code that prevents these controls from receiving keyboard focus. Verify that users can navigate to and activate all interactive elements using only the keyboard (Tab, Shift+Tab, Enter, and Space).
