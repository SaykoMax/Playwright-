Feature: Login functionality

Scenario: Successful login
  Given user is on login page
  When user enters valid username and password
  Then user should be navigated to dashboard

Scenario: Invalid login
  Given user is on login page
  When user enters invalid credentials
  Then error message should be displayed

Scenario Outline: Login with multiple credentials
  Given user is on login page
  When user enters "<username>" and "<password>"
  Then login result should be "<result>"

Examples:
  | username | password | result |
  | tomsmith | SuperSecretPassword! | success |
  | admin | wrong123 | failure |
