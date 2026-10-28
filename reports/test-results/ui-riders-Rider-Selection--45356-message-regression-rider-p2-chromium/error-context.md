# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\riders.spec.js >> Rider Selection >> TC-RIDER-V04 Maximum rider count enforced with message @regression @rider @p2
- Location: tests\ui\riders.spec.js:53:3

# Error details

```
Error: expected a visible message matching /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i

expect(locator).toBeVisible() failed

Locator: getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i }).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - expected a visible message matching /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i }).first() with timeout 8000ms
  - waiting for getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i }).first()

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
    - /url: http://34.93.84.61:8081/applications/145/product
  - link "Application Summary":
    - /url: http://34.93.84.61:8081/applications/145
  - text: "Application #145"
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
          - checkbox [checked]
        - cell "Accidental Death Benefit Rider"
        - cell "Pays additional benefit if death is due to accident."
        - cell:
          - spinbutton "$50,000": "250000"
      - row "Permanent Disability Rider Provides lump sum or income on total permanent disability.":
        - cell:
          - checkbox [checked]
        - cell "Permanent Disability Rider"
        - cell "Provides lump sum or income on total permanent disability."
        - cell:
          - spinbutton "$50,000": "250000"
      - row "Term Rider Add-on Additional term coverage layered on top of the Whole Life base product.":
        - cell:
          - checkbox [checked]
        - cell "Term Rider Add-on"
        - cell "Additional term coverage layered on top of the Whole Life base product."
        - cell:
          - spinbutton "$50,000": "250000"
      - row "Critical Illness Rider Pays lump sum on diagnosis of covered critical illness.":
        - cell:
          - checkbox [checked]
        - cell "Critical Illness Rider"
        - cell "Pays lump sum on diagnosis of covered critical illness."
        - cell:
          - spinbutton "$50,000": "250000"
      - row "Hospital Cash Rider Pays daily cash benefit during hospitalization.":
        - cell:
          - checkbox [checked]
        - cell "Hospital Cash Rider"
        - cell "Pays daily cash benefit during hospitalization."
        - cell:
          - spinbutton "$50,000": "250000"
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
  161 |     if (pattern) await expect(err).toHaveText(pattern);
  162 |   }
  163 | 
  164 |   /** Any visible validation / alert text matching the pattern, anywhere on the page. */
  165 |   async expectErrorText(pattern) {
  166 |     await expect(
  167 |       this.$$(S.common.anyError).filter({ hasText: pattern }).first(),
  168 |       `expected a visible message matching ${pattern}`,
> 169 |     ).toBeVisible();
      |       ^ Error: expected a visible message matching /(maximum|more than|no more than|at most).*(4|four)|maximum|max|limit|no more than/i
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