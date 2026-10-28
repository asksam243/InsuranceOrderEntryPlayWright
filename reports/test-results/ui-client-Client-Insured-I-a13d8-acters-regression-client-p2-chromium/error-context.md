# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\client.spec.js >> Client / Insured Information >> TC-CLI-V14 Name validation rejects digits and special characters @regression @client @p2
- Location: tests\ui\client.spec.js:134:3

# Error details

```
Error: still on the same step

still on the same step

expect(received).toBe(expected) // Object.is equality

Expected: "client|Client / Insured Information"
Received: "address-contact|Address and Contact Information"

Call Log:
- Timeout 8000ms exceeded while waiting on the predicate
```

# Page snapshot

```yaml
- generic [active] [ref=f3e1]:
  - navigation [ref=f3e2]:
    - generic [ref=f3e3]:
      - link "Insurance Order Entry Demo Platform QA Automation Training App" [ref=f3e4] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/dashboard
        - generic [aria-hidden] [ref=f3e5]: IO
        - generic [ref=f3e6]:
          - generic [ref=f3e7]: Insurance Order Entry Demo Platform
          - generic [ref=f3e8]: QA Automation Training App
      - generic [ref=f3e9]:
        - list [ref=f3e10]:
          - listitem [ref=f3e11]:
            - link "Dashboard" [ref=f3e12] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/dashboard
          - listitem [ref=f3e13]:
            - link "Applications" [ref=f3e14] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/applications
          - listitem [ref=f3e15]:
            - link "Products" [ref=f3e16] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/products
          - listitem [ref=f3e17]:
            - link "Support" [ref=f3e18] [cursor=pointer]:
              - /url: http://34.93.84.61:8081/support
        - generic [ref=f3e19]:
          - link "Learner Agent 001" [ref=f3e20] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/profile
          - button "Logout" [ref=f3e22] [cursor=pointer]
  - main [ref=f3e23]:
    - alert [ref=f3e24]: Client information saved.
    - generic [ref=f3e26]:
      - link "← Back to Client Information" [ref=f3e27] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/126/client
      - link "Application Summary" [ref=f3e28] [cursor=pointer]:
        - /url: http://34.93.84.61:8081/applications/126
    - generic [ref=f3e29]:
      - generic [ref=f3e30]:
        - heading "Address and Contact Information" [level=1] [ref=f3e31]
        - paragraph [ref=f3e32]: US address, ZIP, phone, and email details.
      - generic [ref=f3e33]:
        - generic [ref=f3e34]:
          - strong [ref=f3e36]: Residential Address
          - generic [ref=f3e38]:
            - generic [ref=f3e39]:
              - generic [ref=f3e40]: Street Address *
              - textbox "123 Main Street" [ref=f3e41]
            - generic [ref=f3e42]:
              - generic [ref=f3e43]: Apt / Suite
              - textbox "Apt 4B" [ref=f3e44]
            - generic [ref=f3e45]:
              - generic [ref=f3e46]: City *
              - textbox "Austin" [ref=f3e47]
            - generic [ref=f3e48]:
              - generic [ref=f3e49]: State *
              - combobox [ref=f3e50]:
                - option "Select state" [selected]
                - option "Alabama (AL)"
                - option "Alaska (AK)"
                - option "Arizona (AZ)"
                - option "Arkansas (AR)"
                - option "California (CA)"
                - option "Colorado (CO)"
                - option "Connecticut (CT)"
                - option "Delaware (DE)"
                - option "District of Columbia (DC)"
                - option "Florida (FL)"
                - option "Georgia (GA)"
                - option "Hawaii (HI)"
                - option "Idaho (ID)"
                - option "Illinois (IL)"
                - option "Indiana (IN)"
                - option "Iowa (IA)"
                - option "Kansas (KS)"
                - option "Kentucky (KY)"
                - option "Louisiana (LA)"
                - option "Maine (ME)"
                - option "Maryland (MD)"
                - option "Massachusetts (MA)"
                - option "Michigan (MI)"
                - option "Minnesota (MN)"
                - option "Mississippi (MS)"
                - option "Missouri (MO)"
                - option "Montana (MT)"
                - option "Nebraska (NE)"
                - option "Nevada (NV)"
                - option "New Hampshire (NH)"
                - option "New Jersey (NJ)"
                - option "New Mexico (NM)"
                - option "New York (NY)"
                - option "North Carolina (NC)"
                - option "North Dakota (ND)"
                - option "Ohio (OH)"
                - option "Oklahoma (OK)"
                - option "Oregon (OR)"
                - option "Pennsylvania (PA)"
                - option "Rhode Island (RI)"
                - option "South Carolina (SC)"
                - option "South Dakota (SD)"
                - option "Tennessee (TN)"
                - option "Texas (TX)"
                - option "Utah (UT)"
                - option "Vermont (VT)"
                - option "Virginia (VA)"
                - option "Washington (WA)"
                - option "West Virginia (WV)"
                - option "Wisconsin (WI)"
                - option "Wyoming (WY)"
            - generic [ref=f3e51]:
              - generic [ref=f3e52]: ZIP Code *
              - textbox "73301" [ref=f3e53]
              - generic [ref=f3e54]: Use 12345 or 12345-6789.
        - generic [ref=f3e55]:
          - generic [ref=f3e56]:
            - strong [ref=f3e57]: Mailing Address
            - generic [ref=f3e58]:
              - checkbox "Same as residential" [ref=f3e59]
              - generic [ref=f3e60]: Same as residential
          - generic [ref=f3e63]:
            - generic [ref=f3e64]:
              - generic [ref=f3e65]: Street Address
              - textbox "PO Box or street address" [ref=f3e66]
            - generic [ref=f3e67]:
              - generic [ref=f3e68]: Apt / Suite
              - textbox "Suite 200" [ref=f3e69]
            - generic [ref=f3e70]:
              - generic [ref=f3e71]: City
              - textbox "Dallas" [ref=f3e72]
            - generic [ref=f3e73]:
              - generic [ref=f3e74]: State
              - combobox [ref=f3e75]:
                - option "Select state" [selected]
                - option "Alabama (AL)"
                - option "Alaska (AK)"
                - option "Arizona (AZ)"
                - option "Arkansas (AR)"
                - option "California (CA)"
                - option "Colorado (CO)"
                - option "Connecticut (CT)"
                - option "Delaware (DE)"
                - option "District of Columbia (DC)"
                - option "Florida (FL)"
                - option "Georgia (GA)"
                - option "Hawaii (HI)"
                - option "Idaho (ID)"
                - option "Illinois (IL)"
                - option "Indiana (IN)"
                - option "Iowa (IA)"
                - option "Kansas (KS)"
                - option "Kentucky (KY)"
                - option "Louisiana (LA)"
                - option "Maine (ME)"
                - option "Maryland (MD)"
                - option "Massachusetts (MA)"
                - option "Michigan (MI)"
                - option "Minnesota (MN)"
                - option "Mississippi (MS)"
                - option "Missouri (MO)"
                - option "Montana (MT)"
                - option "Nebraska (NE)"
                - option "Nevada (NV)"
                - option "New Hampshire (NH)"
                - option "New Jersey (NJ)"
                - option "New Mexico (NM)"
                - option "New York (NY)"
                - option "North Carolina (NC)"
                - option "North Dakota (ND)"
                - option "Ohio (OH)"
                - option "Oklahoma (OK)"
                - option "Oregon (OR)"
                - option "Pennsylvania (PA)"
                - option "Rhode Island (RI)"
                - option "South Carolina (SC)"
                - option "South Dakota (SD)"
                - option "Tennessee (TN)"
                - option "Texas (TX)"
                - option "Utah (UT)"
                - option "Vermont (VT)"
                - option "Virginia (VA)"
                - option "Washington (WA)"
                - option "West Virginia (WV)"
                - option "Wisconsin (WI)"
                - option "Wyoming (WY)"
            - generic [ref=f3e76]:
              - generic [ref=f3e77]: ZIP Code
              - textbox "75201" [ref=f3e78]
        - generic [ref=f3e79]:
          - strong [ref=f3e81]: Contact Information
          - generic [ref=f3e83]:
            - generic [ref=f3e84]:
              - generic [ref=f3e85]: Primary Email *
              - textbox "name@example.com" [ref=f3e86]
            - generic [ref=f3e87]:
              - generic [ref=f3e88]: Mobile Phone *
              - textbox "(212) 555-1212" [ref=f3e89]
            - generic [ref=f3e90]:
              - generic [ref=f3e91]: Alternate Phone
              - textbox "312-555-1212" [ref=f3e92]
            - generic [ref=f3e93]:
              - generic [ref=f3e94]: Preferred Contact Mode *
              - combobox [ref=f3e95]:
                - option "Select mode" [selected]
                - option "Email"
                - option "Phone"
                - option "Postal Mail"
        - generic [ref=f3e96]:
          - link "Back" [ref=f3e97] [cursor=pointer]:
            - /url: http://34.93.84.61:8081/applications/126/client
          - button "Save and Continue" [ref=f3e98] [cursor=pointer]
  - contentinfo [ref=f3e99]:
    - generic [ref=f3e100]:
      - generic [ref=f3e101]: TalentFarm QA Automation Lab
      - generic [ref=f3e102]: Insurance Order Entry Demo
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