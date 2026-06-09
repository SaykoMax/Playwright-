TC ID	Module	Detailed Test Scenario	Type	Priority	Test Steps	Expected Result

TC_001	Login	Verify that the SauceDemo login page loads successfully and displays Username field, Password field, Login button, and application logo.	Smoke	High	1. Open browser 2. Navigate to SauceDemo URL	Login page should load with all required controls visible
TC_002	Login	Verify that a user can successfully log in using valid credentials (standard_user / secret_sauce).	Smoke	High	1. Open SauceDemo 2. Enter valid username 3. Enter valid password 4. Click Login	User should be redirected to the Products page
TC_003	Login	Verify that an error message is displayed when an invalid username and invalid password are entered.	Negative	High	1. Enter invalid username 2. Enter invalid password 3. Click Login	Appropriate error message should be displayed
TC_004	Login	Verify that an error message is displayed when a valid username and incorrect password are entered.	Negative	High	1. Enter valid username 2. Enter invalid password 3. Click Login	Error message should be displayed
TC_005	Login	Verify that an error message is displayed when an invalid username and valid password are entered.	Negative	High	1. Enter invalid username 2. Enter valid password 3. Click Login	Error message should be displayed
TC_006	Login	Verify that a locked-out user cannot log in and receives the appropriate locked-out error message.	Negative	High	1. Enter locked user credentials 2. Click Login	Locked user error should be displayed
TC_007	Products	Verify that all available products are displayed after successful login.	Smoke	High	1. Login successfully 2. Observe product listing page	All products should be displayed
TC_008	Products	Verify that product name, description, price, and Add to Cart button are visible for every product displayed on the Products page.	Regression	Medium	1. Login 2. View products page	Product details should be visible
TC_009	Cart	Verify that a selected product can be added to the shopping cart successfully.	Regression	High	1. Login 2. Click Add to Cart on a product	Product should be added to cart
TC_010	Cart	Verify that the shopping cart badge count increases after adding a product to the cart.	Regression	High	1. Add one product to cart	Cart badge count should become 1
TC_011	Cart	Verify that multiple products can be added to the shopping cart successfully.	Regression	Medium	1. Add multiple products	All selected products should be added
TC_012	Cart	Verify that the shopping cart badge count accurately reflects the number of selected products.	Regression	Medium	1. Add multiple products	Badge count should match selected items
TC_013	Cart	Verify that a product can be removed successfully from the shopping cart from the Products page.	Regression	Medium	1. Add product 2. Click Remove	Product should be removed
TC_014	Cart	Verify that the shopping cart badge disappears when all products are removed from the cart.	Regression	Medium	1. Add product 2. Remove product	Cart badge should disappear
TC_015	Cart	Verify that clicking the cart icon navigates the user to the Cart page.	Smoke	High	1. Login 2. Click cart icon	Cart page should open
TC_016	Cart	Verify that all selected products are displayed correctly on the Cart page.	Regression	High	1. Add product 2. Open cart	Added products should be displayed
TC_017	Cart	Verify that a product can be removed from the Cart page.	Regression	Medium	1. Open cart 2. Remove product	Product should be removed
TC_018	Cart	Verify that clicking Continue Shopping redirects the user back to the Products page.	Regression	Low	1. Open cart 2. Click Continue Shopping	User should return to Products page
TC_019	Checkout	Verify that clicking the Checkout button redirects the user to the Checkout Information page.	Smoke	High	1. Open cart 2. Click Checkout	Checkout Information page should open
TC_020	Checkout	Verify that checkout is successful when valid First Name, Last Name, and Postal Code are entered.	Smoke	High	1. Enter valid checkout details 2. Click Continue	User should reach Checkout Overview page
TC_021	Checkout	Verify that an error message is displayed when the First Name field is left empty during checkout.	Negative	High	1. Leave First Name blank 2. Continue checkout	Validation message should appear
TC_022	Checkout	Verify that an error message is displayed when the Last Name field is left empty during checkout.	Negative	High	1. Leave Last Name blank 2. Continue checkout	Validation message should appear
TC_023	Checkout	Verify that an error message is displayed when the Postal Code field is left empty during checkout.	Negative	High	1. Leave Postal Code blank 2. Continue checkout	Validation message should appear
TC_024	Checkout	Verify that checkout information is accepted when special characters are entered in the First Name field.	Negative	Medium	1. Enter special characters in First Name 2. Continue	System behavior should be validated
TC_025	Checkout	Verify that checkout information is accepted when numeric values are entered in the First Name field.	Negative	Medium	1. Enter numeric values in First Name 2. Continue	System behavior should be validated
TC_026	Checkout	Verify that Postal Code accepts fewer than 6 digits.	Negative	Medium	1. Enter short Postal Code 2. Continue	System behavior should be validated
TC_027	Checkout	Verify that Postal Code accepts more than 6 digits.	Negative	Medium	1. Enter long Postal Code 2. Continue	System behavior should be validated
TC_028	Checkout	Verify that Postal Code accepts alphanumeric values.	Negative	Medium	1. Enter alphanumeric Postal Code 2. Continue	System behavior should be validated
TC_029	Checkout	Verify that the Checkout Overview page displays all selected products correctly before order placement.	Regression	High	1. Proceed to overview page	Selected products should be displayed
TC_030	Checkout	Verify that item total, tax amount, and final total amount are calculated and displayed correctly.	Regression	High	1. Proceed to overview page	Totals should be calculated correctly
TC_031	Checkout	Verify that clicking the Cancel button during checkout redirects the user back to the Cart page.	Regression	Medium	1. Open checkout page 2. Click Cancel	User should return to Cart page
TC_032	Order Confirmation	Verify that clicking the Finish button successfully places the order.	Smoke	High	1. Complete checkout 2. Click Finish	Order should be placed successfully
TC_033	Order Confirmation	Verify that the order confirmation message "Thank you for your order!" is displayed after successful checkout.	Smoke	High	1. Complete order	Confirmation message should appear
TC_034	Order Confirmation	Verify that clicking the Back Home button redirects the user to the Products page.	Regression	Low	1. Complete order 2. Click Back Home	Products page should open
TC_035	Product Sorting	Verify that products can be sorted alphabetically by Name (A to Z).	Regression	Medium	1. Select Name (A-Z) sorting	Products should appear in ascending order
TC_036	Product Sorting	Verify that products can be sorted alphabetically by Name (Z to A).	Regression	Medium	1. Select Name (Z-A) sorting	Products should appear in descending order
TC_037	Product Sorting	Verify that products can be sorted by Price (Low to High).	Regression	Medium	1. Select Low to High sorting	Products should be sorted by lowest price first
TC_038	Product Sorting	Verify that products can be sorted by Price (High to Low).	Regression	Medium	1. Select High to Low sorting	Products should be sorted by highest price first
TC_039	Navigation/Menu	Verify that the side navigation menu opens successfully when the menu icon is clicked.	Regression	Low	1. Click menu icon	Side menu should open
TC_040	Navigation/Menu	Verify that the user can successfully log out using the Logout option from the side navigation menu.	Smoke	High	1. Open menu 2. Click Logout	User should return to login page
