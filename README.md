// generate-report.js
// Reads the summary.json produced by k6 and builds a standalone HTML report.
// No internet connection needed.
//
// Usage:
//   node generate-report.js summary.json summary-report.html

const fs = require('fs');

const inPath = process.argv[2] || 'summary.json';
const outPath = process.argv[3] || 'summary-report.html';

const data = JSON.parse(fs.readFileSync(inPath, 'utf-8'));
const metrics = data.metrics || {};

function metric(name) {
  return (metrics[name] && metrics[name].values) || {};
}

function fmt(v, unit = '') {
  if (v === undefined || v === null) return 'N/A';
  if (typeof v === 'number') return v.toLocaleString(undefined, { maximumFractionDigits: 2 }) + unit;
  return v + unit;
}

const httpDuration = metric('http_req_duration');
const httpFailed = metric('http_req_failed');
const checks = metric('checks');
const vusMax = metric('vus_max');
const iterations = metric('iterations');
const dataReceived = metric('data_received');
const dataSent = metric('data_sent');

const totalChecks = (checks.passes || 0) + (checks.fails || 0);
const checkPassRate = totalChecks ? ((checks.passes || 0) / totalChecks) * 100 : 0;
const failRatePct = (httpFailed.rate || 0) * 100;

const rows = `
  <tr><td>Total Iterations</td><td>${fmt(iterations.count)}</td></tr>
  <tr><td>Max Virtual Users</td><td>${fmt(vusMax.value)}</td></tr>
  <tr><td>Checks Passed</td><td>${checks.passes || 0} / ${totalChecks} (${checkPassRate.toFixed(1)}%)</td></tr>
  <tr><td>HTTP Request Failure Rate</td><td>${failRatePct.toFixed(2)}%</td></tr>
  <tr><td>Avg Response Time</td><td>${fmt(httpDuration.avg, ' ms')}</td></tr>
  <tr><td>Min Response Time</td><td>${fmt(httpDuration.min, ' ms')}</td></tr>
  <tr><td>Max Response Time</td><td>${fmt(httpDuration.max, ' ms')}</td></tr>
  <tr><td>p90 Response Time</td><td>${fmt(httpDuration['p(90)'], ' ms')}</td></tr>
  <tr><td>p95 Response Time</td><td>${fmt(httpDuration['p(95)'], ' ms')}</td></tr>
  <tr><td>Data Received</td><td>${fmt(dataReceived.count, ' bytes')}</td></tr>
  <tr><td>Data Sent</td><td>${fmt(dataSent.count, ' bytes')}</td></tr>
`;

let thresholdsHtml = '';
for (const [name, m] of Object.entries(metrics)) {
  if (m.thresholds) {
    for (const [cond, result] of Object.entries(m.thresholds)) {
      const ok = result.ok !== false;
      const status = ok ? 'PASS' : 'FAIL';
      const color = ok ? '#1a7f37' : '#c0362c';
      thresholdsHtml += `<tr><td>${name}</td><td>${cond}</td><td style="color:${color};font-weight:bold">${status}</td></tr>`;
    }
  }
}

const html = `<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>K6 Login Load Test — Summary Report</title>
<style>
  body { font-family: Arial, Helvetica, sans-serif; background: #f5f6f8; margin: 0; padding: 40px; color: #1c1e21; }
  h1 { color: #1c1e21; }
  .subtitle { color: #555; margin-bottom: 30px; }
  table { border-collapse: collapse; width: 100%; max-width: 700px; background: #fff; box-shadow: 0 1px 3px rgba(0,0,0,0.1); margin-bottom: 30px; }
  th, td { text-align: left; padding: 10px 14px; border-bottom: 1px solid #e5e5e5; }
  th { background: #2b3a55; color: #fff; }
  tr:hover { background: #f0f4ff; }
  .card { background: #fff; padding: 20px; border-radius: 6px; box-shadow: 0 1px 3px rgba(0,0,0,0.1); max-width: 700px; margin-bottom: 30px; }
</style>
</head>
<body>
  <h1>K6 Login Load Test — Summary Report</h1>
  <p class="subtitle">QuickPizza login endpoint | Generated ${new Date().toLocaleString()}</p>

  <div class="card">
    <h2>Key Metrics</h2>
    <table>${rows}</table>
  </div>

  <div class="card">
    <h2>Thresholds</h2>
    <table>
      <tr><th>Metric</th><th>Condition</th><th>Result</th></tr>
      ${thresholdsHtml || '<tr><td colspan="3">No thresholds defined</td></tr>'}
    </table>
  </div>
</body>
</html>
`;

fs.writeFileSync(outPath, html, 'utf-8');
console.log(`Report written to ${outPath}`);



node generate-report.js summary.json summary-report.html
