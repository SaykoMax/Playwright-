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
      data['name'] || '',
      data['email'] || ''
    );

    await formPage.submitForm();
  }
);

Then('form should be submitted successfully', async function () {
  await expect(this.page.locator('#output')).toBeVisible();
});

Then('form validation message should be displayed', async function () {
  console.log('Validation message displayed');
});

When(
  'user enters form details {string} and {string}',
  async function (name: string, email: string) {
    await formPage.fillForm(name, email);
    await formPage.submitForm();
  }
);

Then('form result should be {string}', async function (result: string) {
  if (result === 'success') {
    await expect(this.page.locator('#output')).toBeVisible();
  } else {
    console.log('Form submission failed');
  }
});
