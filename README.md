# QuickPizza Login - Performance Testing Task

This repo covers both exercises from the performance testing assignment.

## Exercise 1 - Identify the Test Type

Went through the 5 scenarios and matched each one to a test type (Load / Stress / Soak / Spike).
See `exercise1-test-types.md` (or the answer table shared in chat) for the breakdown.

## Exercise 2 - K6 Login Load Test

Target app: https://quickpizza.grafana.com/

### What the script does
- Hits the login endpoint: `POST /api/users/token/login`
- Sends `{ username, password }` as JSON
- Simulates 20 virtual users
  - ramp up: 10s
  - hold: 30s
  - ramp down: 20s
- Checks that the response is `200 OK` and that a login token comes back

### Files
- `login-load-test-no-bonus.js` - the k6 test script
- `generate-report.js` - turns the k6 output into a readable HTML report (Node.js, no internet needed)
- `summary.json` - raw results from the last test run
- `summary-report.html` - the generated report (open this in a browser)

### How to run it

1. Run the load test:
   ```
   k6 run login-load-test-no-bonus.js
   ```
   This creates `summary.json` in the same folder.

2. Generate the HTML report from that file:
   ```
   node generate-report.js summary.json summary-report.html
   ```

3. Open `summary-report.html` in your browser to see the results (response times, pass/fail checks, thresholds).

### Notes
- Default test login is `default` / `12345678`. Change these via env vars if needed:
  ```
  k6 run -e QP_USERNAME=youruser -e QP_PASSWORD=yourpass login-load-test-no-bonus.js
  ```
- The `p(95)` response time threshold is set to under 1000ms - if it shows as crossed, that just means the login endpoint was slower than that under load, not a script issue.
