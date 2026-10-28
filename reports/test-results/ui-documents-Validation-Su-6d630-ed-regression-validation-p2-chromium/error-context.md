# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\documents.spec.js >> Validation Summary (review step with unresolved errors) >> TC-VAL-V01 Validation summary lists all unresolved errors, grouped @regression @validation @p2
- Location: tests\ui\documents.spec.js:74:3

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByTestId('review-validation-errors-items').or(locator('[data-testid="review-validation-errors"] li, [data-testid^="validation-item"], .validation-summary li, .validation-summary a')).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByTestId('review-validation-errors-items').or(locator('[data-testid="review-validation-errors"] li, [data-testid^="validation-item"], .validation-summary li, .validation-summary a')).first() with timeout 8000ms
  - waiting for getByTestId('review-validation-errors-items').or(locator('[data-testid="review-validation-errors"] li, [data-testid^="validation-item"], .validation-summary li, .validation-summary a')).first()

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
  - link "← Back to Documents":
    - /url: http://34.93.84.61:8081/applications/133/documents
  - link "Application Summary":
    - /url: http://34.93.84.61:8081/applications/133
  - text: "Application #133"
  - heading "Review Application" [level=1]
  - paragraph: Review the application details and resolve any blocking validation errors before submission.
  - heading "Submission Validation" [level=2]
  - text: No blocking validation errors found.
  - link "Back to Documents":
    - /url: http://34.93.84.61:8081/applications/133/documents
  - button "Run Validation"
  - button "Submit Application"
  - heading "Application Snapshot" [level=2]
  - term: Client
  - definition: QaGLEYTZDY TesterGLEYTZDYIX
  - term: Calculated Age
  - definition: "36"
  - term: Product
  - definition: SecureLife Whole Life
  - term: Sum Assured
  - definition: $250,000.00
  - term: Premium Payment Frequency
  - definition: MONTHLY
  - term: Premium Payment Term
  - definition: 20 years
  - term: Coverage Term
  - definition: WHOLE_LIFE
  - term: Base Policy Premium
  - definition: $98.96
  - term: Rider Premium
  - definition: $0.00
  - term: Total Modal Premium
  - definition: $98.96
  - term: Status
  - definition: DRAFT
