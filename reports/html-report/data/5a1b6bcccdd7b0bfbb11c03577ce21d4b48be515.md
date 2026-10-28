# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\client-kyc-sensitive.spec.js >> Client / KYC - sensitive data >> TC-CLI-V12 Income vs premium affordability validation @regression @client @p2 @sensitive @seeded @api
- Location: tests\ui\client-kyc-sensitive.spec.js:66:3

# Error details

```
Error: a very high premium against a very low income should raise an affordability warning or block

expect(locator).toBeVisible() failed

Locator: getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).or(getByTestId('product-warning').or(locator('[data-testid="validation-error-alert"], .alert-warning, [role="alert"], .warning')).first()).filter({ hasText: /afford|20\s?%|exceed.*income|income|premium/i }).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - a very high premium against a very low income should raise an affordability warning or block getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).or(getByTestId('product-warning').or(locator('[data-testid="validation-error-alert"], .alert-warning, [role="alert"], .warning')).first()).filter({ hasText: /afford|20\s?%|exceed.*income|income|premium/i }).first() with timeout 8000ms
  - waiting for getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).or(getByTestId('product-warning').or(locator('[data-testid="validation-error-alert"], .alert-warning, [role="alert"], .warning')).first()).filter({ hasText: /afford|20\s?%|exceed.*income|income|premium/i }).first()

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
  - link "Learner Agent 001":
    - /url: http://34.93.84.61:8081/profile
  - button "Logout"
- main:
  - alert:
    - text: "Please review the following:"
    - list:
      - listitem: Sum assured exceeds the selected product maximum.
  - link "← Back to KYC & Financial":
    - /url: http://34.93.84.61:8081/applications/151/kyc-financial
  - link "Application Summary":
    - /url: http://34.93.84.61:8081/applications/151
  - text: "Application #151"
  - heading "Product & Policy Configuration" [level=1]
  - paragraph: Select the product, sum assured, premium payment frequency, premium payment term, and coverage term.
  - text: Product
  - combobox "Product":
    - option "Select product"
    - option "Elite Legacy Whole Life"
    - option "FlexiPay Whole Life"
    - option "SecureLife Whole Life" [selected]
    - option "WealthBuilder Whole Life"
  - text: "Allowed Sum Assured: $100,000.00 to $1,000,000.00 Sum Assured"
  - spinbutton "Sum Assured": "5000000"
  - text: Premium Payment Frequency
  - combobox "Premium Payment Frequency":
    - option "Monthly" [selected]
    - option "Quarterly"
    - option "Semi-Annual"
    - option "Annual"
  - text: Premium Payment Term
  - combobox "Premium Payment Term":
    - option "Select term"
    - option "10 years"
    - option "15 years"
    - option "20 years" [selected]
    - option "25 years"
    - option "30 years"
  - text: Coverage Term
  - combobox "Coverage Term":
    - option "Whole Life" [selected]
    - option "To Age 100"
  - text: Estimated Total Modal Premium $1,979.17 Estimated premium will be saved when you continue.
  - button "Save and Continue"
- contentinfo: TalentFarm QA Automation Lab Insurance Order Entry Demo
```

# Test source

