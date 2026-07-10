import http from 'k6/http';
import { check, sleep } from 'k6';

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

// No external HTML reporter needed — k6 always writes a text summary to
// stdout automatically. To save it to a file instead of just printing it,
// run k6 like this:
//   k6 run login-load-test-no-bonus.js > results.txt
// Or get raw JSON metrics for your own report:
//   k6 run --out json=results.json login-load-test-no-bonus.js
