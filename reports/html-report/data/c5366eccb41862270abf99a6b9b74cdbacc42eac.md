# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\dashboard.spec.js >> Agent Dashboard >> TC-DASH-V05 Status filters (Draft/Submitted/Approved) return correct rows @regression @dashboard @p2
- Location: tests\ui\dashboard.spec.js:31:3

# Error details

```
TimeoutError: locator.evaluate: Timeout 10000ms exceeded.
Call log:
  - waiting for getByTestId('dashboard-status-filter').or(getByLabel(/status/i)).first()

```

# Page snapshot

```yaml
- generic [active] [ref=e1]:
  - navigation [ref=e2]:
    - generic [ref=e3]:
      - link "Insurance Order Entry Demo Platform QA Automation Training App" [ref=e4] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/dashboard
        - generic [aria-hidden] [ref=e5]: IO
        - generic [ref=e6]:
          - generic [ref=e7]: Insurance Order Entry Demo Platform
          - generic [ref=e8]: QA Automation Training App
      - generic [ref=e9]:
        - list [ref=e10]:
          - listitem [ref=e11]:
            - link "Dashboard" [ref=e12] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/dashboard
          - listitem [ref=e13]:
            - link "Applications" [ref=e14] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications
          - listitem [ref=e15]:
            - link "Products" [ref=e16] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/products
          - listitem [ref=e17]:
            - link "Support" [ref=e18] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/support
        - generic [ref=e19]:
          - link "Valid Agent" [ref=e20] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/profile
          - button "Logout" [ref=e22] [cursor=pointer]
  - main [ref=e23]:
    - generic [ref=e24]:
      - generic [ref=e25]:
        - heading "Agent Dashboard" [level=1] [ref=e26]
        - paragraph [ref=e27]: Track drafts, submitted applications, and policy order entry work.
      - link "Start New Application" [ref=e28] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/new
    - generic [ref=e29]:
      - generic [ref=e32]:
        - generic [ref=e33]: Draft
        - generic [ref=e34]: "9"
      - generic [ref=e37]:
        - generic [ref=e38]: Submitted
        - generic [ref=e39]: "2"
      - generic [ref=e42]:
        - generic [ref=e43]: Under Review
        - generic [ref=e44]: "0"
      - generic [ref=e47]:
        - generic [ref=e48]: Approved
        - generic [ref=e49]: "1"
      - generic [ref=e52]:
        - generic [ref=e53]: Requires Info
        - generic [ref=e54]: "0"
    - generic [ref=e55]:
      - generic [ref=e56]:
        - heading "Recent Applications" [level=2] [ref=e57]
        - link "View all" [ref=e58] [cursor=pointer]:
          - /url: http://34.93.84.61:8081/applications
      - table [ref=e60]:
        - rowgroup [ref=e61]:
          - row [ref=e62]:
            - columnheader "Reference" [ref=e63]
            - columnheader "Client" [ref=e64]
            - columnheader "Product" [ref=e65]
            - columnheader "Status" [ref=e66]
            - columnheader "Updated" [ref=e67]
            - columnheader [ref=e68]
        - rowgroup [ref=e69]:
          - row [ref=e70]:
            - 'cell "Draft #128" [ref=e71]'
            - cell "QaDAFCHUGV TesterDAFCHUGVBE" [ref=e72]
            - cell "Not selected" [ref=e73]
            - cell "DRAFT" [ref=e74]
            - cell "28 Oct 2026" [ref=e76]
            - cell [ref=e77]:
              - link "Open" [ref=e78] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/128
          - row [ref=e79]:
            - 'cell "Draft #49" [ref=e80]'
            - cell "New Applicant" [ref=e81]
            - cell "Not selected" [ref=e82]
            - cell "DRAFT" [ref=e83]
            - cell "14 Oct 2026" [ref=e85]
            - cell [ref=e86]:
              - link "Open" [ref=e87] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/49
          - row [ref=e88]:
            - 'cell "Draft #44" [ref=e89]'
            - cell "Test#$# Insured" [ref=e90]
            - cell "Elite Legacy Whole Life" [ref=e91]
            - cell "DRAFT" [ref=e92]
            - cell "04 Jun 2026" [ref=e94]
            - cell [ref=e95]:
              - link "Open" [ref=e96] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/44
          - row [ref=e97]:
            - cell "WL2026060255444" [ref=e98]
            - cell "Test Application" [ref=e99]
            - cell "Elite Legacy Whole Life" [ref=e100]
            - cell "SUBMITTED" [ref=e101]
            - cell "02 Jun 2026" [ref=e103]
            - cell [ref=e104]:
              - link "Open" [ref=e105] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/43
          - row [ref=e106]:
            - 'cell "Draft #42" [ref=e107]'
            - cell [ref=e108]
            - cell "Not selected" [ref=e109]
            - cell "DRAFT" [ref=e110]
            - cell "02 Jun 2026" [ref=e112]
            - cell [ref=e113]:
              - link "Open" [ref=e114] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/42
          - row [ref=e115]:
            - 'cell "Draft #41" [ref=e116]'
            - cell [ref=e117]
            - cell "Not selected" [ref=e118]
            - cell "DRAFT" [ref=e119]
            - cell "17 May 2026" [ref=e121]
            - cell [ref=e122]:
              - link "Open" [ref=e123] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/41
          - row [ref=e124]:
            - 'cell "Draft #40" [ref=e125]'
            - cell [ref=e126]
            - cell "Not selected" [ref=e127]
            - cell "DRAFT" [ref=e128]
            - cell "17 May 2026" [ref=e130]
            - cell [ref=e131]:
              - link "Open" [ref=e132] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/40
          - row [ref=e133]:
            - 'cell "Draft #39" [ref=e134]'
            - cell "Test Name" [ref=e135]
            - cell "Guaranteed Return Whole Life" [ref=e136]
            - cell "DRAFT" [ref=e137]
            - cell "04 Jun 2026" [ref=e139]
            - cell [ref=e140]:
              - link "Open" [ref=e141] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/39
          - row [ref=e142]:
            - 'cell "Draft #38" [ref=e143]'
            - cell "Sudarsan Thyagarajan" [ref=e144]
            - cell "Not selected" [ref=e145]
            - cell "DRAFT" [ref=e146]
            - cell "17 May 2026" [ref=e148]
            - cell [ref=e149]:
              - link "Open" [ref=e150] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/38
          - row [ref=e151]:
            - 'cell "Draft #37" [ref=e152]'
            - cell "Sudarsan Thyagarajan" [ref=e153]
            - cell "Elite Legacy Whole Life" [ref=e154]
            - cell "DRAFT" [ref=e155]
            - cell "17 May 2026" [ref=e157]
            - cell [ref=e158]:
              - link "Open" [ref=e159] [cursor=pointer]:
                - /url: http://34.93.84.61:8081/applications/37
  - contentinfo [ref=e160]:
    - generic [ref=e161]:
      - generic [ref=e162]: TalentFarm QA Automation Lab
      - generic [ref=e163]: Insurance Order Entry Demo
```