```ts
  1  | /**
  2  |  * KYC / SSN / income tests. SENSITIVE-DATA RULE: Playwright traces and videos record typed values and cannot be masked,
  3  |  * so they are OFF for this whole file (test.use must be top-level for trace/video). Masked screenshots from
  4  |  * utils/evidence.js are still attached on failure. Data is synthetic (123-45-6789 placeholder SSN, example.test emails) regardless.
  5  |  */
  6  | const { test, expect } = require('../../fixtures');
  7  | const { tc } = require('../../fixtures');
  8  | const M = require('../../config/messages');
  9  | const { S } = require('../../config/selectors');
  10 | const { files } = require('../../utils/files');
  11 | const { buildKyc, buildProduct } = require('../../utils/dataBuilder');
  12 | const { progressTo } = require('../../utils/flows');
  13 | const routes = require('../../config/routes');
  14 | const { applicationIdFromUrl } = require('../../pages/DashboardPage');
  15 | const { expectBlocked, captureEvidence } = require('../../utils/assertions');
  16 | 
  17 | test.use({ agentRole: 'learnerAgent', trace: 'off', video: 'off' });
  18 | 
  19 | test.describe('Client / KYC - sensitive data', () => {
  20 |   test(...tc('CLI-V08'), async ({ pages, page }, testInfo) => {
  21 |     // The real KYC form has NO separate SSN field: the SSN is the ID number when the ID type is SSN. The app must show it
  22 |     // masked once saved - on the KYC page after a reload, on the review page and in the API response.
  23 |     await progressTo(pages, 'kyc');
  24 |     const id = applicationIdFromUrl(page.url());
  25 |     const kyc = buildKyc({ idType: 'SSN' });
  26 |     const digitsOnly = kyc.idNumber.replace(/-/g, '');
  27 |     await pages.kyc.fill(kyc);
  28 |     const before = await pages.kyc.stepTitle();
  29 |     await pages.kyc.next();
  30 |     await pages.kyc.expectAdvanced(before);
  31 |     const expectMasked = async (label) => {
  32 |       const html = await page.content();
  33 |       expect(html, `${label}: the full SSN must not appear`).not.toContain(kyc.idNumber);
  34 |       expect(html, `${label}: the unformatted SSN must not appear`).not.toContain(digitsOnly);
  35 |     };
  36 |     await test.step('KYC page after reload', async () => {
  37 |       await page.goto(routes.step(id, 'kyc-financial'));
  38 |       await expectMasked('KYC page');
  39 |       const shown = await pages.kyc.visibleSsn();
  40 |       await captureEvidence(page, testInfo, 'ssn-as-displayed');
  41 |       expect(shown, 'only the last four digits may be visible').not.toContain(kyc.idNumber.slice(0, 6));
  42 |       expect(shown, 'last four digits should remain visible').toMatch(/6789$/);
  43 |     });
  44 |     await test.step('review page', async () => {
  45 |       await page.goto(routes.step(id, 'review'));
  46 |       await expectMasked('review page');
  47 |     });
  48 |   });
  49 | 
  50 |   test(...tc('CLI-V09'), async ({ pages }) => {
  51 |     await progressTo(pages, 'kyc');
  52 |     test.skip(!(await pages.kyc.$(S.kyc.uploadInput).count()), 'No upload control on the KYC step (see DOC-V02 for the document step)');
  53 |     await pages.kyc.uploadKycDocument(files.unsupportedExe());
  54 |     await pages.kyc.expectErrorText(M.fileType);
  55 |   });
  56 | 
  57 |   test(...tc('CLI-V10'), async ({ pages }) => {
  58 |     await progressTo(pages, 'kyc');
  59 |     const before = await pages.kyc.stepTitle();
  60 |     await pages.kyc.fill(buildKyc({ pep: true }));
  61 |     await expect(pages.kyc.$(S.kyc.pepDetails)).toBeVisible();
  62 |     await pages.kyc.next();
  63 |     await expectBlocked(pages.kyc, before, M.required);
  64 |   });
  65 | 
  66 |   test(...tc('CLI-V12'), async ({ pages, page }, testInfo) => {
  67 |     const { data } = await progressTo(pages, 'product', {
  68 |       kyc: buildKyc({ income: 12000 }),
  69 |       product: buildProduct({ faceValue: 5_000_000 }),
  70 |     });
  71 |     await pages.product.select(data.product.namePattern);
  72 |     await pages.product.configure(data.product);
  73 |     await pages.product.next();
  74 |     await captureEvidence(page, testInfo, 'affordability-check');
  75 |     await expect(
  76 |       pages.product.$$(S.common.anyError).or(pages.product.$(S.product.warning)).filter({ hasText: M.affordability }).first(),
  77 |       'a very high premium against a very low income should raise an affordability warning or block',
> 78 |     ).toBeVisible();
     |       ^ Error: a very high premium against a very low income should raise an affordability warning or block
  79 |   });
  80 | });
  81 | 
```