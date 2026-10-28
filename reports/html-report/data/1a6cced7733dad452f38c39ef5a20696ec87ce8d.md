# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\client-kyc-sensitive.spec.js >> Client / KYC - sensitive data >> TC-CLI-V10 PEP = Yes makes additional details mandatory @regression @client @p2 @sensitive
- Location: tests\ui\client-kyc-sensitive.spec.js:57:3

# Error details

```
Error: still on the same step

still on the same step

expect(received).toBe(expected) // Object.is equality

Expected: "kyc-financial|KYC, Financial, and Compliance"
Received: "product|Product & Policy Configuration"

Call Log:
- Timeout 8000ms exceeded while waiting on the predicate
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
    - alert [ref=f5e24]: KYC, financial, and compliance information saved.
    - generic [ref=f5e26]:
      - link "← Back to KYC & Financial" [ref=f5e27] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/150/kyc-financial
      - link "Application Summary" [ref=f5e28] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/150
    - generic [ref=f5e29]:
      - generic [ref=f5e31]:
        - generic [ref=f5e32]: "Application #150"
        - heading "Product & Policy Configuration" [level=1] [ref=f5e33]
        - paragraph [ref=f5e34]: Select the product, sum assured, premium payment frequency, premium payment term, and coverage term.
      - generic [ref=f5e37]:
        - generic [ref=f5e38]:
          - generic [ref=f5e39]:
            - generic [ref=f5e40]: Product
            - combobox "Product" [ref=f5e41]:
              - option "Select product" [selected]
              - option "Elite Legacy Whole Life"
              - option "FlexiPay Whole Life"
              - option "SecureLife Whole Life"
              - option "WealthBuilder Whole Life"
          - generic [ref=f5e42]:
            - generic [ref=f5e43]: Sum Assured
            - spinbutton "Sum Assured" [ref=f5e44]
          - generic [ref=f5e45]:
            - generic [ref=f5e46]: Premium Payment Frequency
            - combobox "Premium Payment Frequency" [ref=f5e47]:
              - option "Monthly" [selected]
              - option "Quarterly"
              - option "Semi-Annual"
              - option "Annual"
          - generic [ref=f5e48]:
            - generic [ref=f5e49]: Premium Payment Term
            - combobox "Premium Payment Term" [ref=f5e50]:
              - option "Select term" [selected]
              - option "10 years"
              - option "15 years"
              - option "20 years"
              - option "25 years"
              - option "30 years"
          - generic [ref=f5e51]:
            - generic [ref=f5e52]: Coverage Term
            - combobox "Coverage Term" [ref=f5e53]:
              - option "Whole Life" [selected]
              - option "To Age 100"
        - generic [ref=f5e55]:
          - generic [ref=f5e56]: Estimated Total Modal Premium
          - generic [ref=f5e57]: Pending
          - generic [ref=f5e58]: Select a product to estimate premium.
        - button "Save and Continue" [ref=f5e60] [cursor=pointer]
  - contentinfo [ref=f5e61]:
    - generic [ref=f5e62]:
      - generic [ref=f5e63]: TalentFarm QA Automation Lab
      - generic [ref=f5e64]: Insurance Order Entry Demo
```

# Test source

```ts
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
> 174 |     await expect.poll(() => this.stepTitle(), { message: 'still on the same step' }).toBe(titleBefore);
      |                                                                                      ^ Error: still on the same step
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