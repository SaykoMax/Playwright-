import http from 'k6/http';
import { check } from 'k6';

export const options = {
  stages: [
    { duration: '10s', target: 20 }, // Ramp up
    { duration: '30s', target: 20 }, // Constant load
    { duration: '20s', target: 0 },  // Ramp down
  ],
};

export default function () {

  // Step 1: Get application page to create a session
  const home = http.get('https://quickpizza.grafana.com/');

  // Step 2: Read CSRF cookie
  const jar = http.cookieJar();
  const cookies = jar.cookiesForURL('https://quickpizza.grafana.com/');

  if (!cookies.csrf_token) {
    console.log("CSRF token not received.");
    return;
  }

  const csrf = cookies.csrf_token[0];

  // Step 3: Login request
  const url = 'https://quickpizza.grafana.com/api/users/token/login?set_cookie=true';

  const payload = JSON.stringify({
    username: 'default',
    password: '12345678',
    csrf: csrf
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  const res = http.post(url, payload, params);

  console.log("Status:", res.status);
  console.log("Response:", res.body);

  check(res, {
    'Status is 200': (r) => r.status === 200,
    'Token received': (r) => r.body.includes('token'),
  });
}
