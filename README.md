import { Given, When, Then, Before, After } from '@cucumber/cucumber';
import { chromium, Browser, Page, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';

let browser: Browser;
let page: Page;
let loginPage: LoginPage;

Before({ timeout: 20000 }, async () => {
  browser = await chromium.launch({
    headless: false
  });

  page = await browser.newPage();
  loginPage = new LoginPage(page);
});

After(async () => {
  await browser.close();
});

Given('user is on login page', async () => {
  await page.goto(
    'https://the-internet.herokuapp.com/login',
    {
      waitUntil: 'domcontentloaded',
      timeout: 30000
    }
  );
});

When('user enters valid username and password', async () => {
  await loginPage.login(
    'tomsmith',
    'SuperSecretPassword!'
  );
});

When('user enters invalid credentials', async () => {
  await loginPage.login(
    'admin',
    'wrong123'
  );
});

Then('user should be navigated to dashboard', async () => {
  await expect(page).toHaveURL(/secure/);
});

Then('error message should be displayed', async () => {
  const errorLocator = await loginPage.getErrorMessage();
  await expect(errorLocator).toBeTruthy();
});

When(
  'user enters {string} and {string}',
  async (username, password) => {
    await loginPage.login(username, password);
  }
);

Then(
  'login result should be {string}',
  async (result) => {
    if (result === 'success') {
      await expect(page).toHaveURL(/secure/);
    } else {
      const errorLocator = await loginPage.getErrorMessage();
      await expect(errorLocator).toBeTruthy();
    }
  }
);
