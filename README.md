Playwright Automation Training Task - Day 1 & Day 2

Overview

This project was completed as part of Playwright Automation Training. The objective was to learn advanced Playwright concepts such as Browser Window handling, Network Mocking, Fixtures, Reporting, Debugging, and Timeout handling.

The project is implemented using Playwright with TypeScript and follows reusable automation practices.

---

Technology Stack

- Playwright
- TypeScript
- Node.js
- Visual Studio Code

---

Project Setup

Install Dependencies

npm install

Install Browsers

npx playwright install

Run All Tests

npx playwright test

Run Tests in Headed Mode

npx playwright test --headed

Open HTML Report

npx playwright show-report

Generate Trace

npx playwright test --trace on

Open Trace Viewer

npx playwright show-trace trace.zip

---

Project Structure

TASK2
│
├── tests
│   ├── browser-window.spec.ts
│   ├── network-mocking.spec.ts
│   ├── fixture-demo.spec.ts
│   ├── failures.spec.ts
│   └── timeoutSimulation.spec.ts
│
├── fixtures
│   └── baseFixture.ts
│
├── utils
│   └── Logger.ts
│
├── docs
│   └── Debugging.md
│
├── playwright.config.ts
├── package.json
└── README.md

---

Day 1 Tasks

1. Browser Window Handling

Website Used:

https://demoqa.com/browser-windows

Implemented Scenarios:

- Verify New Tab button opens a new tab
- Verify content of newly opened tab
- Close child tab and switch back to parent tab
- Verify new message window content

Learning

- Handling multiple browser tabs
- Switching between parent and child windows
- Using Browser Context events
- Working with new page events

---

2. Network Mocking

Website Used:

https://demoqa.com/books

Implemented Scenarios:

- Mock Books API with custom data
- Mock empty API response
- Delay API response and observe behavior

Learning

- API interception using page.route()
- Returning mocked responses
- Simulating backend behavior
- Testing UI without dependency on actual APIs

---

Day 2 Tasks

1. Custom Fixtures

Created:

- Logger utility
- Base fixture

Files:

- utils/Logger.ts
- fixtures/baseFixture.ts

Purpose:

To reduce duplicate code and make tests reusable.

Learning

- Fixture lifecycle
- Shared setup and teardown
- Dependency injection in Playwright

---

2. Fixture Based Tests

Implemented test cases using custom fixtures.

Learning

- Cleaner test design
- Better code reusability
- Easier maintenance

---

Reporting

HTML Report

Generated using:

npx playwright show-report

Information Available:

- Passed tests
- Failed tests
- Execution duration
- Error details
- Screenshots

---

Trace Viewer

Generated using:

npx playwright test --trace on

Information Available:

- Step-by-step execution
- Screenshots
- Network requests
- Console logs
- Timeline view

Learning

Trace Viewer is useful for identifying the exact point of failure in a test.

---

Failure Simulation

A separate file was created to understand common automation failures.

Failure Categories Covered

Locator Failure

Root Cause:
Incorrect locator used in the test.

Assertion Failure

Root Cause:
Expected result did not match actual result.

Navigation Failure

Root Cause:
Invalid URL or page unavailable.

Network Failure

Root Cause:
API request was blocked or aborted.

Timeout Failure

Root Cause:
Test execution exceeded configured timeout.

---

Timeout Simulation

The following timeout types were implemented and analyzed.

Test Timeout

Occurs when the entire test takes longer than the configured timeout.

Expect Timeout

Occurs when an assertion condition is not met within the specified time.

Action Timeout

Occurs when actions such as click or fill cannot complete within the configured timeout.

---

Debugging Tools Used

- HTML Report
- Trace Viewer
- Playwright Inspector
- Screenshots
- Console Logs

---

Key Learnings

During this task I learned:

- Playwright project setup
- Browser tab and window handling
- Network mocking concepts
- Custom fixture implementation
- Generating and analyzing reports
- Using Trace Viewer
- Debugging failed tests
- Understanding different timeout types
- Writing reusable automation code

---

Challenges Faced

- Understanding Browser Context events
- Implementing Network Mocking correctly
- Working with custom fixtures
- Analyzing failures using Trace Viewer
- Understanding timeout behavior

---

Conclusion

This assignment helped me gain practical experience with advanced Playwright concepts beyond basic UI automation. I learned how to create reusable test frameworks, debug failures effectively, work with mocked APIs, and analyze executions using reports and traces. These concepts will help in building scalable and maintainable automation frameworks in future projects.
