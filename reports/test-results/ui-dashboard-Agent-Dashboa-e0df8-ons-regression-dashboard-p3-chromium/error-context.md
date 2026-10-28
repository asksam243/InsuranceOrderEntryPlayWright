# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: ui\dashboard.spec.js >> Agent Dashboard >> TC-DASH-V07 Dashboard search returns matching applications @regression @dashboard @p3
- Location: tests\ui\dashboard.spec.js:43:3

# Error details

```
TimeoutError: locator.fill: Timeout 10000ms exceeded.
Call log:
  - waiting for getByTestId('dashboard-search').or(getByLabel(/search/i)).or(getByRole('searchbox')).or(getByPlaceholder(/search/i)).first()

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
  2   | const { BasePage } = require('./BasePage');
  3   | const { S } = require('../config/selectors');
  4   | const { loc } = require('../utils/locators');
  5   | const routes = require('../config/routes');
  6   | 
  7   | /** Extracts the application id from URLs like /applications/123/client or /application/ABC-1/edit. */
  8   | function applicationIdFromUrl(url) {
  9   |   const m = new URL(url).pathname.match(/applications?\/(?!new\b|create\b)([A-Za-z0-9_-]+)/i);
  10  |   return m ? m[1] : null;
  11  | }
  12  | 
  13  | class DashboardPage extends BasePage {
  14  |   async goto() {
  15  |     await this.page.goto(routes.dashboard);
  16  |     await this.expectLoaded();
  17  |   }
  18  | 
  19  |   async expectLoaded() {
  20  |     await expect(this.page).toHaveURL(/dashboard/);
  21  |     await expect(this.newApplicationControl).toBeVisible();
  22  |   }
  23  | 
  24  |   get newApplicationControl() {
  25  |     return loc(this.page, S.dashboard.newApplication).or(loc(this.page, S.dashboard.newApplicationBtn)).first();
  26  |   }
  27  | 
  28  |   /**
  29  |    * Dashboard -> Start New Application -> Create Draft -> client form. Returns the application id.
  30  |    * The real app has an intermediate "start" page with a Create Draft button (the missing step that stalled every UI flow
  31  |    * in the first smoke run); builds that go straight to the client form are tolerated.
  32  |    */
  33  |   async startNewApplication() {
  34  |     await this.newApplicationControl.click();
  35  |     const createDraft = this.$(S.dashboard.createDraft);
  36  |     const clientForm = this.$(S.client.firstName);
  37  |     await expect(createDraft.or(clientForm), 'the Create Draft page or the client form').toBeVisible();
  38  |     if (await createDraft.isVisible()) await createDraft.click();
  39  |     await this.page.waitForURL(/\/applications\/\d+\/client/);
  40  |     await expect(clientForm).toBeVisible();
  41  |     return applicationIdFromUrl(this.page.url());
  42  |   }
  43  | 
  44  |   get rows() {
  45  |     return this.$$(S.dashboard.rows);
  46  |   }
  47  | 
  48  |   rowFor(text) {
  49  |     return this.rows.filter({ hasText: text }).first();
  50  |   }
  51  | 
  52  |   /** Row for an application: matches the client name, the id as text, or the row's own "open" link (application-open-<id>). */
  53  |   rowForApplication({ name, id } = {}) {
  54  |     let rows = this.rows.filter({ hasText: name || '\u0000never' });
  55  |     if (id) {
  56  |       rows = rows
  57  |         .or(this.rows.filter({ hasText: String(id) }))
  58  |         .or(this.rows.filter({ has: this.page.getByTestId(`${S.dashboard.openPrefix}${id}`) }));
  59  |     }
  60  |     return rows.first();
  61  |   }
  62  | 
  63  |   /** Application id from the row's open link (application-open-<id>), its own testid, or its first link href; or null. */
  64  |   async rowId(row) {
  65  |     const open = row.locator(`[data-testid^="${S.dashboard.openPrefix}"]`).first();
  66  |     if (await open.count()) {
  67  |       const tid = await open.getAttribute('data-testid');
  68  |       return tid.slice(S.dashboard.openPrefix.length);
  69  |     }
  70  |     const own = await row.getAttribute('data-testid');
  71  |     if (own && own.startsWith(S.dashboard.rowPrefix)) return own.slice(S.dashboard.rowPrefix.length);
  72  |     const href = await row.locator('a').first().getAttribute('href').catch(() => null);
  73  |     const m = href && href.match(/applications?\/([A-Za-z0-9_-]+)/i);
  74  |     return m ? m[1] : null;
  75  |   }
  76  | 
  77  |   statusOf(row) {
  78  |     return row.locator(S.dashboard.statusCell.css).first();
  79  |   }
  80  | 
  81  |   /** Lower-cased status text of every visible row. */
  82  |   async statuses() {
  83  |     const n = await this.rows.count();
  84  |     const out = [];
  85  |     for (let i = 0; i < n; i += 1) {
  86  |       out.push(((await this.statusOf(this.rows.nth(i)).textContent()) || '').trim().toLowerCase());
  87  |     }
  88  |     return out;
  89  |   }
  90  | 
  91  |   async filterByStatus(status) {
  92  |     await this.choose(S.dashboard.statusFilter, status);
  93  |     await this.page.waitForLoadState('networkidle');
  94  |   }
  95  | 
  96  |   async search(text) {
> 97  |     await this.$(S.dashboard.search).fill(text);
      |                                      ^ TimeoutError: locator.fill: Timeout 10000ms exceeded.
  98  |     await this.$(S.dashboard.search).press('Enter');
  99  |     await this.page.waitForLoadState('networkidle');
  100 |   }
  101 | 
  102 |   /** Opens an application row (resume a draft). */
  103 |   async resume(row) {
  104 |     const open = row.locator(`[data-testid^="${S.dashboard.openPrefix}"]`).first();
  105 |     if (await open.count()) {
  106 |       await open.click();
  107 |       return;
  108 |     }
  109 |     const link = row.locator('a, button').filter({ hasText: /resume|continue|open|edit/i }).first();
  110 |     if (await link.count()) await link.click();
  111 |     else await row.click();
  112 |   }
  113 | 
  114 |   async logout() {
  115 |     await this.$(S.common.logout).click();
  116 |   }
  117 | }
  118 | 
  119 | module.exports = { DashboardPage, applicationIdFromUrl };
  120 | 
```