Feature: Form Submission

Scenario: Successful form submission
  Given user is on form page
  When user fills the form with following data:
    | name  | Sayee             |
    | email | sayee@test.com    |
  Then form should be submitted successfully

Scenario: Submit form with empty name
  Given user is on form page
  When user fills the form with following data:
    | name  |                  |
    | email | sayee@test.com   |
  Then form validation message should be displayed

Scenario: Submit form with invalid email
  Given user is on form page
  When user fills the form with following data:
    | name  | Sayee      |
    | email | invalid123 |
  Then form validation message should be displayed

Scenario Outline: Multiple form submissions
  Given user is on form page
  When user enters "<name>" and "<email>"
  Then form result should be "<result>"

Examples:
  | name  | email            | result  |
  | Sayee | sayee@test.com   | success |
  |       | sayee@test.com   | failure |
