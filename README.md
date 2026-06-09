Cart
import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';
import { ProductsPage } from '../pages/ProductsPage';
import { CartPage } from '../pages/CartPage';

test('TC_007 Remove product from cart @cart', async ({ page }) => {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await productsPage.removeBackpack();

    await expect(
        page.locator('.shopping_cart_badge')
    ).toHaveCount(0);

});

test('TC_013 Continue Shopping @cart', async ({ page }) => {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);
    const cartPage = new CartPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await productsPage.goToCart();

    await cartPage.continueShopping();

    await expect(page)
        .toHaveURL(/inventory.html/);

});


Checkout 
import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';
import { ProductsPage } from '../pages/ProductsPage';
import { CartPage } from '../pages/CartPage';
import { CheckoutPage } from '../pages/CheckoutPage';

async function loginAndReachCheckout(page: any) {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);
    const cartPage = new CartPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await productsPage.goToCart();

    await cartPage.checkout();
}

// TC_010
test('TC_010 Valid checkout @checkout', async ({ page }) => {

    const checkoutPage = new CheckoutPage(page);

    await loginAndReachCheckout(page);

    await checkoutPage.fillDetails(
        'Sayee',
        'Kokate',
        '400001'
    );

    await checkoutPage.continueCheckout();

    await expect(page)
        .toHaveURL(/checkout-step-two/);

});

// TC_011
test('TC_011 Checkout with missing first name @negative', async ({ page }) => {

    const checkoutPage = new CheckoutPage(page);

    await loginAndReachCheckout(page);

    await checkoutPage.fillDetails(
        '',
        'Kokate',
        '400001'
    );

    await checkoutPage.continueCheckout();

    await checkoutPage.verifyValidationMessage(
        'First Name is required'
    );

});

// TC_012
test('TC_012 Checkout with missing postal code @negative', async ({ page }) => {

    const checkoutPage = new CheckoutPage(page);

    await loginAndReachCheckout(page);

    await checkoutPage.fillDetails(
        'Sayee',
        'Kokate',
        ''
    );

    await checkoutPage.continueCheckout();

    await checkoutPage.verifyValidationMessage(
        'Postal Code is required'
    );

});



Login
import { test, expect } from '@playwright/test';
import { users } from '../test-cases/users';
import { LoginPage } from '../pages/LoginPage';

// TC_001
test('TC_001 Login page should load @smoke', async ({ page }) => {

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await expect(page).toHaveTitle(/Swag Labs/);

});

// TC_002
test('TC_002 Valid user should login @smoke', async ({ page }) => {

    const standardUser = users.find(
        user => user.type === 'standard'
    );

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await loginPage.login(
        standardUser!.username,
        standardUser!.password
    );

    await expect(page).toHaveURL(/inventory/);

});

// TC_003
test('TC_003 Invalid password should show error @negative', async ({ page }) => {

    const standardUser = users.find(
        user => user.type === 'standard'
    );

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await loginPage.login(
        standardUser!.username,
        'wrongpassword'
    );

    await loginPage.verifyErrorMessage(
        'Username and password do not match'
    );

});

// TC_004
test('TC_004 Locked user should not login @negative', async ({ page }) => {

    const lockedUser = users.find(
        user => user.type === 'locked'
    );

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await loginPage.login(
        lockedUser!.username,
        lockedUser!.password
    );

    await loginPage.verifyErrorMessage(
        'locked out'
    );

});




Product 
import { test, expect } from '@playwright/test';
import { LoginPage } from '../pages/LoginPage';
import { ProductsPage } from '../pages/ProductPage';

test('TC_005 Product list visible @regression', async ({ page }) => {

    const loginPage = new LoginPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await expect(
        page.locator('.inventory_item')
    ).toHaveCount(6);

});

test('TC_006 Add product to cart @cart', async ({ page }) => {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await productsPage.verifyCartCount('1');

});

test('TC_008 Add multiple products @cart', async ({ page }) => {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await page
        .locator('#add-to-cart-sauce-labs-bike-light')
        .click();

    await productsPage.verifyCartCount('2');

});

test('TC_009 Verify products in cart @cart', async ({ page }) => {

    const loginPage = new LoginPage(page);
    const productsPage = new ProductsPage(page);

    await loginPage.goto();

    await loginPage.login(
        'standard_user',
        'secret_sauce'
    );

    await productsPage.addBackpack();

    await productsPage.goToCart();

    await expect(
        page.getByText('Sauce Labs Backpack')
    ).toBeVisible();

});
