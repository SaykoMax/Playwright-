const report = require('multiple-cucumber-html-reporter');

report.generate({
  jsonDir: 'reports',
  reportPath: 'reports/html-report',
  metadata: {
    browser: {
      name: 'chrome',
      version: 'latest'
    },
    device: 'Local Machine',
    platform: {
      name: 'windows',
      version: '11'
    }
  }
});

console.log('HTML Report Generated');
