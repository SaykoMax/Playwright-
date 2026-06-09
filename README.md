import { Page, Locator, expect } from '@playwright/test';

export class LoginPage {

    readonly page: Page;
    readonly usernameInput: Locator;
    readonly passwordInput: Locator;
    readonly loginButton: Locator;
    readonly errorMessage: Locator;

    constructor(page: Page) {
        this.page = page;

        this.usernameInput = page.locator('#user-name');
        this.passwordInput = page.locator('#password');
        this.loginButton = page.locator('#login-button');
        this.errorMessage = page.locator('[data-test="error"]');
    }

    async goto() {
        await this.page.goto('https://www.saucedemo.com/');
    }

    async login(username: string, password: string) {
        await this.usernameInput.fill(username);
        await this.passwordInput.fill(password);
        await this.loginButton.click();
    }

    async verifyErrorMessage(message: string) {
        await expect(this.errorMessage)
            .toContainText(message);
    }
}




import { Page, expect } from '@playwright/test';

export class ProductsPage {

    constructor(private page: Page) {}

    async addBackpack() {
        await this.page
            .locator('#add-to-cart-sauce-labs-backpack')
            .click();
    }

    async removeBackpack() {
        await this.page
            .locator('#remove-sauce-labs-backpack')
            .click();
    }

    async verifyCartCount(count: string) {
        await expect(
            this.page.locator('.shopping_cart_badge')
        ).toHaveText(count);
    }

    async goToCart() {
        await this.page.locator('.shopping_cart_link').click();
    }
}




import { Page, expect } from '@playwright/test';

export class CartPage {

    constructor(private page: Page) {}

    async verifyProduct(product: string) {
        await expect(
            this.page.getByText(product)
        ).toBeVisible();
    }

    async checkout() {
        await this.page.locator('#checkout').click();
    }
}




import { Page, expect } from '@playwright/test';

export class CheckoutPage {

    constructor(private page: Page) {}

    async fillDetails(
        firstName: string,
        lastName: string,
        postalCode: string
    ) {

        await this.page.fill('#first-name', firstName);
        await this.page.fill('#last-name', lastName);
        await this.page.fill('#postal-code', postalCode);
    }

    async continueCheckout() {
        await this.page.locator('#continue').click();
    }

    async verifyValidationMessage(message: string) {
        await expect(
            this.page.locator('[data-test="error"]')
        ).toContainText(message);
    }
}




import { Page } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';

export async function loginAsStandardUser(page: Page) {

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );
}
