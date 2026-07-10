 http from 'k6/http';
import { check, sleep } from 'k6';
import { htmlReport } from 'https://raw.githubusercontent.com/benc-uk/k6-reporter/main/dist/bundle.js';
import { textSummary } from 'https://jslib.k6.io/k6-summary/0.0.2/index.js';

// --- Test configuration ---
export const options = {
  stages: [
    { duration: '10s', target: 20 }, // ramp-up to 20 VUs over 10s
    { duration: '30s', target: 20 }, // hold at 20 VUs for 30s
    { duration: '20s', target: 0 },  // ramp-down to 0 over 20s
  ],
  thresholds: {
    http_req_failed: ['rate<0.01'],   // less than 1% failed requests
    http_req_duration: ['p(95)<1000'], // 95% of requests under 1s
  },
};

const BASE_URL = 'https://quickpizza.grafana.com';

// Set these to a valid QuickPizza account.
// If you don't have one yet, register once via:
//   POST {BASE_URL}/api/users  { "username": "...", "password": "..." }
const USERNAME = __ENV.QP_USERNAME || 'default';
const PASSWORD = __ENV.QP_PASSWORD || '12345678';

export default function () {
  const payload = JSON.stringify({
    username: USERNAME,
    password: PASSWORD,
  });

  const params = {
    headers: { 'Content-Type': 'application/json' },
  };

  const res = http.post(`${BASE_URL}/api/users/token/login`, payload, params);

  check(res, {
    'status is 200': (r) => r.status === 200,
    'login successful (token present)': (r) => {
      try {
        return !!r.json('token');
      } catch (e) {
        return false;
      }
    },
  });

  sleep(1);
}

// --- Bonus: generate an HTML summary report ---
export function handleSummary(data) {
  return {
    'summary.html': htmlReport(data),
    stdout: textSummary(data, { indent: ' ', enableColors: true }),
  };
}
