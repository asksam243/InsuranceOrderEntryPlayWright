# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\beneficiaries.spec.js >> Beneficiary Management >> TC-BEN-V10 At least one primary beneficiary is mandatory @regression @beneficiary @p2
- Location: tests\ui\beneficiaries.spec.js:121:3

# Error details

```
Error: still on the same step

still on the same step

expect(received).toBe(expected) // Object.is equality

Expected: "beneficiaries|Beneficiaries"
Received: "documents|Upload Document"

Call Log:
- Timeout 8000ms exceeded while waiting on the predicate
```

# Page snapshot

```yaml
- generic [active] [ref=f8e1]:
  - navigation [ref=f8e2]:
    - generic [ref=f8e3]:
      - link "Insurance Order Entry Demo Platform QA Automation Training App" [ref=f8e4] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/dashboard
        - generic [aria-hidden] [ref=f8e5]: IO
        - generic [ref=f8e6]:
          - generic [ref=f8e7]: Insurance Order Entry Demo Platform
          - generic [ref=f8e8]: QA Automation Training App
      - generic [ref=f8e9]:
        - list [ref=f8e10]:
          - listitem [ref=f8e11]:
            - link "Dashboard" [ref=f8e12] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/dashboard
          - listitem [ref=f8e13]:
            - link "Applications" [ref=f8e14] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications
          - listitem [ref=f8e15]:
            - link "Products" [ref=f8e16] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/products
          - listitem [ref=f8e17]:
            - link "Support" [ref=f8e18] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/support
        - generic [ref=f8e19]:
          - link "Learner Agent 001" [ref=f8e20] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/profile
          - button "Logout" [ref=f8e22] [cursor=pointer]
  - main [ref=f8e23]:
    - generic [ref=f8e25]:
      - link "← Back to Beneficiaries" [ref=f8e26] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/115/beneficiaries
      - link "Application Summary" [ref=f8e27] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/115
    - generic [ref=f8e28]:
      - generic [ref=f8e31]:
        - heading "Upload Document" [level=1] [ref=f8e32]
        - generic [ref=f8e33]:
          - generic [ref=f8e34]:
            - generic [ref=f8e35]: Document Type
            - combobox [ref=f8e36]:
              - option "KYC_ID" [selected]
              - option "ADDRESS_PROOF"
              - option "INCOME_PROOF"
              - option "OTHER"
          - generic [ref=f8e37]:
            - generic [ref=f8e38]: Upload File
            - button "Choose File" [ref=f8e39] [cursor=pointer]
          - generic [ref=f8e40]:
            - generic [ref=f8e41]: Simulated File Name
            - textbox "simulated-upload.pdf" [ref=f8e42]
          - button "Upload Document" [ref=f8e43] [cursor=pointer]
      - generic [ref=f8e46]:
        - heading "Uploaded Documents" [level=2] [ref=f8e47]
        - table [ref=f8e49]:
          - rowgroup [ref=f8e50]:
            - row [ref=f8e51]:
              - columnheader "Type" [ref=f8e52]
              - columnheader "File" [ref=f8e53]
              - columnheader "Size KB" [ref=f8e54]
              - columnheader "Status" [ref=f8e55]
              - columnheader [ref=f8e56]
          - rowgroup [ref=f8e57]:
            - row [ref=f8e58]:
              - cell "No documents uploaded." [ref=f8e59]
        - link "Continue to Review" [ref=f8e60] [cursor=pointer]:
          - /url: http://34.93.84.61:8081/applications/115/review
  - contentinfo [ref=f8e61]:
    - generic [ref=f8e62]:
      - generic [ref=f8e63]: TalentFarm QA Automation Lab
      - generic [ref=f8e64]: Insurance Order Entry Demo
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