import http from 'k6/http';
import { check } from 'k6';

export const options = {
  stages: [
    { duration: '10s', target: 20 },
    { duration: '30s', target: 20 },
    { duration: '20s', target: 0 },
  ],
};

export default function () {
  const url = 'https://quickpizza.grafana.com/api/users/token/login?set_cookie=true';

  const payload = JSON.stringify({
    username: 'default',
    password: '12345678',
    csrf: 'RYSU4jq3Syf0yHsTjvH6y5woFXvQhRUS'
  });

  const params = {
    headers: {
      'Content-Type': 'application/json',
    },
  };

  const res = http.post(url, payload, params);

  check(res, {
    'Status is 200': (r) => r.status === 200,
    'Login successful': (r) => r.status === 200,
  });
}



For Exercise 1: Identify the Test Type, the correct answers are:

Scenario	Test Type	Reason

5,000 students start a quiz at exactly 9:00 AM	Load Testing	Verifies system performance under the expected peak number of concurrent users.
LMS is pushed to 20,000 users to determine the system breaking point	Stress Testing	Increases the load beyond normal capacity to identify when the system fails.
Quiz platform is run continuously for 24 hours	Soak (Endurance) Testing	Checks system stability, memory leaks, and performance over a long duration.
The tester gradually increases virtual users until the application becomes unresponsive and starts returning errors	Stress Testing	Continues increasing the load until the application reaches its breaking point.
The course enrollment system is run with 2,500 concurrent users continuously for 24 hours	Soak (Endurance) Testing	Tests how the application performs under a sustained normal load for an extended period.


Final Answers

1. Load Testing


2. Stress Testing


3. Soak (Endurance) Testing


4. Stress Testing


5. Soak (Endurance) Testing 


