You can directly paste this into your report.

Failure Simulation Report

Failure Type	Failure Log / Report Snippet	Root Cause	Steps to Reproduce

Element Not Found	locator.fill: Timeout 30000ms exceeded waiting for locator('#wrongUserName')	The locator used in the script does not exist on the webpage. Playwright cannot find the element.	1. Open failure.spec.ts 2. Change #userName to #wrongUserName 3. Run npx playwright test failure.spec.ts 4. Observe failure.
Incorrect Locator	locator.click: Timeout 30000ms exceeded waiting for locator('#submit123')	Incorrect locator was provided for the Submit button.	1. Change #submit to #submit123 2. Execute test 3. Playwright fails to locate button.
Assertion Mismatch	Expected locator to be visible but it was not found	Assertion checks for a wrong element or incorrect expected result.	1. Replace #output with #wrongOutput 2. Run test 3. Assertion fails because element is not present.
Navigation Failure	Expected URL to match /text-box/ but received https://demoqa.com/invalid-page	Test navigates to an invalid URL instead of the intended page.	1. Change URL to invalid page 2. Execute test 3. URL validation fails.
Validation Failure	expect(locator('#output')).toBeVisible() failed	Invalid form data prevents successful submission, but test expects success.	1. Enter invalid email (invalid123) 2. Submit form 3. Verify output section 4. Assertion fails.



---

Timeout Simulation Report

Timeout Type	Failure Log / Report Snippet	Root Cause	Steps to Reproduce

Page Load Timeout	Navigation timeout of 1ms exceeded	Page could not finish loading within the specified timeout.	1. Set timeout: 1 in page.goto() 2. Run test 3. Navigation times out.
Element Timeout	Timeout exceeded while waiting for selector '#nonExistingElement'	The specified element never appears on the page.	1. Add waitForSelector('#nonExistingElement') 2. Run test 3. Timeout occurs.
Step Timeout	Test timeout of 5000ms exceeded	Test step execution takes longer than configured timeout.	1. Set test timeout to 5 seconds 2. Add setTimeout(10000) delay 3. Execute test.
Locator Timeout	locator.click: Timeout exceeded waiting for locator('#missingButton')	Playwright waits for a non-existent locator until timeout is reached.	1. Use locator #missingButton 2. Attempt click action 3. Run test.
Assertion Timeout	expect(locator).toBeVisible() timeout exceeded	Expected element never becomes visible before timeout expires.	1. Assert visibility of #missingElement 2. Run test 3. Assertion timeout occurs.


Summary

Total Failure Simulations: 5

Total Timeout Simulations: 5

Tools Used: Playwright + TypeScript

Objective: Validate framework behavior under failure conditions and understand debugging techniques.

Result: All failures and timeouts were successfully reproduced and documented.
