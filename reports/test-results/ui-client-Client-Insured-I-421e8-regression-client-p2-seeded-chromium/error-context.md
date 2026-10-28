# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\client.spec.js >> Client / Insured Information >> TC-CLI-V13 Calculated age shown on review matches the date of birth @regression @client @p2 @seeded
- Location: tests\ui\client.spec.js:125:3

# Error details

```
Error: a client born exactly 35 years ago today (1991-10-28) should show age 35

expect(received).toBe(expected) // Object.is equality

Expected: 35
Received: 36
```

# Page snapshot

```yaml
- generic [active] [ref=f11e1]:
  - navigation [ref=f11e2]:
    - generic [ref=f11e3]:
      - link "Insurance Order Entry Demo Platform QA Automation Training App" [ref=f11e4] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/dashboard
        - generic [aria-hidden] [ref=f11e5]: IO
        - generic [ref=f11e6]:
          - generic [ref=f11e7]: Insurance Order Entry Demo Platform
          - generic [ref=f11e8]: QA Automation Training App
      - generic [ref=f11e9]:
        - list [ref=f11e10]:
          - listitem [ref=f11e11]:
            - link "Dashboard" [ref=f11e12] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/dashboard
          - listitem [ref=f11e13]:
            - link "Applications" [ref=f11e14] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications
          - listitem [ref=f11e15]:
            - link "Products" [ref=f11e16] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/products
          - listitem [ref=f11e17]:
            - link "Support" [ref=f11e18] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/support
        - generic [ref=f11e19]:
          - link "Learner Agent 001" [ref=f11e20] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/profile
          - button "Logout" [ref=f11e22] [cursor=pointer]
  - main [ref=f11e23]:
    - generic [ref=f11e25]:
      - link "← Back to Documents" [ref=f11e26] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/125/documents
      - link "Application Summary" [ref=f11e27] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/125
    - generic [ref=f11e28]:
      - generic [ref=f11e30]:
        - generic [ref=f11e31]: "Application #125"
        - heading "Review Application" [level=1] [ref=f11e32]
        - paragraph [ref=f11e33]: Review the application details and resolve any blocking validation errors before submission.
      - generic [ref=f11e34]:
        - generic [ref=f11e37]:
          - heading "Submission Validation" [level=2] [ref=f11e38]
          - generic [ref=f11e39]: No blocking validation errors found.
          - generic [ref=f11e40]:
            - link "Back to Documents" [ref=f11e41] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/125/documents
            - button "Run Validation" [ref=f11e42] [cursor=pointer]
          - button "Submit Application" [ref=f11e44] [cursor=pointer]
        - generic [ref=f11e47]:
          - heading "Application Snapshot" [level=2] [ref=f11e48]
          - generic [ref=f11e49]:
            - term [ref=f11e50]: Client
            - definition [ref=f11e51]: QaBHVAMAGS TesterBHVAMAGSCJ
            - term [ref=f11e52]: Calculated Age
            - definition [ref=f11e53]: "36"
            - term [ref=f11e54]: Product
            - definition [ref=f11e55]: SecureLife Whole Life
            - term [ref=f11e56]: Sum Assured
            - definition [ref=f11e57]: $250,000.00
            - term [ref=f11e58]: Premium Payment Frequency
            - definition [ref=f11e59]: MONTHLY
            - term [ref=f11e60]: Premium Payment Term
            - definition [ref=f11e61]: 20 years
            - term [ref=f11e62]: Coverage Term
            - definition [ref=f11e63]: WHOLE_LIFE
            - term [ref=f11e64]: Base Policy Premium
            - definition [ref=f11e65]: $98.96
            - term [ref=f11e66]: Rider Premium
            - definition [ref=f11e67]: $0.00
            - term [ref=f11e68]: Total Modal Premium
            - definition [ref=f11e69]: $98.96
            - term [ref=f11e70]: Status
            - definition [ref=f11e71]: DRAFT
  - contentinfo [ref=f11e72]:
    - generic [ref=f11e73]:
      - generic [ref=f11e74]: TalentFarm QA Automation Lab
      - generic [ref=f11e75]: Insurance Order Entry Demo
```

