module.exports = {
default: {
require: ["step-definitions/.ts"],
requireModule: ["ts-node/register"],
paths: ["features/.feature"],
format: ["progress"]
}
};

Feature: Login functionality

Scenario: Successful login
Given user is on login page
When user enters valid username and password
Then user should be navigated to dashboard

Scenario: Invalid login
Given user is on login page
When user enters invalid credentials
Then error message should be displayed

Scenario Outline: Login with multiple credentials
Given user is on login page
When user enters "<username>" and "<password>"
Then login result should be "<result>"

Examples:
| username | password             | result  |
| tomsmith | SuperSecretPassword! | success |
| admin    | wrong123             | failure |

import { Page } from '@playwright/test';

export class LoginPage {
constructor(private page: Page) {}

async navigate() {
await this.page.goto(
'https://the-internet.herokuapp.com/login'
);
}

async login(username: string, password: string) {
await this.page.fill('#username', username);
await this.page.fill('#password', password);
await this.page.click('button[type="submit"]');
}

async getErrorMessage() {
return this.page.locator('#flash');
}
}

import { Given, When, Then } from '@cucumber/cucumber';
import { chromium, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';

let browser: any;
let page: any;
let loginPage: LoginPage;

Given('user is on login page', async () => {
browser = await chromium.launch({ headless: false });
page = await browser.newPage();

loginPage = new LoginPage(page);
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
await browser.close();
});

Then('error message should be displayed', async () => {
await expect(
loginPage.getErrorMessage()
).resolves.toBeTruthy();

await browser.close();
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
await expect(
loginPage.getErrorMessage()
).resolves.toBeTruthy();
}

await browser.close();

}
);
