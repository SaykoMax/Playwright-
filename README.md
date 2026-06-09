TC_012 – Verify that the shopping cart badge count accurately reflects the number of selected products.

Steps:

1. Login to the application.
2. Add multiple products to the cart.
3. Observe the cart badge count.

Expected Result:
The cart badge count should match the total number of selected products.

---

TC_013 – Verify that a product can be removed successfully from the shopping cart from the Products page.

Steps:

1. Login to the application.
2. Add a product to the cart.
3. Click the Remove button for the selected product.

Expected Result:
The selected product should be removed from the cart.

---

TC_014 – Verify that the shopping cart badge disappears when all products are removed from the cart.

Steps:

1. Login to the application.
2. Add a product to the cart.
3. Remove the product from the cart.

Expected Result:
The shopping cart badge should disappear.

---

TC_015 – Verify that clicking the cart icon navigates the user to the Cart page.

Steps:

1. Login to the application.
2. Click the cart icon.

Expected Result:
The Cart page should open successfully.

---

TC_016 – Verify that all selected products are displayed correctly on the Cart page.

Steps:

1. Login to the application.
2. Add one or more products to the cart.
3. Open the Cart page.

Expected Result:
All selected products should be displayed on the Cart page.

---

TC_017 – Verify that a product can be removed from the Cart page.

Steps:

1. Login to the application.
2. Add a product to the cart.
3. Open the Cart page.
4. Click the Remove button.

Expected Result:
The selected product should be removed from the cart.

---

TC_018 – Verify that clicking Continue Shopping redirects the user back to the Products page.

Steps:

1. Login to the application.
2. Open the Cart page.
3. Click Continue Shopping.

Expected Result:
The user should be redirected to the Products page.

---

TC_019 – Verify that clicking the Checkout button redirects the user to the Checkout Information page.

Steps:

1. Login to the application.
2. Add a product to the cart.
3. Open the Cart page.
4. Click Checkout.

Expected Result:
The Checkout Information page should open.

---

TC_020 – Verify that checkout is successful when valid First Name, Last Name, and Postal Code are entered.

Steps:

1. Proceed to the Checkout Information page.
2. Enter valid First Name.
3. Enter valid Last Name.
4. Enter valid Postal Code.
5. Click Continue.

Expected Result:
The user should navigate to the Checkout Overview page.

---

TC_021 – Verify that an error message is displayed when the First Name field is left empty during checkout.

Steps:

1. Proceed to the Checkout Information page.
2. Leave the First Name field blank.
3. Enter Last Name and Postal Code.
4. Click Continue.

Expected Result:
A validation message indicating that First Name is required should be displayed.

---

TC_022 – Verify that an error message is displayed when the Last Name field is left empty during checkout.

Steps:

1. Proceed to the Checkout Information page.
2. Enter First Name.
3. Leave Last Name blank.
4. Enter Postal Code.
5. Click Continue.

Expected Result:
A validation message indicating that Last Name is required should be displayed.

---

TC_023 – Verify that an error message is displayed when the Postal Code field is left empty during checkout.

Steps:

1. Proceed to the Checkout Information page.
2. Enter First Name.
3. Enter Last Name.
4. Leave Postal Code blank.
5. Click Continue.

Expected Result:
A validation message indicating that Postal Code is required should be displayed.

---

TC_024 – Verify system behavior when special characters are entered in the First Name field during checkout.

Steps:

1. Proceed to the Checkout Information page.
2. Enter special characters in the First Name field.
3. Enter valid Last Name and Postal Code.
4. Click Continue.

Expected Result:
The application should handle the input according to business rules without crashing.

---

TC_025 – Verify system behavior when numeric values are entered in the First Name field during checkout.

Steps:

1. Proceed to the Checkout Information page.
2. Enter numeric values in the First Name field.
3. Enter valid Last Name and Postal Code.
4. Click Continue.

Expected Result:
The application should handle the input according to business rules.

---

TC_026 – Verify system behavior when Postal Code contains fewer than 6 digits.

Steps:

1. Proceed to the Checkout Information page.
2. Enter valid First Name and Last Name.
3. Enter a short Postal Code.
4. Click Continue.

Expected Result:
The application should process the input according to validation rules.

---

TC_027 – Verify system behavior when Postal Code contains more than 6 digits.

Steps:

1. Proceed to the Checkout Information page.
2. Enter valid First Name and Last Name.
3. Enter a long Postal Code.
4. Click Continue.

Expected Result:
The application should process the input according to validation rules.

---

TC_028 – Verify system behavior when alphanumeric values are entered in the Postal Code field.

Steps:

1. Proceed to the Checkout Information page.
2. Enter valid First Name and Last Name.
3. Enter an alphanumeric Postal Code.
4. Click Continue.

Expected Result:
The application should process the input according to validation rules.

---

TC_029 – Verify that the Checkout Overview page displays all selected products correctly before order placement.

Steps:

1. Add products to the cart.
2. Complete Checkout Information.
3. Proceed to the Checkout Overview page.

Expected Result:
All selected products should be displayed correctly.

---

TC_030 – Verify that item total, tax amount, and final total amount are calculated and displayed correctly.

Steps:

1. Add products to the cart.
2. Proceed to Checkout Overview.
3. Review price details.

Expected Result:
Item total, tax amount, and final total should be calculated accurately.

---

TC_031 – Verify that clicking the Cancel button during checkout redirects the user back to the Cart page.

Steps:

1. Open the Checkout Information page.
2. Click Cancel.

Expected Result:
The user should be redirected to the Cart page.

---

TC_032 – Verify that clicking the Finish button successfully places the order.

Steps:

1. Complete checkout information.
2. Proceed to Checkout Overview.
3. Click Finish.

Expected Result:
The order should be placed successfully.

---

TC_033 – Verify that the order confirmation message "Thank you for your order!" is displayed after successful checkout.

Steps:

1. Complete the order process.
2. Observe the confirmation page.

Expected Result:
The message "Thank you for your order!" should be displayed.

---

TC_034 – Verify that clicking the Back Home button redirects the user to the Products page.

Steps:

1. Complete an order.
2. Click Back Home.

Expected Result:
The user should be redirected to the Products page.

---

TC_035 – Verify that products can be sorted alphabetically by Name (A to Z).

Steps:

1. Login to the application.
2. Select the Name (A to Z) sorting option.

Expected Result:
Products should be displayed in ascending alphabetical order.

---

TC_036 – Verify that products can be sorted alphabetically by Name (Z to A).

Steps:

1. Login to the application.
2. Select the Name (Z to A) sorting option.

Expected Result:
Products should be displayed in descending alphabetical order.

---

TC_037 – Verify that products can be sorted by Price (Low to High).

Steps:

1. Login to the application.
2. Select the Price (Low to High) sorting option.

Expected Result:
Products should be displayed from the lowest price to the highest price.

---

TC_038 – Verify that products can be sorted by Price (High to Low).

Steps:

1. Login to the application.
2. Select the Price (High to Low) sorting option.

Expected Result:
Products should be displayed from the highest price to the lowest price.

---

TC_039 – Verify that the side navigation menu opens successfully when the menu icon is clicked.

Steps:

1. Login to the application.
2. Click the menu icon.

Expected Result:
The side navigation menu should open successfully.

---

TC_040 – Verify that the user can successfully log out using the Logout option from the side navigation menu.

Steps:

1. Login to the application.
2. Open the side navigation menu.
3. Click Logout.

Expected Result:
The user should be redirected to the Login page.
