import { test, expect } from '@playwright/test';

// TC_005 Mock Books API Response
test('TC_005 Mock Books API', async ({ page }) => {

    await page.route('**/BookStore/v1/Books', async route => {

        await route.fulfill({
            status: 200,
            contentType: 'application/json',
            body: JSON.stringify({
                books: [
                    {
                        isbn: '111',
                        title: 'Playwright Mock Book',
                        subTitle: 'Testing Book',
                        author: 'QA Team',
                        publish_date: '2025-01-01',
                        publisher: 'Playwright',
                        pages: 100,
                        description: 'Mocked response',
                        website: 'https://playwright.dev'
                    }
                ]
            })
        });

    });

    await page.goto('https://demoqa.com/books');

    await expect(
        page.getByText('Playwright Mock Book')
    ).toBeVisible();

});

// TC_006 Mock Empty Books Response
test('TC_006 Mock Empty Books Response', async ({ page }) => {

    await page.route('**/BookStore/v1/Books', async route => {

        await route.fulfill({
            status: 200,
            contentType: 'application/json',
            body: JSON.stringify({
                books: []
            })
        });

    });

    await page.goto('https://demoqa.com/books');

    await expect(page).toHaveURL(/books/);

});

// TC_007 Delay API Response
test('TC_007 Delay Books API Response', async ({ page }) => {

    await page.route('**/BookStore/v1/Books', async route => {

        await page.waitForTimeout(3000);

        await route.continue();

    });

    await page.goto('https://demoqa.com/books');

    await expect(page).toHaveTitle(/DEMOQA/);

});




import { test, expect } from '@playwright/test';

// TC_001 Verify New Tab button opens a new tab
test('TC_001 Verify New Tab button opens a new tab', async ({ page }) => {

    await page.goto('https://demoqa.com/browser-windows');

    const [newPage] = await Promise.all([
        page.context().waitForEvent('page'),
        page.locator('#tabButton').click()
    ]);

    await newPage.waitForLoadState();

    await expect(newPage).toHaveURL(/sample/);

});

// TC_002 Verify content of newly opened tab
test('TC_002 Verify content of newly opened tab', async ({ page }) => {

    await page.goto('https://demoqa.com/browser-windows');

    const [newPage] = await Promise.all([
        page.context().waitForEvent('page'),
        page.locator('#tabButton').click()
    ]);

    await newPage.waitForLoadState();

    await expect(
        newPage.locator('#sampleHeading')
    ).toHaveText('This is a sample page');

});

// TC_003 Close child tab and switch back to parent
test('TC_003 Close child tab and switch back', async ({ page }) => {

    await page.goto('https://demoqa.com/browser-windows');

    const [newPage] = await Promise.all([
        page.context().waitForEvent('page'),
        page.locator('#tabButton').click()
    ]);

    await newPage.close();

    await expect(
        page.locator('#tabButton')
    ).toBeVisible();

});

// TC_004 Verify New Window Message
test('TC_004 Verify New Window Message', async ({ page }) => {

    await page.goto('https://demoqa.com/browser-windows');

    const [newWindow] = await Promise.all([
        page.context().waitForEvent('page'),
        page.locator('#messageWindowButton').click()
    ]);

    await newWindow.waitForLoadState();

    const text = await newWindow
        .locator('body')
        .textContent();

    expect(text).toContain('Knowledge');

});
