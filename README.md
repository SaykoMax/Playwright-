import {
  Given,
  When,
  Then,
  Before,
  After,
  BeforeAll,
  AfterAll,
  setDefaultTimeout
} from '@cucumber/cucumber';

import {
  chromium,
  Browser,
  BrowserContext,
  Page,
  expect
} from '@playwright/test';

import { LoginPage } from '../pages/LoginPage';

setDefaultTimeout(120000);

let browser: Browser;
let context: BrowserContext;
let page: Page;
let loginPage: LoginPage;

BeforeAll(async () => {
  browser = await chromium.launch({
    headless: true
  });
});

AfterAll(async () => {
  await browser.close();
});

Before(async () => {
  context = await browser.newContext();
  page = await context.newPage();
  loginPage = new LoginPage(page);
});

After(async () => {
  await context.close();
});

Given('user is on login page', async function () {
  await loginPage.navigate();
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
  const errorLocator = loginPage.getErrorMessage();
  await expect(errorLocator).toBeVisible();
});

When(
  'user enters {string} and {string}',
  async (username: string, password: string) => {
    await loginPage.login(username, password);
  }
);

Then(
  'login result should be {string}',
  async (result: string) => {
    if (result === 'success') {
      await expect(page).toHaveURL(/secure/);
    } else {
      const errorLocator = loginPage.getErrorMessage();
      await expect(errorLocator).toBeVisible();
    }
  }
);



import { Page } from '@playwright/test';

export class LoginPage {
  constructor(private page: Page) {}

  async navigate() {
    await this.page.goto(
      'https://the-internet.herokuapp.com/login',
      {
        waitUntil: 'networkidle'
      }
    );
  }

  async login(
    username: string,
    password: string
  ) {
    await this.page.fill('#username', username);
    await this.page.fill('#password', password);
    await this.page.click('button[type="submit"]');
  }

  getErrorMessage() {
    return this.page.locator('#flash');
  }
}
