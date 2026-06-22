Scenario: Verify error message visibility
  Given user is on login page
  When user enters invalid credentials
  Then error message should be displayed

Scenario: Successful logout
  Given user is on login page
  When user enters valid username and password
  Then user should be navigated to dashboard
  When user clicks logout button
  Then user should be redirected to login page


When('user clicks logout button', async () => {
  await page.click('a[href="/logout"]');
});

Then('user should be redirected to login page', async () => {
  await expect(page).toHaveURL(/login/);
});
