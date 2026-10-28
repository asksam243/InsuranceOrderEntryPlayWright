# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\riders.spec.js >> Rider Selection >> TC-RIDER-V06 Critical illness rider triggers health questionnaire @regression @rider @p2
- Location: tests\ui\riders.spec.js:89:3

# Error details

```
Error: expect(locator).toBeVisible() failed

Locator: getByTestId('health-questionnaire').or(locator('[data-testid="health-questionnaire"], form.health-questionnaire, [role="dialog"]')).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - Expect "toBeVisible" getByTestId('health-questionnaire').or(locator('[data-testid="health-questionnaire"], form.health-questionnaire, [role="dialog"]')).first() with timeout 8000ms
  - waiting for getByTestId('health-questionnaire').or(locator('[data-testid="health-questionnaire"], form.health-questionnaire, [role="dialog"]')).first()

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
  - alert: Product configuration saved and premium recalculated.
  - link "← Back to Product Configuration":
    - /url: http://34.93.84.61:8081/applications/146/product
  - link "Application Summary":
    - /url: http://34.93.84.61:8081/applications/146
  - text: "Application #146"
  - heading "Riders" [level=1]
  - paragraph: Select optional rider benefits for the policy.
  - text: "Current rider premium: $0.00"
  - table:
    - rowgroup:
      - row "Select Rider Description Benefit Amount":
        - columnheader "Select"
        - columnheader "Rider"
        - columnheader "Description"
        - columnheader "Benefit Amount"
    - rowgroup:
      - row "Accidental Death Benefit Rider Pays additional benefit if death is due to accident.":
        - cell:
          - checkbox
        - cell "Accidental Death Benefit Rider"
        - cell "Pays additional benefit if death is due to accident."
        - cell:
          - spinbutton "$50,000"
      - row "Permanent Disability Rider Provides lump sum or income on total permanent disability.":
        - cell:
          - checkbox
        - cell "Permanent Disability Rider"
        - cell "Provides lump sum or income on total permanent disability."
        - cell:
          - spinbutton "$50,000"
      - row "Term Rider Add-on Additional term coverage layered on top of the Whole Life base product.":
        - cell:
          - checkbox
        - cell "Term Rider Add-on"
        - cell "Additional term coverage layered on top of the Whole Life base product."
        - cell:
          - spinbutton "$50,000"
      - row "Critical Illness Rider Pays lump sum on diagnosis of covered critical illness.":
        - cell:
          - checkbox [checked]
        - cell "Critical Illness Rider"
        - cell "Pays lump sum on diagnosis of covered critical illness."
        - cell:
          - spinbutton "$50,000": "250000"
      - row "Hospital Cash Rider Pays daily cash benefit during hospitalization.":
        - cell:
          - checkbox
        - cell "Hospital Cash Rider"
        - cell "Pays daily cash benefit during hospitalization."
        - cell:
          - spinbutton "$50,000"
      - row "Waiver of Premium - Disability Waives future premiums if insured becomes totally disabled.":
        - cell:
          - checkbox
        - cell "Waiver of Premium - Disability"
        - cell "Waives future premiums if insured becomes totally disabled."
        - cell:
          - spinbutton "$50,000"
      - row "Waiver of Premium - Critical Illness Waives future premiums upon diagnosis of covered critical illness.":
        - cell:
          - checkbox
        - cell "Waiver of Premium - Critical Illness"
        - cell "Waives future premiums upon diagnosis of covered critical illness."
        - cell:
          - spinbutton "$50,000"
      - row "Family Income Benefit Rider Provides monthly income to family for a defined period after insured death.":
        - cell:
          - checkbox
        - cell "Family Income Benefit Rider"
        - cell "Provides monthly income to family for a defined period after insured death."
        - cell:
          - spinbutton "$50,000"
      - row "Guaranteed Income Rider Provides guaranteed periodic income for a set duration.":
        - cell:
          - checkbox
        - cell "Guaranteed Income Rider"
        - cell "Provides guaranteed periodic income for a set duration."
        - cell:
          - spinbutton "$50,000"
  - button "Save and Continue"
- contentinfo: TalentFarm QA Automation Lab Insurance Order Entry Demo
```

# Test source

