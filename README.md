Setup and Execution Steps

1. Clone or download the project from GitHub.

2. Open the project in Visual Studio Code.

3. Install project dependencies using:
   
   npm install

4. Install Playwright browsers using:
   
   npx playwright install

5. Run all test cases using:
   
   npx playwright test

6. Run tests in headed mode using:
   
   npx playwright test --headed

7. View the HTML report using:
   
   npx playwright show-report

Project Structure

- tests → Contains test scripts
- pages → Contains Page Object Model (POM) files
- test-data → Contains test data
- utils → Contains reusable helper methods

The project is developed using Playwright with TypeScript and follows the Page Object Model (POM) design pattern.
Self Review Note

Through this assignment, I learned Playwright automation with TypeScript and gained hands-on experience in creating automated test cases for Login, Products, Cart, and Checkout modules. I implemented Page Object Model (POM), used TypeScript interfaces and types for test data, and created reusable methods to improve code quality. I also learned about Smoke, Regression, and Negative testing, report generation, and debugging failed test cases. This task helped me improve my automation and QA testing skills.
