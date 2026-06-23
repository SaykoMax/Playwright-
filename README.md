Playwright BDD Automation Framework

About This Project

This project was created as part of a QA Automation assignment using Playwright, TypeScript, and Cucumber BDD. The main objective was to automate user workflows using industry-standard automation practices such as Page Object Model (POM), reusable components, hooks, reporting, and debugging techniques.

The project covers automation of two modules:

- Login Functionality
- Form Submission Functionality

It also includes report generation, failure simulation, and timeout handling for debugging practice.

---

Technologies Used

- Playwright
- TypeScript
- Cucumber BDD
- Node.js
- Multiple Cucumber HTML Reporter

---

Project Structure

bdd-playwright/
│
├── features/
│   ├── login.feature
│   └── form.feature
│
├── step-definitions/
│   ├── login.steps.ts
│   ├── form.steps.ts
│   └── hooks.ts
│
├── pages/
│   ├── LoginPage.ts
│   └── FormPage.ts
│
├── reports/
│
├── generate-report.js
├── package.json
└── tsconfig.json

---

Framework Design

The framework follows the Page Object Model design pattern.

LoginPage

Contains all login-related locators and actions such as:

- Enter username
- Enter password
- Click login
- Validate login results

FormPage

Contains all form-related actions such as:

- Enter name
- Enter email
- Submit form
- Validate submission

Using POM helps keep locators separate from test logic and makes maintenance easier.

---

Hooks Implementation

Hooks are implemented using Cucumber.

Before Hook

Executed before every scenario.

Responsibilities:

- Launch browser
- Create browser context
- Open a new page

After Hook

Executed after every scenario.

Responsibilities:

- Close page
- Close browser
- Clean up resources

This ensures each test runs independently.

---

Login Module

The following scenarios were automated:

1. Successful login with valid credentials
2. Login with invalid credentials
3. Login using multiple credential combinations
4. Error message visibility validation
5. Logout functionality
6. Redirection to login page after logout

Scenario Outline was used for data-driven login testing.

---

Form Module

The following scenarios were automated:

1. Successful form submission
2. Form submission with empty name
3. Form submission with invalid email
4. Multiple form submissions using Scenario Outline

DataTable was used to pass form input data dynamically.

Example:

When user fills the form with following data:
| name  | Sayee          |
| email | sayee@test.com |

---

Reporting

Cucumber HTML Report

After test execution:

npm test

Generate HTML report:

node generate-report.js

Report location:

reports/html-report/index.html

---

Failure Simulation

For debugging practice, different failure scenarios were created:

- Element Not Found
- Incorrect Locator
- Assertion Mismatch
- Navigation Failure
- Validation Failure

For each failure, root cause analysis and reproduction steps were documented.

---

Timeout Simulation

The following timeout scenarios were explored:

- Page Load Timeout
- Element Timeout
- Step Timeout

This helped in understanding how Playwright behaves when operations exceed expected execution time.

---

Key Concepts Demonstrated

- Page Object Model (POM)
- Hooks (Before and After)
- DataTable Usage
- Scenario Outline
- Reusable Page Classes
- Separation of Concerns
- HTML Reporting
- Debugging and Failure Analysis

---

How to Run the Project

Install dependencies:

npm install

Execute tests:

npm test

Generate report:

node generate-report.js

Open generated report:

reports/html-report/index.html

---

Learning Outcomes

Through this assignment, I gained hands-on experience in:

- Building a BDD automation framework from scratch
- Writing reusable Playwright automation code
- Implementing Page Object Model
- Working with Cucumber DataTables and Scenario Outlines
- Generating execution reports
- Analyzing failures and debugging test cases
- Organizing automation projects using best practices

---

Author

Sayee Kokate

BE – Artificial Intelligence & Data Science

QA Automation Assignment – Playwright + TypeScript + Cucumber BDD
