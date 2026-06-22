When('user clicks logout button', async function (this: CustomWorld) {
await this.page.click('a[href="/logout"]');
});

Then('user should be redirected to login page', async function (this: CustomWorld) {
await expect(this.page).toHaveURL(/login/);
});

When('user clicks logout button', async function () {
await this.page.click('a[href="/logout"]');
});

Then('user should be redirected to login page', async function () {
await expect(this.page).toHaveURL(/login/);
});
