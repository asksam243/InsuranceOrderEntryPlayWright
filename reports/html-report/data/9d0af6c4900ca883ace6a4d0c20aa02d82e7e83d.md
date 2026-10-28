# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\dashboard.spec.js >> Agent Dashboard >> multi-agent isolation >> TC-DASH-V02 Agent sees only own applications (multi-agent isolation) @regression @dashboard @p1 @release-gate @api
- Location: tests\ui\dashboard.spec.js:68:5

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByTestId('login-email-input').or(getByLabel(/e-?mail|user ?name/i)).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByTestId('login-email-input').or(getByLabel(/e-?mail|user ?name/i)).first() with timeout 8000ms
  - waiting for getByTestId('login-email-input').or(getByLabel(/e-?mail|user ?name/i)).first()

```

```yaml
- navigation:
  - link "Insurance Order Entry Demo Platform QA Automation Training App":
    - /url: http://34.93.84.61:8081/dashboard
  - list:
    - listitem:
      - link "Dashboard":
        - /url: http://34.93.84.61:8081/dashboard
    - listitem:
      - link "Applications":
        - /url: http://34.93.84.61:8081/applications
    - listitem:
      - link "Products":
        - /url: http://34.93.84.61:8081/products
    - listitem:
      - link "Support":
        - /url: http://34.93.84.61:8081/support
  - link "Valid Agent":
    - /url: http://34.93.84.61:8081/profile
  - button "Logout"
- main:
  - heading "Agent Dashboard" [level=1]
  - paragraph: Track drafts, submitted applications, and policy order entry work.
  - link "Start New Application":
    - /url: http://34.93.84.61:8081/applications/new
  - text: Draft 9 Submitted 2 Under Review 0 Approved 1 Requires Info 0
  - heading "Recent Applications" [level=2]
  - link "View all":
    - /url: http://34.93.84.61:8081/applications
  - table:
    - rowgroup:
      - row "Reference Client Product Status Updated":
        - columnheader "Reference"
        - columnheader "Client"
        - columnheader "Product"
        - columnheader "Status"
        - columnheader "Updated"
        - columnheader
    - rowgroup:
      - 'row "Draft #128 QaDAFCHUGV TesterDAFCHUGVBE Not selected DRAFT 28 Oct 2026 Open"':
        - 'cell "Draft #128"'
        - cell "QaDAFCHUGV TesterDAFCHUGVBE"
        - cell "Not selected"
        - cell "DRAFT"
        - cell "28 Oct 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/128
      - 'row "Draft #49 New Applicant Not selected DRAFT 14 Oct 2026 Open"':
        - 'cell "Draft #49"'
        - cell "New Applicant"
        - cell "Not selected"
        - cell "DRAFT"
        - cell "14 Oct 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/49
      - 'row "Draft #44 Test#$# Insured Elite Legacy Whole Life DRAFT 04 Jun 2026 Open"':
        - 'cell "Draft #44"'
        - cell "Test#$# Insured"
        - cell "Elite Legacy Whole Life"
        - cell "DRAFT"
        - cell "04 Jun 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/44
      - row "WL2026060255444 Test Application Elite Legacy Whole Life SUBMITTED 02 Jun 2026 Open":
        - cell "WL2026060255444"
        - cell "Test Application"
        - cell "Elite Legacy Whole Life"
        - cell "SUBMITTED"
        - cell "02 Jun 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/43
      - 'row "Draft #42 Not selected DRAFT 02 Jun 2026 Open"':
        - 'cell "Draft #42"'
        - cell
        - cell "Not selected"
        - cell "DRAFT"
        - cell "02 Jun 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/42
      - 'row "Draft #41 Not selected DRAFT 17 May 2026 Open"':
        - 'cell "Draft #41"'
        - cell
        - cell "Not selected"
        - cell "DRAFT"
        - cell "17 May 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/41
      - 'row "Draft #40 Not selected DRAFT 17 May 2026 Open"':
        - 'cell "Draft #40"'
        - cell
        - cell "Not selected"
        - cell "DRAFT"
        - cell "17 May 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/40
      - 'row "Draft #39 Test Name Guaranteed Return Whole Life DRAFT 04 Jun 2026 Open"':
        - 'cell "Draft #39"'
        - cell "Test Name"
        - cell "Guaranteed Return Whole Life"
        - cell "DRAFT"
        - cell "04 Jun 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/39
      - 'row "Draft #38 Sudarsan Thyagarajan Not selected DRAFT 17 May 2026 Open"':
        - 'cell "Draft #38"'
        - cell "Sudarsan Thyagarajan"
        - cell "Not selected"
        - cell "DRAFT"
        - cell "17 May 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/38
      - 'row "Draft #37 Sudarsan Thyagarajan Elite Legacy Whole Life DRAFT 17 May 2026 Open"':
        - 'cell "Draft #37"'
        - cell "Sudarsan Thyagarajan"
        - cell "Elite Legacy Whole Life"
        - cell "DRAFT"
        - cell "17 May 2026"
        - cell "Open":
          - link "Open":
            - /url: http://34.93.84.61:8081/applications/37
- contentinfo: TalentFarm QA Automation Lab Insurance Order Entry Demo
```

# Test source

```ts
  1  | const { expect } = require('@playwright/test');
  2  | const { BasePage } = require('./BasePage');
  3  | const { S } = require('../config/selectors');
  4  | const routes = require('../config/routes');
  5  | 
  6  | class LoginPage extends BasePage {
  7  |   async goto() {
  8  |     await this.page.goto(routes.login);
> 9  |     await expect(this.$(S.login.email)).toBeVisible();
     |                                         ^ Error: expect(locator).toBeVisible() failed
  10 |   }
  11 | 
  12 |   async login(user) {
  13 |     await this.$(S.login.email).fill(user.email);
  14 |     await this.$(S.login.password).fill(user.password);
  15 |     await this.$(S.login.submit).click();
  16 |   }
  17 | 
  18 |   async loginViaUi(user) {
  19 |     await this.goto();
  20 |     await this.login(user);
  21 |   }
  22 | 
  23 |   async expectLoggedIn() {
  24 |     await expect(this.page).not.toHaveURL(/\/login\/?(\?.*)?$/);
  25 |     await expect(this.$(S.common.logout)).toBeVisible();
  26 |   }
  27 | 
  28 |   /** Still on the login page, with a message that matches the pattern, and no session. */
  29 |   async expectRejected(pattern) {
  30 |     await expect(this.page).toHaveURL(/\/login/);
  31 |     const err = this.$(S.login.error);
  32 |     await expect(err).toBeVisible();
  33 |     if (pattern) await expect(err).toHaveText(pattern);
  34 |   }
  35 | 
  36 |   async fillOtp(code) {
  37 |     await this.$(S.login.otpInput).fill(code);
  38 |     await this.$(S.login.otpSubmit).click();
  39 |   }
  40 | 
  41 |   async logout() {
  42 |     await this.$(S.common.logout).click();
  43 |     await expect(this.page).toHaveURL(/login/);
  44 |   }
  45 | 
  46 |   async openForgotPassword() {
  47 |     await this.$(S.login.forgotLink).click();
  48 |   }
  49 | }
  50 | 
  51 | module.exports = { LoginPage };
  52 | 
```