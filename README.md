import { test, expect } from '@playwright/test';

test('Element Not Found Failure', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  // Wrong locator
  await page.fill('#wrongUserName', 'Sayee');
});

test('Incorrect Locator Failure', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await page.click('#submit123');
});

test('Assertion Mismatch Failure', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await expect(page.locator('#wrongOutput')).toBeVisible();
});

test('Navigation Failure', async ({ page }) => {
  await page.goto('https://demoqa.com/invalid-page');

  await expect(page).toHaveURL(/text-box/);
});

test('Validation Failure', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await page.fill('#userName', 'Sayee');
  await page.fill('#userEmail', 'invalid123');

  await page.click('#submit');

  await expect(page.locator('#output')).toBeVisible();
});


import { test, expect } from '@playwright/test';

test('Page Load Timeout', async ({ page }) => {
  await page.goto(
    'https://demoqa.com/text-box',
    { timeout: 1 }
  );
});

test('Element Timeout', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await page.waitForSelector('#nonExistingElement');
});

test('Step Timeout', async ({ page }) => {
  test.setTimeout(5000);

  await page.goto('https://demoqa.com/text-box');

  await new Promise(resolve =>
    setTimeout(resolve, 10000)
  );
});

test('Locator Timeout', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await page.locator('#missingButton').click();
});

test('Assertion Timeout', async ({ page }) => {
  await page.goto('https://demoqa.com/text-box');

  await expect(page.locator('#missingElement')).toBeVisible({
    timeout: 5000,
  });
});
