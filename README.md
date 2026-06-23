import { Page } from '@playwright/test';

export class FormPage {
  constructor(private page: Page) {}

  async navigate() {
    await this.page.goto('https://demoqa.com/text-box');
  }


Feature: Form Submission

Scenario: Submit form with multiple fields

  Given user is on form page

  When user fills the form with following data:
    | field | value          |
    | name  | John           |
    | email | john@test.com  |

  Then form should be submitted successfully



import { Given, When, Then, DataTable } from '@cucumber/cucumber';
import { expect } from '@playwright/test';
import { FormPage } from '../pages/FormPage';

let formPage: FormPage;

Given('user is on form page', async function () {
  formPage = new FormPage(this.page);

  await formPage.navigate();
});

When(
  'user fills the form with following data:',
  async function (table: DataTable) {

    const data = table.rowsHash();

    await formPage.fillForm(
      data.name,
      data.email
    );

    await formPage.submitForm();
  }
);

Then('form should be submitted successfully', async function () {

  await expect(
    this.page.locator('#output')
  ).toBeVisible();

});

  async fillForm(name: string, email: string) {
    await this.page.fill('#userName', name);
    await this.page.fill('#userEmail', email);
  }

  async submitForm() {
    await this.page.click('#submit');
  }
}




"test": "cucumber-js --require-module ts-node/register --require step-definitions/*.ts --format json:reports/cucumber-report.json"
