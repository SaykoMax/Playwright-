# Playwright-prodicts
import { test, expect } from '@playwright/test';

const USERNAME = 'standard_user';
const PASSWORD = 'secret_sauce';

async function login(page: any) {
  await page.goto('https://www.saucedemo.com/');
  await page.locator('#user-name').fill(USERNAME);
  await page.locator('#password').fill(PASSWORD);
  await page.locator('#login-button').click();
}

// TC_005
test('TC_005 Product list should be visible after login', async ({ page }) => {
  await login(page);

  await expect(page.locator('.inventory_item')).toHaveCount(6);
});

// TC_006
test('TC_006 Add one product to cart', async ({ page }) => {
  await login(page);

  await page.locator('#add-to-cart-sauce-labs-backpack').click();

  await expect(page.locator('.shopping_cart_badge')).toHaveText('1');
});

// TC_007
test('TC_007 Remove product from cart', async ({ page }) => {
  await login(page);

  await page.locator('#add-to-cart-sauce-labs-backpack').click();
  await page.locator('#remove-sauce-labs-backpack').click();

  await expect(page.locator('.shopping_cart_badge')).toHaveCount(0);
});

// TC_008
test('TC_008 Add multiple products to cart', async ({ page }) => {
  await login(page);

  await page.locator('#add-to-cart-sauce-labs-backpack').click();
  await page.locator('#add-to-cart-sauce-labs-bike-light').click();

  await expect(page.locator('.shopping_cart_badge')).toHaveText('2');
});

// TC_009
test('TC_009 Cart page should show selected products', async ({ page }) => {
  await login(page);

  await page.locator('#add-to-cart-sauce-labs-backpack').click();
  await page.locator('#add-to-cart-sauce-labs-bike-light').click();

  await page.locator('.shopping_cart_link').click();

  await expect(page.getByText('Sauce Labs Backpack')).toBeVisible();
  await expect(page.getByText('Sauce Labs Bike Light')).toBeVisible();
});