```ts
  1   | const { test, tc, expect, env } = require('../../fixtures');
  2   | const M = require('../../config/messages');
  3   | const { dobForAge } = require('../../utils/dates');
  4   | const { buildClient } = require('../../utils/dataBuilder');
  5   | const { progressTo, finishFrom } = require('../../utils/flows');
  6   | const { captureEvidence } = require('../../utils/assertions');
  7   | 
  8   | const r = env.rules;
  9   | const adb = r.patterns.riderAdb;
  10  | 
  11  | test.describe('Rider Selection', () => {
  12  |   test.use({ agentRole: 'learnerAgent' });
  13  | 
  14  |   const needRider = async (pages, pattern, label) => {
  15  |     test.skip(!(await pages.rider.cardFor(pattern).count()), `No ${label} rider offered in this environment`);
  16  |   };
  17  | 
  18  |   test(...tc('RIDER-V01'), async ({ pages }, testInfo) => {
  19  |     const { data } = await progressTo(pages, 'riders');
  20  |     await needRider(pages, adb, 'ADB');
  21  |     await pages.rider.add(adb, data.product.faceValue);
  22  |     await pages.rider.saveAndReopen(); // the rider premium summary is calculated on save, not while ticking
  23  |     expect(await pages.rider.isAdded(adb), 'the rider is still selected after saving').toBe(true);
  24  |     try {
  25  |       await expect.poll(() => pages.rider.riderPremiumSummary(), { message: 'rider premium in the summary' }).toBeGreaterThan(0);
  26  |     } catch (e) {
  27  |       // Attach exactly what the page showed, so the cause (no summary element, a zero premium, a different label) is visible in the report.
  28  |       await testInfo.attach('rider-premium-diagnostics', { body: await pages.rider.premiumDiagnostics(), contentType: 'text/plain' });
  29  |       throw e;
  30  |     }
  31  |   });
  32  | 
  33  |   test(...tc('RIDER-V02'), async ({ pages, page }, testInfo) => {
  34  |     const { data } = await progressTo(pages, 'riders');
  35  |     await needRider(pages, adb, 'ADB');
  36  |     await pages.rider.add(adb);
  37  |     await pages.rider.setCoverage(adb, data.product.faceValue + 1);
  38  |     await pages.rider.next(); // the rule is enforced on Save & Continue
  39  |     await captureEvidence(page, testInfo, 'rider-coverage-above-face-value');
  40  |     await pages.rider.expectErrorText(M.riderExceeds);
  41  |   });
  42  | 
  43  |   test(...tc('RIDER-V03'), async ({ pages }) => {
  44  |     test.skip(!r.patterns.riderAgeRestricted, 'Set RIDER_AGE_RESTRICTED_PATTERN to run (Q15)');
  45  |     await progressTo(pages, 'riders', { client: buildClient({ dob: dobForAge(64) }) });
  46  |     const pattern = r.patterns.riderAgeRestricted;
  47  |     await needRider(pages, pattern, 'age-restricted');
  48  |     if (await pages.rider.isDisabled(pattern)) return; // disabled == correctly blocked
  49  |     await pages.rider.add(pattern);
  50  |     await pages.rider.expectErrorText(M.eligibility);
  51  |   });
  52  | 
  53  |   test(...tc('RIDER-V04'), async ({ pages }) => {
  54  |     test.skip(r.maxRiders === null, 'Set MAX_RIDERS to run (Q15)');
  55  |     await progressTo(pages, 'riders');
  56  |     // Pick riders that cannot trip OTHER rules (waiver riders are mutually exclusive; some riders are age-restricted),
  57  |     // so the only rule that can refuse the extra rider is the maximum count.
  58  |     const n = await pages.rider.cards.count();
  59  |     const usable = [];
  60  |     for (let i = 0; i < n; i += 1) {
  61  |       const text = (await pages.rider.cards.nth(i).innerText()) || '';
  62  |       if (/waiver/i.test(text) || (r.patterns.riderAgeRestricted && r.patterns.riderAgeRestricted.test(text))) continue;
  63  |       usable.push(i);
  64  |     }
  65  |     test.skip(usable.length <= r.maxRiders, `Only ${usable.length} non-exclusive rider(s) offered; need more than MAX_RIDERS=${r.maxRiders}`);
  66  |     for (const i of usable.slice(0, r.maxRiders)) await pages.rider.addAt(i);
  67  |     const extra = pages.rider.toggleAt(usable[r.maxRiders]);
  68  |     if (await extra.isDisabled()) return; // disabled == correctly blocked
  69  |     await pages.rider.addAt(usable[r.maxRiders]);
  70  |     await pages.rider.expectErrorText(M.riderMax);
  71  |   });
  72  | 
  73  |   test(...tc('RIDER-V05'), async ({ pages, page }, testInfo) => {
  74  |     const { riderWaiverA: waiverA, riderWaiverB: waiverB } = r.patterns;
  75  |     test.skip(!waiverA || !waiverB, 'Set RIDER_WAIVER_A_PATTERN and RIDER_WAIVER_B_PATTERN to run (Q15)');
  76  |     await progressTo(pages, 'riders');
  77  |     await needRider(pages, waiverA, 'waiver A');
  78  |     await needRider(pages, waiverB, 'waiver B');
  79  |     await pages.rider.add(waiverA);
  80  |     if (!(await pages.rider.isDisabled(waiverB))) {
  81  |       await pages.rider.add(waiverB).catch(() => {});
  82  |       await pages.rider.expectErrorText(M.riderExclusive);
  83  |     }
  84  |     await captureEvidence(page, testInfo, 'exclusive-waiver-riders');
  85  |     const both = (await pages.rider.isAdded(waiverA)) && (await pages.rider.isAdded(waiverB));
  86  |     expect(both, 'mutually exclusive waiver riders must not both be selected').toBe(false);
  87  |   });
  88  | 
  89  |   test(...tc('RIDER-V06'), async ({ pages }) => {
  90  |     await progressTo(pages, 'riders');
  91  |     const ci = r.patterns.riderCriticalIllness;
  92  |     await needRider(pages, ci, 'critical illness');
  93  |     await pages.rider.add(ci);
> 94  |     await expect(pages.rider.questionnaire).toBeVisible();
      |                                             ^ Error: expect(locator).toBeVisible() failed
  95  |   });
  96  | 
  97  |   test(...tc('RIDER-V07'), async ({ pages, page }, testInfo) => {
  98  |     const { data } = await progressTo(pages, 'riders');
  99  |     await needRider(pages, adb, 'ADB');
  100 |     await pages.rider.add(adb, data.product.faceValue);
  101 |     await pages.rider.next();
  102 |     await finishFrom(pages, 'beneficiaries', data);
  103 |     // The review snapshot itemises Base Policy Premium, Rider Premium and Total Modal Premium (live finding).
  104 |     await captureEvidence(page, testInfo, 'rider-premium-itemised');
  105 |     const { base, rider, total } = await pages.review.premiumBreakdown();
  106 |     expect(base, 'base premium on review').toBeGreaterThan(0);
  107 |     expect(rider, 'rider premium itemised on review').toBeGreaterThan(0);
  108 |     expect(total, 'total = base + rider premium').toBeCloseTo(base + rider, 2);
  109 |   });
  110 | });
  111 | 
```