# Test source

```ts
  1   | const { expect } = require('@playwright/test');
  2   | const env = require('../config/env');
  3   | const { S } = require('../config/selectors');
  4   | const { loc, byPrefix } = require('../utils/locators');
  5   | const { formatDate } = require('../utils/dates');
  6   | const { escapeRegex } = require('../utils/parse');
  7   | const { disableBrowserValidation, isNativelyInvalid } = require('../utils/browser');
  8   | 
  9   | /**
  10  |  * The real app has no generic "Next" button: every step has its own Save & Continue control (FROM MARKUP).
  11  |  * Keyed by the last URL segment of /applications/:id/<step>.
  12  |  */
  13  | const STEP_CONTINUE = {
  14  |   client: 'client-save-continue-button',
  15  |   'address-contact': 'address-contact-save-continue-button',
  16  |   'kyc-financial': 'kyc-financial-save-continue-button',
  17  |   product: 'product-save-continue-button',
  18  |   riders: 'rider-save-continue-button',
  19  |   beneficiaries: 'beneficiary-continue-button',
  20  |   documents: 'documents-continue-review-button',
  21  | };
  22  | 
  23  | /**
  24  |  * Shared behaviour for every screen. Page objects expose USER ACTIONS and read-only getters;
  25  |  * the test files own the assertions (small reusable state checks live here as expect* helpers).
  26  |  */
  27  | class BasePage {
  28  |   constructor(page) {
  29  |     this.page = page;
  30  |   }
  31  | 
  32  |   /** First element matching a selector definition (testid, with role/label fallbacks). */
  33  |   $(def) {
  34  |     return loc(this.page, def).first();
  35  |   }
  36  |   /** All elements matching a selector definition. */
  37  |   $$(def) {
  38  |     return loc(this.page, def);
  39  |   }
  40  |   byPrefix(prefix) {
  41  |     return byPrefix(this.page, prefix);
  42  |   }
  43  | 
  44  |   async goto(path) {
  45  |     await this.page.goto(path);
  46  |   }
  47  | 
  48  |   async fillField(def, value) {
  49  |     if (value === undefined || value === null) return;
  50  |     await this.$(def).fill(String(value));
  51  |   }
  52  | 
  53  |   /**
  54  |    * Selects an option. Playwright matches a plain string against the option VALUE or its visible LABEL, which covers both
  55  |    * the app's enum values (MALE) and readable text (Male); falls back to a partial text match, then the first real option.
  56  |    */
  57  |   async choose(def, value) {
  58  |     if (value === undefined || value === null) return;
  59  |     const el = this.$(def);
> 60  |     const tag = await el.evaluate((n) => n.tagName.toLowerCase());
      |                          ^ TimeoutError: locator.evaluate: Timeout 10000ms exceeded.
  61  |     if (tag !== 'select') {
  62  |       await el.fill(String(value));
  63  |       return;
  64  |     }
  65  |     for (const attempt of [String(value), { label: String(value) }]) {
  66  |       try {
  67  |         await el.selectOption(attempt, { timeout: 1500 });
  68  |         return;
  69  |       } catch {
  70  |         /* try next strategy */
  71  |       }
  72  |     }
  73  |     const options = await el.locator('option').evaluateAll((os) =>
  74  |       os.map((o) => ({ v: o.value, t: (o.textContent || '').trim() })).filter((o) => o.v),
  75  |     );
  76  |     const pattern = new RegExp(escapeRegex(value), 'i');
  77  |     const match = options.find((o) => pattern.test(o.t) || pattern.test(o.v)) || options[0];
  78  |     if (!match) throw new Error(`No selectable option found for ${JSON.stringify(def.id)} (wanted "${value}")`);
  79  |     await el.selectOption(match.v);
  80  |   }
  81  | 
  82  |   /** Types a Date into a date input in the app's configured format, then blurs to trigger age/validation logic. */
  83  |   async setDate(def, date) {
  84  |     const el = this.$(def);
  85  |     await el.fill(formatDate(date, env.dateFormat));
  86  |     await el.press('Tab');
  87  |   }
  88  | 
  89  |   async setChecked(def, checked) {
  90  |     const el = this.$(def);
  91  |     if (checked) await el.check();
  92  |     else await el.uncheck();
  93  |   }
  94  | 
  95  |   /** Slug of the current application step ("client", "address-contact", ...), or "" outside an application. */
  96  |   stepSlug() {
  97  |     const m = new URL(this.page.url()).pathname.match(/\/applications\/[^/]+\/([a-z-]+)/i);
  98  |     return m ? m[1] : '';
  99  |   }
  100 | 
  101 |   /** The Save & Continue control of the current step (falls back to a generic Next / Continue button). */
  102 |   continueControl() {
  103 |     const id = STEP_CONTINUE[this.stepSlug()];
  104 |     const generic = loc(this.page, S.common.next);
  105 |     return (id ? this.page.getByTestId(id).or(generic) : generic).first();
  106 |   }
  107 | 
  108 |   /** Saves the current step and moves on. `ignoreBrowserValidation` reaches the SERVER-side messages for blank forms. */
  109 |   async next({ ignoreBrowserValidation = false } = {}) {
  110 |     if (ignoreBrowserValidation) await disableBrowserValidation(this.page);
  111 |     await this.continueControl().click();
  112 |     await this.page.waitForLoadState('domcontentloaded');
  113 |   }
  114 | 
  115 |   async back() {
  116 |     await this.$(S.common.back).click();
  117 |   }
  118 | 
  119 |   /**
  120 |    * There is NO "Save draft" button in the real app: the draft is created at the start page and saved by each
  121 |    * Save & Continue. If a build does have a dedicated button it is used; otherwise Save & Continue persists the draft.
  122 |    */
  123 |   async saveDraft() {
  124 |     const explicit = this.$$(S.common.saveDraft);
  125 |     if (await explicit.count()) {
  126 |       await explicit.first().click();
  127 |       await this.page.waitForLoadState('domcontentloaded');
  128 |       return;
  129 |     }
  130 |     await this.next();
  131 |   }
  132 | 
  133 |   /** Identifies the current step: URL step slug + first heading. Changes when the browser moves on. */
  134 |   async stepTitle() {
  135 |     const heading = await this.$$(S.common.stepTitle).first().textContent({ timeout: 3000 }).catch(() => '');
  136 |     return `${this.stepSlug()}|${(heading || '').trim()}`;
  137 |   }
  138 | 
  139 |   async expectStep(pattern) {
  140 |     await expect.poll(() => this.stepTitle(), { message: `step to match ${pattern}` }).toMatch(pattern);
  141 |   }
  142 | 
  143 |   /** Error element belonging to a field: <testid>-error first, then an error node inside the field's wrapper. */
  144 |   fieldError(def) {
  145 |     const field = this.$(def);
  146 |     return this.page
  147 |       .getByTestId(`${def.id}-error`)
  148 |       .or(field.locator('xpath=ancestor::div[1]').locator(S.common.anyError.css))
  149 |       .first();
  150 |   }
  151 | 
  152 |   /**
  153 |    * A field is "flagged" when the app shows an error for it OR the browser itself refuses it. The real forms use HTML
  154 |    * `required`, so a blank mandatory field is blocked by the browser (:invalid) before the server can answer.
  155 |    */
  156 |   async expectFieldError(def, pattern) {
  157 |     const field = this.$(def);
  158 |     if (!pattern && (await field.count()) && (await isNativelyInvalid(field).catch(() => false))) return;
  159 |     const err = this.fieldError(def);
  160 |     await expect(err, `expected a validation error next to "${def.id}"`).toBeVisible();
```