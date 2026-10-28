# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: e2e\workflow.spec.js >> Submission & Status Tracking >> TC-WF-V02 Draft resumed with previously saved data intact @regression @workflow @p2 @seeded
- Location: tests\e2e\workflow.spec.js:32:3

# Error details

```
TimeoutError: locator.click: Timeout 10000ms exceeded.
Call log:
  - waiting for getByTestId('step-back').or(getByRole('button', { name: /^(back|previous)/i })).first()

```

# Page snapshot

```yaml
- generic [active] [ref=f5e1]:
  - navigation [ref=f5e2]:
    - generic [ref=f5e3]:
      - link "Insurance Order Entry Demo Platform QA Automation Training App" [ref=f5e4] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/dashboard
        - generic [aria-hidden] [ref=f5e5]: IO
        - generic [ref=f5e6]:
          - generic [ref=f5e7]: Insurance Order Entry Demo Platform
          - generic [ref=f5e8]: QA Automation Training App
      - generic [ref=f5e9]:
        - list [ref=f5e10]:
          - listitem [ref=f5e11]:
            - link "Dashboard" [ref=f5e12] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/dashboard
          - listitem [ref=f5e13]:
            - link "Applications" [ref=f5e14] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications
          - listitem [ref=f5e15]:
            - link "Products" [ref=f5e16] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/products
          - listitem [ref=f5e17]:
            - link "Support" [ref=f5e18] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/support
        - generic [ref=f5e19]:
          - link "Learner Agent 001" [ref=f5e20] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/profile
          - button "Logout" [ref=f5e22] [cursor=pointer]
  - main [ref=f5e23]:
    - generic [ref=f5e25]:
      - link "← Back" [ref=f5e26] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications
      - link "Application Summary" [ref=f5e27] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/100
    - generic [ref=f5e28]:
      - generic [ref=f5e30]:
        - generic [ref=f5e31]: "Application #100"
        - heading "Application Summary" [level=1] [ref=f5e32]
        - paragraph [ref=f5e33]: Review the current application state and continue the order entry workflow.
      - generic [ref=f5e34]:
        - generic [ref=f5e37]:
          - heading "Snapshot" [level=2] [ref=f5e38]
          - generic [ref=f5e39]:
            - term [ref=f5e40]: Client
            - definition [ref=f5e41]: QaVDAJCYEG TesterVDAJCYEGRG
            - term [ref=f5e42]: Product
            - definition [ref=f5e43]: Pending
            - term [ref=f5e44]: Sum Assured
            - definition [ref=f5e45]: Pending
            - term [ref=f5e46]: Total Modal Premium
            - definition [ref=f5e47]: $0.00
            - term [ref=f5e48]: Beneficiaries
            - definition [ref=f5e49]: "0"
            - term [ref=f5e50]: Documents
            - definition [ref=f5e51]: "0"
            - term [ref=f5e52]: Status
            - definition [ref=f5e53]: DRAFT
        - generic [ref=f5e56]:
          - heading "Continue Workflow" [level=2] [ref=f5e57]
          - generic [ref=f5e58]:
            - link "Client Information" [ref=f5e59] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/client
            - link "Address & Contact" [ref=f5e60] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/address-contact
            - link "KYC & Financial" [ref=f5e61] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/kyc-financial
            - link "Product & Policy Configuration" [ref=f5e62] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/product
            - link "Riders" [ref=f5e63] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/riders
            - link "Beneficiaries" [ref=f5e64] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/beneficiaries
            - link "Documents" [ref=f5e65] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/documents
            - link "Review Application" [ref=f5e66] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications/100/review
  - contentinfo [ref=f5e67]:
    - generic [ref=f5e68]:
      - generic [ref=f5e69]: TalentFarm QA Automation Lab
      - generic [ref=f5e70]: Insurance Order Entry Demo
```

# Test source

```ts
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
  60  |     const tag = await el.evaluate((n) => n.tagName.toLowerCase());
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
> 116 |     await this.$(S.common.back).click();
      |                                 ^ TimeoutError: locator.click: Timeout 10000ms exceeded.
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
  161 |     if (pattern) await expect(err).toHaveText(pattern);
  162 |   }
  163 | 
  164 |   /** Any visible validation / alert text matching the pattern, anywhere on the page. */
  165 |   async expectErrorText(pattern) {
  166 |     await expect(
  167 |       this.$$(S.common.anyError).filter({ hasText: pattern }).first(),
  168 |       `expected a visible message matching ${pattern}`,
  169 |     ).toBeVisible();
  170 |   }
  171 | 
  172 |   /** The user was NOT moved on: the step identity is unchanged after a rejected Save & Continue. */
  173 |   async expectStillOnStep(titleBefore) {
  174 |     await expect.poll(() => this.stepTitle(), { message: 'still on the same step' }).toBe(titleBefore);
  175 |   }
  176 | 
  177 |   async expectAdvanced(titleBefore) {
  178 |     await expect.poll(() => this.stepTitle(), { timeout: 10_000, message: 'moved to another step' }).not.toBe(titleBefore);
  179 |   }
  180 | 
  181 |   async getValue(def) {
  182 |     return this.$(def).inputValue();
  183 |   }
  184 | }
  185 | 
  186 | module.exports = { BasePage, STEP_CONTINUE };
  187 | 
```