import { test, expect } from '@playwright/test';

/*
Failure 1: Locator Failure
*/
test('Locator Failure Example', async ({ page }) => {
    await page.goto('https://demoqa.com');

    await page.locator('#wrongLocator').click();
});

/*
Failure 2: Assertion Failure
*/
test('Assertion Failure Example', async ({ page }) => {
    await page.goto('https://demoqa.com');

    await expect(page).toHaveTitle('Wrong Title');
});

/*
Failure 3: Visibility Failure
*/
test('Visibility Failure Example', async ({ page }) => {
    await page.goto('https://demoqa.com');

    await expect(
        page.locator('#hiddenElement')
    ).toBeVisible();
});

/*
Failure 4: Navigation Failure
*/
test('Navigation Failure Example', async ({ page }) => {
    await page.goto('https://invalid-demoqa-url.com');

    await expect(page).toHaveURL(/demoqa/);
});

/*
Failure 5: Timeout Failure
*/
test('Timeout Failure Example', async ({ page }) => {
    test.setTimeout(1000);

    await page.goto('https://demoqa.com');

    await page.waitForTimeout(5000);
});




import { test, expect } from '@playwright/test';

// TC_009 Test Timeout
test('Test Timeout Example', async ({ page }) => {

    test.setTimeout(1000);

    await page.goto('https://demoqa.com');

    await page.waitForTimeout(5000);
});


// TC_010 Expect Timeout
test('Expect Timeout Example', async ({ page }) => {

    await page.goto('https://demoqa.com');

    await expect(
        page.locator('#wrongLocator')
    ).toBeVisible({
        timeout: 1000
    });
});


// TC_011 Action Timeout
test('Action Timeout Example', async ({ page }) => {

    page.setDefaultTimeout(1000);

    await page.goto('https://demoqa.com');

    await page.locator('#wrongLocator').click();
});
