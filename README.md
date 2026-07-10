import http from 'k6/http';
import { check } from 'k6';

export const options = {
  stages: [
    { duration: '10s', target: 20 }, // Ramp-up
    { duration: '30s', target: 20 }, // Maintain load
    { duration: '20s', target: 0 },  // Ramp-down
  ],
};

const BASE_URL = 'https://quickpizza.grafana.com';

export default function (): void {

  const payload = JSON.stringify({
    username: 'default',
    password: '12345678',
    csrf: 'RYSU4jq3Syf0yHsTjvH6y5woFXvQhRUS' // Replace with a fresh CSRF token if required
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  const response = http.post(
    `${BASE_URL}/api/users/token/login?set_cookie=true`,
    payload,
    params
  );

  check(response, {
    'Status code is 200': (r) => r.status === 200,
    'Login successful': (r) => r.body.includes('token'),
  });

  console.log(`Status: ${response.status}`);
  console.log(`Response: ${response.body}`);
}