- contentinfo: TalentFarm QA Automation Lab Insurance Order Entry Demo
```

# Test source

```ts
  1   | const { test, tc, expect, env } = require('../../fixtures');
  2   | const M = require('../../config/messages');
  3   | const { files } = require('../../utils/files');
  4   | const { progressTo } = require('../../utils/flows');
  5   | const routes = require('../../config/routes');
  6   | const { applicationIdFromUrl } = require('../../pages/DashboardPage');
  7   | const { expectBlocked, captureEvidence } = require('../../utils/assertions');
  8   | 
  9   | test.describe('Document Upload & Validation Summary', () => {
  10  |   test.use({ agentRole: 'learnerAgent' });
  11  | 
  12  |   test(...tc('DOC-V01'), async ({ pages }) => {
  13  |     await progressTo(pages, 'documents');
  14  |     for (const file of [files.validPdf(), files.validJpg(), files.validPng()]) {
  15  |       await test.step(`${file.name} is accepted`, async () => {
  16  |         await pages.documents.upload(file, 0);
  17  |         await expect(pages.documents.uploaded.first()).toBeVisible();
  18  |         await expect(pages.documents.$$({ id: 'x', css: '.field-error, .invalid-feedback, [role="alert"]' }).filter({ hasText: M.fileType })).toHaveCount(0);
  19  |       });
  20  |     }
  21  |   });
  22  | 
  23  |   test(...tc('DOC-V02'), async ({ pages }) => {
  24  |     await progressTo(pages, 'documents');
  25  |     for (const file of [files.unsupportedExe(), files.unsupportedTxt()]) {
  26  |       await test.step(`${file.name} is rejected`, async () => {
  27  |         await pages.documents.upload(file, 0);
  28  |         await pages.documents.expectErrorText(M.fileType);
  29  |         await expect(pages.documents.uploaded).toHaveCount(0);
  30  |       });
  31  |     }
  32  |   });
  33  | 
  34  |   test(...tc('DOC-V03'), async ({ pages }) => {
  35  |     const max = env.rules.maxUploadMb;
  36  |     test.skip(max === null, 'Set MAX_UPLOAD_MB to run (Q17)');
  37  |     test.skip(max >= 49, 'Playwright in-memory upload limit is 50 MB; use a smaller MAX_UPLOAD_MB on the test environment');
  38  |     await progressTo(pages, 'documents');
  39  |     await pages.documents.upload(files.oversizePdf(max), 0);
  40  |     await pages.documents.expectErrorText(M.fileSize);
  41  |   });
  42  | 
  43  |   test(...tc('DOC-V04'), async ({ pages, page }, testInfo) => {
  44  |     await progressTo(pages, 'documents', { documents: false });
  45  |     const before = await pages.documents.stepTitle();
  46  |     await pages.documents.next();
  47  |     await captureEvidence(page, testInfo, 'next-without-documents');
  48  |     const reachedReview = await pages.review.submitButton.isVisible().catch(() => false);
  49  |     if (!reachedReview) {
  50  |       await expectBlocked(pages.documents, before, M.mandatoryDocument);
  51  |       return;
  52  |     }
  53  |     // The app lets the agent reach review: submission itself must still be blocked.
  54  |     if (await pages.review.submitButton.isEnabled()) {
  55  |       await pages.review.submit();
  56  |       await expect(pages.review.$({ id: 'reference-number', css: '[data-testid="reference-number"], .reference-number' }), 'no reference number may be issued without mandatory documents').toHaveCount(0);
  57  |     } else {
  58  |       await expect(pages.review.submitButton).toBeDisabled();
  59  |     }
  60  |   });
  61  | });
  62  | 
  63  | test.describe('Validation Summary (review step with unresolved errors)', () => {
  64  |   test.use({ agentRole: 'learnerAgent' });
  65  | 
  66  |   /** Reaches review WITHOUT uploading documents; skips if the app refuses to show review with errors. */
  67  |   async function reviewWithMissingDocuments(pages) {
  68  |     await progressTo(pages, 'documents', { documents: false });
  69  |     await pages.documents.next();
  70  |     const onReview = await pages.review.submitButton.waitFor({ state: 'visible', timeout: 5000 }).then(() => true).catch(() => false);
  71  |     test.skip(!onReview, 'The app blocks reaching review while errors exist (validation summary not reachable this way)');
  72  |   }
  73  | 
  74  |   test(...tc('VAL-V01'), async ({ pages }) => {
  75  |     await reviewWithMissingDocuments(pages);
> 76  |     await expect(pages.review.validation.items.first()).toBeVisible();
      |                                                         ^ Error: expect(locator).toBeVisible() failed
  77  |     const texts = await pages.review.validation.texts();
  78  |     expect(texts.some((t) => M.mandatoryDocument.test(t)), `a summary item about documents in: ${JSON.stringify(texts)}`).toBeTruthy();
  79  |   });
  80  | 
  81  |   test(...tc('VAL-V02'), async ({ pages, page }) => {
  82  |     await reviewWithMissingDocuments(pages);
  83  |     const urlBefore = page.url();
  84  |     const titleBefore = await pages.review.stepTitle();
  85  |     await pages.review.validation.clickItem(0);
  86  |     await expect.poll(async () => page.url() !== urlBefore || (await pages.review.stepTitle()) !== titleBefore, {
  87  |       message: 'clicking a validation item should navigate to the section that owns the error',
  88  |     }).toBe(true);
  89  |   });
  90  | 
  91  |   test(...tc('VAL-V03'), async ({ pages, page }, testInfo) => {
  92  |     await reviewWithMissingDocuments(pages);
  93  |     await test.step('Submit is disabled while errors exist', async () => {
  94  |       await captureEvidence(page, testInfo, 'submit-state-with-errors');
  95  |       await expect(pages.review.submitButton).toBeDisabled();
  96  |     });
  97  |     await test.step('Submit becomes enabled once the errors are resolved', async () => {
  98  |       await page.goto(routes.step(applicationIdFromUrl(page.url()), 'documents')); // the real review page has no Back button
  99  |       await pages.documents.uploadAllRequired(files.validPdf());
  100 |       await pages.documents.next();
  101 |       await expect(pages.review.submitButton).toBeEnabled();
  102 |     });
  103 |   });
  104 | });
  105 | 
```