# Test source

```ts
  31  | 
  32  |   test(...tc('CLI-V03'), async ({ pages, page }, testInfo) => {
  33  |     const { data } = await progressTo(pages, 'client');
  34  |     const before = await pages.client.stepTitle();
  35  |     await pages.client.fill({ ...data.client, dob: dobForAge(18, { dayOffset: 1 }) }); // turns 18 TOMORROW => age 17
  36  |     await test.step('age 17 is rejected', async () => {
  37  |       await pages.client.next();
  38  |       await expectBlocked(pages.client, before, M.dobUnderAge);
  39  |       await captureEvidence(page, testInfo, 'age-17-rejected');
  40  |     });
  41  |     await test.step(`age 18 is ${inclusive ? 'accepted' : 'rejected'} (inclusive=${inclusive})`, async () => {
  42  |       await pages.client.setDob(dobForAge(18));
  43  |       await pages.client.next();
  44  |       if (inclusive) await expectAdvanced(pages.client, before);
  45  |       else await expectBlocked(pages.client, before, M.dobUnderAge);
  46  |     });
  47  |   });
  48  | 
  49  |   test(...tc('CLI-V04'), async ({ pages, page }, testInfo) => {
  50  |     const { data } = await progressTo(pages, 'client');
  51  |     const before = await pages.client.stepTitle();
  52  |     await pages.client.fill({ ...data.client, dob: dobForAge(66) });
  53  |     await test.step('age 66 is rejected', async () => {
  54  |       await pages.client.next();
  55  |       await expectBlocked(pages.client, before, M.dobOverAge);
  56  |       await captureEvidence(page, testInfo, 'age-66-rejected');
  57  |     });
  58  |     await test.step(`age 65 is ${inclusive ? 'accepted' : 'rejected'} (inclusive=${inclusive})`, async () => {
  59  |       await pages.client.setDob(dobForAge(65));
  60  |       await pages.client.next();
  61  |       if (inclusive) await expectAdvanced(pages.client, before);
  62  |       else await expectBlocked(pages.client, before, M.dobOverAge);
  63  |     });
  64  |   });
  65  | 
  66  |   test(...tc('CLI-V05'), async ({ pages, page }, testInfo) => {
  67  |     const { data } = await progressTo(pages, 'client');
  68  |     const before = await pages.client.stepTitle();
  69  |     await pages.client.fill(data.client);
  70  |     for (const [label, date] of [['tomorrow', futureDate(1)], ['5 years ahead', futureDate(1825)]]) {
  71  |       await test.step(`future DOB (${label}) is rejected`, async () => {
  72  |         await pages.client.setDob(date);
  73  |         await pages.client.next();
  74  |         await expectBlocked(pages.client, before, M.dobFuture);
  75  |         await captureEvidence(page, testInfo, `future-dob-${label.replace(/\s/g, '-')}`);
  76  |       });
  77  |     }
  78  |   });
  79  | 
  80  |   test(...tc('CLI-V06'), async ({ pages }) => {
  81  |     await progressTo(pages, 'address');
  82  |     const a = buildAddress();
  83  |     await pages.address.fillResidential(a);
  84  |     await pages.address.setChecked(S.address.sameAsResidential, true);
  85  |     const mailing = await pages.address.mailingValues();
  86  |     expect(mailing).toEqual({ line1: a.line1, city: a.city, zip: a.zip });
  87  |   });
  88  | 
  89  |   test(...tc('CLI-V07'), async ({ pages }) => {
  90  |     await progressTo(pages, 'address');
  91  |     const before = await pages.address.stepTitle();
  92  |     const good = buildAddress();
  93  |     await pages.address.fillResidential(good);
  94  |     const bad = [
  95  |       ['email', 'plainaddress'], ['email', 'missing-domain@'], ['email', 'two@@example.test'], ['email', 'with space@example.test'],
  96  |       ['phone', 'abcdefghij'], ['phone', '123'],
  97  |     ];
  98  |     for (const [field, value] of bad) {
  99  |       await test.step(`invalid ${field} "${value}" is rejected`, async () => {
  100 |         await pages.address.fillContact({ ...good, [field]: value });
  101 |         await pages.address.next();
  102 |         await expectBlocked(pages.address, before, field === 'email' ? M.email : M.phone);
  103 |       });
  104 |     }
  105 |   });
  106 | 
  107 | 
  108 | 
  109 | 
  110 |   test(...tc('CLI-V11'), async ({ pages }) => {
  111 |     await progressTo(pages, 'address');
  112 |     const before = await pages.address.stepTitle();
  113 |     const good = buildAddress();
  114 |     for (const zip of ['ABCDE', '123', '0211000000']) {
  115 |       await test.step(`invalid ZIP "${zip}" is rejected`, async () => {
  116 |         await pages.address.fillResidential({ ...good, zip });
  117 |         await pages.address.fillContact(good);
  118 |         await pages.address.next();
  119 |         await expectBlocked(pages.address, before, M.zip);
  120 |       });
  121 |     }
  122 |   });
  123 | 
  124 | 
  125 |   test(...tc('CLI-V13'), async ({ pages, page }, testInfo) => {
  126 |     // The live app shows "Calculated Age" only in the review snapshot, so the age is read there.
  127 |     const dob = dobForAge(35);
  128 |     await progressTo(pages, 'review', { client: buildClient({ dob }) });
  129 |     const shown = await pages.review.calculatedAge();
  130 |     await testInfo.attach('dob-and-age', { body: `DOB entered: ${formatDate(dob, 'iso')}\nToday (test machine, UTC): ${new Date().toISOString().slice(0, 10)}\nAge shown on review: ${shown}`, contentType: 'text/plain' });
> 131 |     expect(shown, `a client born exactly 35 years ago today (${formatDate(dob, 'iso')}) should show age 35`).toBe(35);
      |                                                                                                              ^ Error: a client born exactly 35 years ago today (1991-10-28) should show age 35
  132 |   });
  133 | 
  134 |   test(...tc('CLI-V14'), async ({ pages }) => {
  135 |     const { data } = await progressTo(pages, 'client');
  136 |     const before = await pages.client.stepTitle();
  137 |     await pages.client.fill(data.client);
  138 |     await test.step('digits in first name are rejected', async () => {
  139 |       await pages.client.fillField(S.client.firstName, 'J0hn123');
  140 |       await pages.client.next();
  141 |       await expectBlocked(pages.client, before, M.name);
  142 |     });
  143 |     await test.step('special characters in last name are rejected', async () => {
  144 |       await pages.client.fillField(S.client.firstName, data.client.firstName);
  145 |       await pages.client.fillField(S.client.lastName, 'O@#$%');
  146 |       await pages.client.next();
  147 |       await expectBlocked(pages.client, before, M.name);
  148 |     });
  149 |   });
  150 | 
  151 |   test(...tc('CLI-V15'), async ({ pages }) => {
  152 |     await progressTo(pages, 'address');
  153 |     const before = await pages.address.stepTitle();
  154 |     await pages.address.fillResidential(buildAddress());
  155 |     await pages.address.fillContact(buildAddress());
  156 |     const state = pages.address.$(S.address.resState);
  157 |     const isSelect = (await state.evaluate((n) => n.tagName.toLowerCase())) === 'select';
  158 |     test.skip(isSelect && !(await state.locator('option[value=""]').count()), 'State control has no empty option to clear it with');
  159 |     if (isSelect) await state.selectOption('');
  160 |     else await state.fill('');
  161 |     await pages.address.next();
  162 |     await expectBlocked(pages.address, before, M.state);
  163 |   });
  164 | });
  165 | 
```