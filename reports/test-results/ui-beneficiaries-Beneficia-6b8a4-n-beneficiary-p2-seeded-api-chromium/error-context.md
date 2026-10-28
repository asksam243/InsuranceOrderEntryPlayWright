# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\beneficiaries.spec.js >> Beneficiary Management >> TC-BEN-V08 Duplicate beneficiary (Name + DOB + Relationship) blocked @regression @beneficiary @p2 @seeded @api
- Location: tests\ui\beneficiaries.spec.js:100:3

# Error details

```
Error: expected a visible message matching /duplicate|already (added|exists)|same beneficiary/i

expect(locator).toBeVisible() failed

Locator: getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /duplicate|already (added|exists)|same beneficiary/i }).first()
Expected: visible
Timeout: 8000ms
Error: element(s) not found

Call log:
  - expected a visible message matching /duplicate|already (added|exists)|same beneficiary/i getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /duplicate|already (added|exists)|same beneficiary/i }).first() with timeout 8000ms
  - waiting for getByTestId('validation-error-alert').or(locator('[data-testid="validation-error-alert"], [data-testid="beneficiary-error-summary"], [data-testid="review-validation-errors"], .field-error, .invalid-feedback, .text-danger, [role="alert"]')).filter({ hasText: /duplicate|already (added|exists)|same beneficiary/i }).first()

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
  - alert: Beneficiary saved.
  - link "← Back to Riders":
    - /url: http://34.93.84.61:8081/applications/113/riders
  - link "Application Summary":
    - /url: http://34.93.84.61:8081/applications/113
  - text: "Application #113"
  - heading "Beneficiaries" [level=1]
  - paragraph: Add or update primary and secondary beneficiaries for the policy.
  - link "Back to Application":
    - /url: http://34.93.84.61:8081/applications/113
  - text: "Primary allocation: 100.00% | Secondary allocation: 0.00%"
  - strong: Existing Beneficiaries
  - table:
    - rowgroup:
      - row "Level Type Name Designation Relationship Age Allocation Email Phone Action":
        - columnheader "Level"
        - columnheader "Type"
        - columnheader "Name"
        - columnheader "Designation"
        - columnheader "Relationship"
        - columnheader "Age"
        - columnheader "Allocation"
        - columnheader "Email"
        - columnheader "Phone"
        - columnheader "Action"
    - rowgroup:
      - row "PRIMARY INDIVIDUAL BenHMEGAT PayeeHMEGAT Revocable SPOUSE 34 50.00% - - Edit Remove":
        - cell "PRIMARY"
        - cell "INDIVIDUAL"
        - cell "BenHMEGAT PayeeHMEGAT"
        - cell "Revocable"
        - cell "SPOUSE"
        - cell "34"
        - cell "50.00%"
        - cell "-"
        - cell "-"
        - cell "Edit Remove":
          - link "Edit":
            - /url: http://34.93.84.61:8081/applications/113/beneficiaries?edit=75
          - button "Remove"
      - row "PRIMARY INDIVIDUAL BenHMEGAT PayeeHMEGAT Revocable SPOUSE 34 50.00% - - Edit Remove":
        - cell "PRIMARY"
        - cell "INDIVIDUAL"
        - cell "BenHMEGAT PayeeHMEGAT"
        - cell "Revocable"
        - cell "SPOUSE"
        - cell "34"
        - cell "50.00%"
        - cell "-"
        - cell "-"
        - cell "Edit Remove":
          - link "Edit":
            - /url: http://34.93.84.61:8081/applications/113/beneficiaries?edit=76
          - button "Remove"
  - strong: Add Beneficiary
  - text: Beneficiary Level *
  - combobox:
    - option "Select" [selected]
    - option "Primary"
    - option "Secondary"
  - text: Beneficiary Type *
  - combobox:
    - option "Individual" [selected]
    - option "Trust"
    - option "Organization"
  - text: Relationship *
  - combobox:
    - option "Select" [selected]
    - option "Spouse"
    - option "Child"
    - option "Parent"
    - option "Sibling"
    - option "Trust"
    - option "Organization"
    - option "Other"
  - text: Allocation % *
  - spinbutton: "100"
  - text: Beneficiary Designation *
  - combobox:
    - option "Revocable" [selected]
    - option "Irrevocable"
  - text: Irrevocable beneficiaries cannot be changed or removed in this demo without beneficiary consent. Phone
  - textbox "(212) 555-1212"
  - text: Email
  - textbox
  - text: Country
  - textbox: US
  - strong: Individual Beneficiary Details
  - text: First Name *
  - textbox
  - text: Middle Name
  - textbox
  - text: Last Name *
  - textbox
  - text: Date of Birth *
  - textbox
  - text: Gender
  - combobox:
    - option "Select" [selected]
    - option "Male"
    - option "Female"
    - option "Non-binary"
  - strong: Address Details
  - text: Address Line 1
  - textbox
  - text: City
  - textbox
  - text: State
  - textbox
  - text: Postal Code
  - textbox
  - strong: Minor Beneficiary Guardian Details
  - text: Guardian Name
  - textbox
  - text: Guardian Relationship
  - textbox
  - text: Guardian Contact
  - textbox
  - text: Guardian Address
  - textbox
  - checkbox "Legal acknowledgement completed for minor beneficiary"
  - text: Legal acknowledgement completed for minor beneficiary
  - link "Back":
    - /url: http://34.93.84.61:8081/applications/113/riders
  - button "Save Beneficiary"
  - link "Continue":
    - /url: http://34.93.84.61:8081/applications/113/documents
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
      |       ^ Error: expected a visible message matching /duplicate|already (added|exists)|same beneficiary/i
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