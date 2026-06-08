test('TC_006 Add product to cart', async ({ page }) => {

    await page.goto('https://www.saucedemo.com/');

    await page.locator('#user-name').fill('standard_user');
    await page.locator('#password').fill('secret_sauce');
    await page.locator('#login-button').click();

    await page.locator('#add-to-cart-sauce-labs-backpack').click();

    await expect(page.locator('.shopping_cart_badge'))
        .toHaveText('1');
});
test('TC_007 Remove product from cart', async ({ page }) => {

    await page.goto('https://www.saucedemo.com/');

    await page.locator('#user-name').fill('standard_user');
    await page.locator('#password').fill('secret_sauce');
    await page.locator('#login-button').click();

    await page.locator('#add-to-cart-sauce-labs-backpack').click();

    await page.locator('#remove-sauce-labs-backpack').click();

    await expect(
        page.locator('.shopping_cart_badge')
    ).toHaveCount(0);
});
test('TC_008 Add multiple products', async ({ page }) => {

    await page.goto('https://www.saucedemo.com/');

    await page.locator('#user-name').fill('standard_user');
    await page.locator('#password').fill('secret_sauce');
    await page.locator('#login-button').click();

    await page.locator('#add-to-cart-sauce-labs-backpack').click();

    await page.locator('#add-to-cart-sauce-labs-bike-light').click();

    await expect(page.locator('.shopping_cart_badge'))
        .toHaveText('2');
});
test('TC_009 Verify products in cart', async ({ page }) => {

    await page.goto('https://www.saucedemo.com/');

    await page.locator('#user-name').fill('standard_user');
    await page.locator('#password').fill('secret_sauce');
    await page.locator('#login-button').click();

    await page.locator('#add-to-cart-sauce-labs-backpack').click();

    await page.locator('.shopping_cart_link').click();

    await expect(
        page.getByText('Sauce Labs Backpack')
    ).toBeVisible();
});





import { test, expect } from '@playwright/test';

const USERNAME = 'standard_user';
const PASSWORD = 'secret_sauce';

async function loginAndAddProduct(page: any) {

    await page.goto('https://www.saucedemo.com/');

    await page.locator('#user-name').fill(USERNAME);
    await page.locator('#password').fill(PASSWORD);
    await page.locator('#login-button').click();

    await page.locator('#add-to-cart-sauce-labs-backpack').click();

    await page.locator('.shopping_cart_link').click();

    await page.locator('#checkout').click();
}

// TC_010
test('TC_010 Valid checkout', async ({ page }) => {

    await loginAndAddProduct(page);

    await page.locator('#first-name').fill('Sayee');
    await page.locator('#last-name').fill('Kokate');
    await page.locator('#postal-code').fill('400001');

    await page.locator('#continue').click();

    await expect(page).toHaveURL(/checkout-step-two/);
});

// TC_011
test('TC_011 Checkout with missing first name', async ({ page }) => {

    await loginAndAddProduct(page);

    await page.locator('#last-name').fill('Kokate');
    await page.locator('#postal-code').fill('400001');

    await page.locator('#continue').click();

    await expect(page.locator('[data-test="error"]'))
        .toContainText('First Name is required');
});

// TC_012
test('TC_012 Checkout with missing postal code', async ({ page }) => {

    await loginAndAddProduct(page);

    await page.locator('#first-name').fill('Sayee');
    await page.locator('#last-name').fill('Kokate');

    await page.locator('#continue').click();

    await expect(page.locator('[data-test="error"]'))
        .toContainText('Postal Code is required');
});
