Based on the screenshot, WAVE reports "Missing form label" for a form control on the New Password / Reset Password page. This maps to WCAG 1.3.1 – Info and Relationships (Level A) and WCAG 3.3.2 – Labels or Instructions (Level A).

Use this Excel report format:

Field	Details

Page	New Password / Reset Password
Success Criteria	3.3.2 – Labels or Instructions
Conformance Level	A
Issue Summary	A form control on the New Password page does not have an associated accessible label.
Issue & Users Impacted	One of the form controls on the New Password page does not have a programmatically associated label. As a result, screen readers may announce the control without describing its purpose, making it difficult for users with visual impairments to understand what information is required. Keyboard and assistive technology users may be unable to complete the form accurately.
Source Code Example	html<br><input type="password" id="newPassword"><br><!-- Missing associated <label> or aria-label -->
Recommendation to Fix	Associate every form control with a visible <label> using the for attribute or provide an accessible name using aria-label or aria-labelledby. For example:<br><br>html<br><label for="newPassword">New Password</label><br><input type="password" id="newPassword">


You can also report:

Success Criteria: 1.3.1 – Info and Relationships (Level A)


This criterion applies because the relationship between the form control and its label is not programmatically exposed to assistive technologies. If you're reporting only one criterion, 3.3.2 – Labels or Instructions is the most direct fit for this issue.
