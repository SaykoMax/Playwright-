Perfect. Since the repository contains the files we created for the assignment, here's how you can explain the project to your senior file-by-file.

Project Overview

This project is divided into two parts:

Day 1

Browser Window Handling

Network Mocking


Day 2

Fixtures

Reports

Trace Viewer

Debugging

Timeout Simulation



---

playwright.config.ts

Purpose

This is the central configuration file for Playwright.

What it controls

Browser settings

Trace configuration

Screenshots

Reports

Test directory


Example explanation:

> This file defines how Playwright executes tests. I configured trace generation, browser execution settings, and reporting options here.




---

browser-window.spec.ts

Purpose

Automates multiple tab and window scenarios on DemoQA.

Test Cases

TC_001 Verify New Tab button opens a new tab

What happens:

1. Open Browser Windows page.


2. Click New Tab button.


3. Wait for new page event.


4. Verify new tab URL.



Learning:

page.context().waitForEvent('page')

This waits for a new tab to open.


---

TC_002 Verify content of newly opened tab

What happens:

1. Open new tab.


2. Capture new tab object.


3. Verify text:



This is a sample page

Learning:

Working with child pages.


---

TC_003 Close child tab and switch back

What happens:

1. Open new tab.


2. Close child tab.


3. Continue working with parent page.



Learning:

Window management.


---

TC_004 Verify New Window Message

What happens:

1. Open message window.


2. Capture new page.


3. Read body text.


4. Verify message.



Learning:

Handling popup windows.


---

network-mocking.spec.ts

Purpose

Learn API interception.


---

TC_005 Mock Books API

What happens:

page.route()

intercepts Books API.

Instead of actual response:

{
  "books": [...]
}

we return our own data.

Then verify UI shows mocked book.

Learning:

route.fulfill()

returns custom response.


---

TC_006 Mock Empty Response

What happens:

Return:

{
  "books": []
}

Verify application handles no data.

Learning:

Edge case testing.


---

TC_007 Delay API Response

What happens:

Intercept request.

Simulate delayed response.

Verify application still loads correctly.

Learning:

Slow network testing.


---

Logger.ts

Purpose

Utility class.

Code:

export class Logger {
   log(message:string){
      console.log(message);
   }
}

Explanation:

Instead of writing:

console.log()

everywhere,

we created reusable utility.

Learning:

Code reusability.


---

baseFixture.ts

Purpose

Create reusable Playwright fixture.

Example:

export const test = base.extend(...)

Explanation:

Fixture automatically provides Logger object to tests.

Instead of:

const logger = new Logger();

inside every test,

fixture injects it automatically.

Learning:

Dependency Injection.


---

fixture-demo.spec.ts

Purpose

Demonstrate fixture usage.

Example:

test('Fixture Demo',
 async({page,logger})=>{

Explanation:

Logger comes from fixture.

No object creation needed.

Learning:

Fixture consumption.


---

failures.spec.ts

Purpose

Understand common automation failures.

Contains:

Locator Failure

Wrong locator.

Learning:

Importance of stable locators.


---

Assertion Failure

Wrong expected value.

Learning:

Assertion validation.


---

Navigation Failure

Invalid URL.

Learning:

URL validation.


---

Network Failure

API aborted.

Learning:

Backend dependency failures.


---

Timeout Failure

Execution exceeds timeout.

Learning:

Test performance analysis.


---

timeoutSimulation.spec.ts

Purpose

Understand Playwright timeout types.


---

Test Timeout

Entire test exceeds timeout.

test.setTimeout()


---

Expect Timeout

Assertion exceeds timeout.

expect(...).toBeVisible()


---

Action Timeout

Click/fill action exceeds timeout.

Learning:

Different timeout levels.


---

Debugging.md

Purpose

Document debugging analysis.

Contains:

For each failure:

Failure Type

Steps Used

Root Cause

Learning


Examples:

Locator Failure

Assertion Failure

Navigation Failure

Network Failure

Timeout Failure


Also contains:

Test Timeout

Expect Timeout

Action Timeout



---

README.md

Purpose

Project documentation.

Contains:

Setup steps

Execution steps

Project structure

Learning summary

Challenges faced



---

HTML Report

Generated using:

npx playwright show-report

Purpose:

View passed tests

View failed tests

Error details

Screenshots



---

Trace Viewer

Generated using:

npx playwright test --trace on

Purpose:

Replay test execution step-by-step.

Shows:

Actions

Screenshots

Network calls

DOM state



---

If Senior Asks "What did you learn?"

You can answer:

> In this assignment I learned how to handle multiple browser tabs and windows, perform network mocking using Playwright, create reusable fixtures, generate HTML reports and traces, debug different failure types, and understand different timeout mechanisms. I also learned how to organize automation code in a reusable and maintainable structure.
