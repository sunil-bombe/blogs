# 1. What is Playwright?
Answer:
Playwright is an open-source end-to-end automation framework developed by Microsoft. It supports Chromium, Firefox, and WebKit using a single API.

# 2. Why Playwright over Selenium?
PlaywrightSeleniumAuto waitsManual waits often neededFasterComparatively slowerMultiple browser contextsRequires separate browser instancesBuilt-in network mockingLimited supportBetter handling of modern SPAsMore configuration neededSupports Chromium, Firefox, WebKitBrowser driver dependent

# 3. Which browsers does Playwright support?
- Chromium
- Firefox
- WebKit
- Google Chrome
- Microsoft Edge
# 4. Difference between Browser, BrowserContext and Page?
Browser

Actual browser instance.
BrowserContext

Incognito session.
Multiple contexts can exist in one browser.
Page
A single browser tab.
```
Browser
   |
   |-- Context1
   |      |
   |      |-- Page1
   |      |-- Page2
   |
   |-- Context2
          |
          |-- Page1
```
# 5. What is auto waiting?
Playwright automatically waits for:

Element attached
Visible
Stable
Enabled
Receives events
Example:

```typescript
 await page.getByRole('button').click();
```
No explicit wait required.

# 6. What are Locators?
Locators are Playwright's recommended way to find elements.

Examples
```typescript
page.locator()

page.getByRole()

page.getByText()

page.getByLabel()

page.getByPlaceholder()

page.getByTestId()
```

# 7. Which locator is preferred?
Priority
```
getByRole()
getByLabel()
getByPlaceholder()
getByText()
getByTestId()
```
CSS/XPath
# 8. Difference between locator() and $
```typescript
locator()
```
Lazy evaluation
Auto wait
Retry
Recommended
```typescript
page.$()
```
Returns ElementHandle
No retry
Deprecated approach
# 9. Difference between fill() and type()
```typescript
fill()
```
Clears textbox first
```typescript
type()
```
Types character by character
# 10. Difference between click() and dblclick()
```typescript
await locator.click();
await locator.dblclick();
```
## Intermediate Questions
# 11. How does Playwright handle synchronization?
Using
```typescript
Auto waiting
expect()
waitForSelector()
waitForURL()
waitForLoadState()
```
# 12. What are different wait methods?
```typescript
waitForSelector()
waitForLoadState()
waitForTimeout()
waitForURL()
waitForEvent()
waitForResponse()
waitForRequest()
```
# 13. Why avoid waitForTimeout()?
- Hard waits
- Slow execution
- Flaky tests
# 14. Difference between waitForSelector() and expect()
```typescript
await page.waitForSelector('#msg');
```
Only waits.
```typescript
await expect(locator).toBeVisible();
```
Waits + verifies.

# 15. How to upload a file?
```typescript
await page.setInputFiles('input', 'sample.pdf');
```
# 16. Handle multiple tabs
```typescript
const pagePromise = context.waitForEvent('page');
await page.click('#open');
const newPage = await pagePromise;
```
# 17. Handle alerts
```typescript
page.on('dialog', async dialog => {
   await dialog.accept();
});
```
# 18. Handle frames
```typescript
const frame =
page.frameLocator('#frame');
await frame.locator('#name').fill('Sunil');
```
# 19. Handle dropdown
```typescript
await locator.selectOption('India');
```
# 20. Handle dynamic elements?
Smart locators
Auto waiting
Relative locators
Retry assertions
Advanced Questions
# 21. Explain Browser Context.
- Each context is an isolated session.
- Useful for
- Parallel execution
- Multiple users
- Incognito sessions
# 22. API Testing in Playwright
```typescript
const request =
await playwright.request.newContext();
const response =
await request.get(url);
```
# 23. Mock API Response
```typescript
await page.route(
'**/users',
route => route.fulfill({
status:200,
body:JSON.stringify(data)
}));
```
# 24. Block Network Calls
```typescript
await page.route(
'**/*.png',
route => route.abort()
);
```
# 25. Capture Screenshot
```typescript
await page.screenshot({
path:'home.png'
});
```
# 26. Record Video
```typescript
use:{
video:'on'
}
```
# 27. Trace Viewer
```typescript
use:{
trace:'on-first-retry'
}
```
Open
```bash
npx playwright show-trace trace.zip
```
# 28. Retry Failed Tests
retries:2
# 29. Parallel Execution
workers:4
# 30. Serial Execution
```typescript
test.describe.configure({
mode:'serial'
});
```
## Framework Questions
# 31. Explain your Playwright framework architecture.
Mention:
- Page Object Model
- Fixtures
- Utilities
- Config
- Test Data
- API Layer
- Reports
- CI/CD
- Logger
# 32. How do you manage test data?
JSON
CSV
Excel
Environment files
33. How do you execute different environments?
Using

.env.dev
.env.qa
.env.stage
.env.prod
34. Which reports have you used?
HTML
Allure
JSON
JUnit
35. CI/CD integration?
Jenkins
GitHub Actions
Azure DevOps
36. How do you handle flaky tests?
Stable locators
Auto waits
Retry
Network mocking
Proper assertions
37. Difference between Fixtures and Hooks?
Hooks

beforeEach()
afterEach()
Fixtures

Become a Medium member
Reusable objects shared across tests.

38. Explain test.describe().
Groups related test cases.

39. Explain test.step().
Improves reporting.

40. Soft Assertion
await expect.soft(locator)
.toBeVisible();
Execution continues even if the assertion fails.

Coding Questions
Reverse string
function reverse(str){
return str.split('').reverse().join('');
}
Find duplicate array elements
const arr=[1,2,2,3,4,4];
const dup=arr.filter(
(item,index)=>
arr.indexOf(item)!==index
);
Count characters
const map={};
for(const c of str){
map[c]=(map[c]||0)+1;
}
Remove duplicates
[...new Set(arr)]
Sort numbers
arr.sort((a,b)=>a-b);
# Scenario-Based Playwright Interview Questions

1. **How would you automate OTP login?**
2. **How would you test file downloads?**
3. **How do you handle CAPTCHA in automation?**
4. **How would you automate infinite scrolling?**
5. **How would you test a table with 10,000 rows?**
6. **How would you test a React application?**
7. **How do you handle Shadow DOM?**
8. **How do you test WebSockets?**
9. **How do you verify emails received after registration?**
10. **How do you debug a flaky Playwright test?**

# 1. How would you automate OTP login?

One-Time Password (OTP) authentication is commonly used as a second factor of authentication. While it is an important feature to test, **reading the actual SMS or email during UI automation is generally not recommended** because it introduces dependencies on external systems, making tests slow and flaky.

The preferred approach is to use test-specific mechanisms provided by the application or backend.

---

## Why Not Read the Actual SMS or Email?

Automating OTP by reading real SMS or email can lead to:

- ❌ Dependency on third-party services
- ❌ Slow and unreliable test execution
- ❌ Network and delivery delays
- ❌ Difficult test maintenance
- ❌ Flaky tests due to external failures

---

## Approach 1: Test Environment Bypass (Recommended ✅)

The best practice is to ask developers to provide test-friendly authentication mechanisms, such as:

- ✅ Static OTP
- ✅ API to fetch the latest OTP
- ✅ Disable OTP validation in the QA environment
- ✅ Test-only authentication endpoint
- ✅ Feature flag to bypass OTP verification

This is the most reliable and maintainable approach for automated testing.

---

## Approach 2: Read OTP from the Database

If the OTP is stored in the database and your test environment allows database access, retrieve it directly.

```typescript
const otp = await getOtpFromDB(phoneNumber);

await page.getByLabel('OTP').fill(otp);
```

---

## Approach 3: Read OTP from Email

If the OTP is sent via email, retrieve it using an email service such as:

- 📧 MailSlurp
- 📧 Gmail API
- 📧 MailHog
- 📧 Mailtrap

Example:

```typescript
const otp = await mailSlurp.getLatestOTP();

await page.getByLabel('OTP').fill(otp);
```

---

## Approach 4: Read OTP from an SMS Service

If the application sends OTPs via SMS, integrate with the SMS provider's API to retrieve the message.

Common providers include:

- 📱 Twilio
- 📱 AWS SNS
- 📱 MessageBird

Example workflow:

```text
Generate OTP
      │
      ▼
SMS Service
      │
      ▼
Retrieve OTP via API
      │
      ▼
Enter OTP in Application
```

---

## What to Validate

When testing OTP authentication, verify:

- ✅ OTP is generated successfully.
- ✅ OTP is delivered through the expected channel.
- ✅ Valid OTP allows successful login.
- ✅ Invalid OTP displays an appropriate error message.
- ✅ Expired OTP is rejected.
- ✅ OTP cannot be reused.
- ✅ Maximum retry attempts are enforced.
- ✅ Resend OTP functionality works correctly.

---

## Best Practices

- ✅ Prefer backend APIs or test hooks over reading real SMS.
- ✅ Keep UI automation independent of third-party services.
- ✅ Use disposable test accounts and test data.
- ✅ Test OTP expiry and invalid OTP scenarios.
- ✅ Validate resend OTP functionality.
- ✅ Avoid hard-coded waits; use event-driven or API-based synchronization.

---

## Interview Tip

> **Avoid automating the actual SMS or email delivery in UI tests because it introduces dependencies on external systems. Instead, use backend APIs, database access, test hooks, or dedicated test endpoints to retrieve or bypass the OTP in QA environments.**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How would you automate OTP login?*

**Answer:**

> "I generally avoid automating OTP by reading the actual SMS or email because it depends on external services and can make tests flaky. The preferred approach is to use a test-specific mechanism, such as a static OTP, a backend API to retrieve the OTP, a test authentication endpoint, or disabling OTP validation in the QA environment. If those options aren't available, I can retrieve the OTP from the database, an email service like MailSlurp or the Gmail API, or an SMS provider such as Twilio. This approach keeps the automation reliable while still validating the application's authentication flow."

# 2. How would you test file downloads?

Playwright provides built-in support for handling file downloads through the **`download`** event. This makes it easy to wait for a download, save the file, and validate its properties.

---

## Download Flow

```text
Click Download Button
        │
        ▼
Wait for Download Event
        │
        ▼
Save the File
        │
        ▼
Validate File
```

---

## Example

Wait for the download event before clicking the download button.

```typescript
const downloadPromise = page.waitForEvent('download');

await page.click('text=Download');

const download = await downloadPromise;

await download.saveAs('downloads/report.pdf');
```

---

## What to Validate

After downloading the file, verify the following:

- ✅ File exists
- ✅ File name
- ✅ File extension
- ✅ File size
- ✅ File content
- ✅ MIME type (if applicable)
- ✅ Download completed successfully

---

## Validate File Name

```typescript
expect(download.suggestedFilename()).toContain('.pdf');
```

---

## Validate File Exists

```typescript
import fs from 'fs';

expect(fs.existsSync('downloads/report.pdf')).toBeTruthy();
```

---

## Validate File Size

```typescript
const stats = fs.statSync('downloads/report.pdf');

expect(stats.size).toBeGreaterThan(0);
```

---

## Validate File Content

For text-based files, read the contents and verify the expected data.

```typescript
const content = fs.readFileSync(
  'downloads/report.pdf'
);

// Perform content validation as needed.
```

> **Note:** For PDF files, you can use a PDF parsing library (such as `pdf-parse`) to extract and verify the text content.

---

## Best Practices

- ✅ Always wait for the `download` event before clicking the download button.
- ✅ Save downloaded files to a dedicated test directory.
- ✅ Validate the file name, extension, and size.
- ✅ Verify the file content whenever possible.
- ✅ Clean up downloaded files after test execution.
- ✅ Avoid fixed delays; rely on Playwright's event handling.

---

## Common Test Scenarios

- Verify the correct file is downloaded.
- Verify the downloaded file has the expected name.
- Verify the correct file extension (`.pdf`, `.csv`, `.xlsx`, etc.).
- Verify the file is not empty.
- Verify the file contains the expected content.
- Verify download behavior for unauthorized users.
- Verify error handling when the download fails.

---

## Interview Tip

> **Always use Playwright's `download` event instead of fixed waits. After the download completes, validate the file's existence, name, extension, size, and content to ensure it was downloaded correctly.**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How would you test file downloads in Playwright?*

**Answer:**

> "Playwright provides a built-in `download` event that allows me to reliably handle file downloads. I first wait for the download event, trigger the download action, and then save the file to a known location. After that, I validate that the file exists, verify its name, extension, and size, and, when applicable, check its contents to ensure the correct file was downloaded. I avoid using hard waits and rely on Playwright's event-based approach for stable and reliable download tests."

# 3. How do you handle CAPTCHA?

CAPTCHA is designed to distinguish humans from automated scripts. Its primary purpose is to **prevent automation**, so attempting to automate CAPTCHA defeats its purpose and is **not considered a best practice** in test automation.

Instead of solving CAPTCHA during automated tests, teams typically use test-specific configurations to bypass or mock its validation in non-production environments.

---

## Why You Shouldn't Automate CAPTCHA

- ❌ CAPTCHA is intentionally built to block automated tools.
- ❌ Automating it makes tests unreliable and difficult to maintain.
- ❌ Production CAPTCHAs should always remain enabled for security.

---

## Recommended Approaches

In QA or test environments, use one of the following approaches:

- ✅ Disable CAPTCHA in the QA environment.
- ✅ Use a test bypass token provided by the application.
- ✅ Whitelist the automation server's IP address.
- ✅ Mock the CAPTCHA validation service.
- ✅ Use feature flags or configuration to skip CAPTCHA during automated tests.

---

## Google reCAPTCHA Test Keys

If the application uses **Google reCAPTCHA**, Google provides **test keys** that always return predictable results in test environments. These keys allow automation without compromising production security.

> **Note:** Test keys should only be used in development or QA environments, never in production.

---

## What to Validate Instead

Rather than testing CAPTCHA solving, verify the application's behavior:

- ✅ CAPTCHA is displayed when expected.
- ✅ Users cannot proceed without completing CAPTCHA (in production or manual testing).
- ✅ Valid CAPTCHA responses allow the request to continue.
- ✅ Invalid or missing CAPTCHA responses display the correct error message.
- ✅ CAPTCHA bypass works correctly in the QA environment.

---

## Best Practices

- ✅ Keep CAPTCHA enabled in production.
- ✅ Bypass or mock CAPTCHA only in test environments.
- ✅ Separate CAPTCHA validation from business logic testing.
- ✅ Focus automation on the application's functionality, not on solving CAPTCHA challenges.
- ✅ Use official test keys where supported.

---

## Interview Tip

> **CAPTCHA itself should not be automated because it is specifically designed to prevent bots. In automated testing, the recommended approach is to bypass or mock CAPTCHA validation in QA environments while keeping it enabled in production.**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How do you handle CAPTCHA in automation?*

**Answer:**

> "I don't automate CAPTCHA because its purpose is to prevent automated access. Instead, in QA environments we typically disable CAPTCHA, use a test bypass token, whitelist the automation server's IP, or mock the CAPTCHA validation service. If the application uses Google reCAPTCHA, Google provides official test keys that can be used for automation in non-production environments. This allows us to validate the application's business functionality without compromising security or creating unstable tests."

# 4. How would you automate infinite scrolling?

Infinite scrolling is a UI pattern where additional content is loaded automatically as the user scrolls down the page. The automation script should continue scrolling until no new content is loaded.

---

## Basic Approach

The general approach is:

1. Scroll to the bottom of the page.
2. Wait for new content to load.
3. Check if the page height has increased.
4. Repeat until the page height no longer changes.

---

## Example

```typescript
let previousHeight = 0;

while (true) {
  const currentHeight = await page.evaluate(() =>
    document.body.scrollHeight
  );

  if (currentHeight === previousHeight) {
    break;
  }

  previousHeight = currentHeight;

  await page.evaluate(() =>
    window.scrollTo(0, document.body.scrollHeight)
  );

  await page.waitForTimeout(1000);
}
```

---

## Better Approach

Instead of using a fixed timeout (`waitForTimeout()`), wait for the network request or API response that loads the next set of data.

```typescript
await Promise.all([
  page.waitForResponse(response =>
    response.url().includes('/products') &&
    response.status() === 200
  ),
  page.evaluate(() =>
    window.scrollTo(0, document.body.scrollHeight)
  )
]);
```

This approach is:

- ✅ Faster
- ✅ More reliable
- ✅ Less flaky
- ✅ Independent of network speed

---

## Alternative Approach

If each scroll loads additional elements, wait until the number of elements increases.

```typescript
const items = page.locator('.product-card');

const initialCount = await items.count();

await page.evaluate(() =>
  window.scrollTo(0, document.body.scrollHeight)
);

await expect(items).toHaveCount(initialCount + 20);
```

---

## What to Validate

When testing infinite scrolling, verify:

- ✅ New content loads after scrolling.
- ✅ No duplicate items are displayed.
- ✅ Items appear in the correct order.
- ✅ Loading indicators appear and disappear correctly.
- ✅ The scroll stops when all data has been loaded.
- ✅ API requests are triggered as expected.
- ✅ Performance remains acceptable with large datasets.

---

## Best Practices

- ✅ Prefer waiting for API responses over fixed delays.
- ✅ Avoid `waitForTimeout()` whenever possible.
- ✅ Verify that newly loaded items are unique.
- ✅ Validate both UI updates and backend responses.
- ✅ Handle scenarios where no more data is available.
- ✅ Use Playwright's built-in waiting mechanisms for better stability.

---

## Interview Tip

> **Avoid using hard waits (`waitForTimeout()`) for infinite scrolling. Instead, wait for the API response or for new elements to appear. This makes tests faster, more reliable, and less flaky.**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How would you automate infinite scrolling in Playwright?*

**Answer:**

> "To automate infinite scrolling, I repeatedly scroll to the bottom of the page and check whether additional content has been loaded by comparing the page height or the number of displayed items. If no new content appears, I stop scrolling. Rather than relying on fixed delays like `waitForTimeout()`, I prefer waiting for the API response or new elements to load using Playwright's built-in waiting mechanisms. I also verify that new items are loaded correctly, there are no duplicates, the loading indicator behaves as expected, and the application stops requesting data once all content has been loaded."

# 5. How would you test a table with 10,000 rows?

Testing every row in a large table is inefficient, time-consuming, and unnecessary. Instead of validating all 10,000 rows through the UI, focus on testing the table's functionality and validate the complete dataset through backend or API testing.

---

## Why Not Validate All Rows?

Validating every row:

- ❌ Increases test execution time
- ❌ Makes tests slow and brittle
- ❌ Provides little additional value
- ❌ Is better suited for API or database validation

---

## What to Test Instead

Focus on the following functionality:

- ✅ Pagination
- ✅ Search functionality
- ✅ Sorting (ascending and descending)
- ✅ Filtering
- ✅ Random sampling of displayed rows
- ✅ Row selection and actions
- ✅ Column visibility and formatting
- ✅ API or database validation for the complete dataset

---

## Example: Validate Visible Rows

Verify that only the expected number of rows is displayed on the current page.

```typescript
const rows = page.locator('table tbody tr');

await expect(rows).toHaveCount(50);
```

For example, if pagination displays **50 rows per page**, verify only those 50 rows.

---

## Test Pagination

Verify that navigating between pages loads the correct data.

```typescript
await page.getByRole('button', { name: 'Next' }).click();

await expect(page.locator('table tbody tr')).toHaveCount(50);
```

---

## Test Search

Search for a known record and verify the results.

```typescript
await page.getByPlaceholder('Search').fill('John Doe');

await expect(page.getByText('John Doe')).toBeVisible();
```

---

## Test Sorting

Verify that data is sorted correctly when clicking a column header.

```typescript
await page.getByRole('columnheader', { name: 'Name' }).click();

// Validate that the displayed rows are sorted correctly.
```

---

## Test Filtering

Apply filters and confirm that only matching records are displayed.

```typescript
await page.getByLabel('Status').selectOption('Active');

await expect(page.getByText('Inactive')).toHaveCount(0);
```

---

## Validate the Backend or API

Instead of validating all UI rows, verify the complete dataset through the API or database.

Example:

```typescript
const response = await page.request.get('/api/users');

expect(response.ok()).toBeTruthy();
```

The backend is the appropriate place to verify:

- Total number of records
- Data integrity
- Missing or duplicate records
- Business rules

---

## Best Practices

- ✅ Validate only the visible rows in the UI.
- ✅ Test pagination, sorting, filtering, and searching.
- ✅ Use random sampling for data verification.
- ✅ Compare selected UI records with API responses.
- ✅ Perform full dataset validation at the API or database layer.
- ✅ Keep UI tests focused on user functionality rather than data volume.

---

## Interview Tip

> **"UI tests should validate representative data and user interactions, while backend or API tests should validate the complete dataset."**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How would you test a table with 10,000 rows?*

**Answer:**

> "I wouldn't validate all 10,000 rows through the UI because it's slow, unnecessary, and better suited for backend validation. Instead, I'd focus on testing the table's functionality, such as pagination, search, sorting, filtering, and row actions. I'd verify that the correct number of rows is displayed per page and use random sampling to compare displayed records with API responses. Finally, I'd validate the complete dataset through the API or database, where checking all records is faster and more reliable. This approach keeps UI tests efficient while ensuring complete data validation at the backend."

# 6. How would you test a React application?

React applications are dynamic and component-based. The UI updates automatically whenever the component state or props change, so tests should focus on user behavior rather than the underlying implementation.

Playwright is well-suited for testing React applications because it provides **auto-waiting**, reliable locators, and built-in assertions that work seamlessly with dynamic UI updates.

---

## Key Areas to Test

When testing a React application, focus on the following:

- ✅ Dynamic DOM updates
- ✅ Component rendering
- ✅ State changes
- ✅ API requests and responses
- ✅ Loading spinners
- ✅ Lazy-loaded components
- ✅ Form validation
- ✅ Navigation and routing
- ✅ Error handling
- ✅ User interactions (clicks, inputs, dropdowns)

---

## Use Stable Locators

Prefer accessibility-based locators because they are more reliable and less likely to break when the UI changes.

```typescript
await page.getByRole('button', { name: 'Login' }).click();

await page.getByLabel('Email').fill('user@example.com');

await page.getByTestId('submit-button').click();
```

---

## Avoid XPath

❌ Avoid XPath whenever possible because React frequently re-renders components, making XPath expressions fragile and difficult to maintain.

```typescript
// Avoid
page.locator('//button[@class="btn"]');
```

Instead, use:

```typescript
page.getByRole('button', { name: 'Submit' });
```

---

## Use Playwright's Auto-Waiting

React updates the DOM asynchronously after state changes or API responses. Instead of using hard waits, rely on Playwright's built-in auto-waiting and assertions.

```typescript
await expect(page.getByText('Welcome')).toBeVisible();
```

Avoid:

```typescript
await page.waitForTimeout(5000);
```

---

## Validate API Calls

Verify that API requests are triggered correctly and the UI updates based on the response.

```typescript
await page.waitForResponse(response =>
  response.url().includes('/users') &&
  response.status() === 200
);
```

---

## Test Loading States

Ensure loading indicators appear while data is being fetched and disappear after the response.

```typescript
await expect(page.getByTestId('loader')).toBeVisible();

await expect(page.getByTestId('loader')).toBeHidden();
```

---

## Test Lazy Loading

Verify that lazy-loaded components are rendered only when required.

```typescript
await page.getByRole('button', { name: 'Load More' }).click();

await expect(page.getByText('Additional Content')).toBeVisible();
```

---

## Best Practices

- ✅ Use accessibility-based locators (`getByRole`, `getByLabel`).
- ✅ Use `getByTestId()` for elements without accessible attributes.
- ✅ Avoid XPath whenever possible.
- ✅ Let Playwright handle synchronization with auto-waiting.
- ✅ Verify UI updates after state changes.
- ✅ Test API success and failure scenarios.
- ✅ Validate loading indicators and error messages.
- ✅ Write tests from the user's perspective rather than testing React internals.

---

## Interview Tip

> **Prefer accessibility-based locators such as `getByRole()` and `getByLabel()` because they are more stable, improve test reliability, and continue to work even when the UI structure changes.**

---

# Interview Summary (2-Minute Answer)

> **Question:** *How would you test a React application?*

**Answer:**

> "When testing a React application, I focus on user-facing functionality such as component rendering, dynamic DOM updates, state changes, API interactions, loading indicators, and lazy-loaded components. Since React updates the DOM asynchronously, I rely on Playwright's built-in auto-waiting and assertions instead of hard waits. I prefer accessibility-based locators like `getByRole()` and `getByLabel()`, and use `getByTestId()` when needed, while avoiding XPath because it's more fragile in React applications. I also validate API responses, loading states, and error scenarios to ensure the application behaves correctly from the user's perspective."

# 7. How do you handle Shadow DOM?

Shadow DOM is a web standard that allows developers to encapsulate the HTML, CSS, and JavaScript of a component. It is commonly used in Web Components to prevent styles and DOM structure from leaking outside the component.

Playwright provides built-in support for **Open Shadow DOM**, allowing you to interact with elements inside it without any additional configuration.

---

## Handling Open Shadow DOM

You can chain locators to access elements inside an open shadow root.

```typescript
await page
  .locator('custom-element')
  .locator('#submit')
  .click();
```

---

## Alternative Syntax

Playwright also supports the `>>` selector syntax for traversing into the Shadow DOM.

```typescript
await page
  .locator('custom-element >> button')
  .click();
```

---

## What to Validate

When testing elements inside a Shadow DOM, verify:

- ✅ Elements are visible and accessible
- ✅ Buttons, inputs, and links are clickable
- ✅ User interactions behave correctly
- ✅ Form inputs accept valid data
- ✅ Validation messages appear as expected
- ✅ UI updates correctly after user actions

---

## Closed Shadow DOM

A **Closed Shadow DOM** cannot be accessed directly by automation tools, including Playwright.

In such cases:

- ❌ You cannot inspect or interact with internal elements.
- ✅ Ask developers to expose **test hooks**, such as:
  - `data-testid`
  - Public methods
  - Test-only APIs
- ✅ Test the component through its **public UI** and verify the expected behavior instead of accessing internal elements.

---

## Best Practices

- ✅ Prefer Playwright's built-in Shadow DOM support.
- ✅ Use reliable locators such as `getByRole()` or `getByTestId()` when available.
- ✅ Avoid relying on internal implementation details.
- ✅ For Closed Shadow DOM, validate functionality through user-visible behavior.
- ✅ Collaborate with developers to expose test-friendly hooks if deeper testing is required.

---

# Open vs. Closed Shadow DOM

| Feature | Open Shadow DOM | Closed Shadow DOM |
|----------|-----------------|-------------------|
| Accessible by Playwright | ✅ Yes | ❌ No |
| Can inspect elements | ✅ Yes | ❌ No |
| Can interact with internal elements | ✅ Yes | ❌ No |
| Recommended testing approach | Direct interaction | Test via public UI or test hooks |

---

# Interview Summary (2-Minute Answer)

> **Question:** *How do you handle Shadow DOM in Playwright?*

**Answer:**

> "Playwright has built-in support for **Open Shadow DOM**, so I can interact with elements inside a shadow root using chained locators or the `>>` selector syntax. For example, I locate the shadow host first and then the element inside it. However, **Closed Shadow DOM** is intentionally inaccessible, so automation tools cannot interact with its internal elements. In those cases, I either ask developers to expose test hooks such as `data-testid` or validate the component's behavior through its public UI. This ensures the tests remain reliable without depending on internal implementation details."

# 8. How do you test WebSockets?

WebSockets enable real-time, bidirectional communication between the client and the server. Unlike traditional HTTP requests, a WebSocket connection remains open, allowing data to be sent and received instantly.

In Playwright, you can listen for WebSocket events and validate the messages exchanged between the client and server.

---

## Listen for WebSocket Events

Capture WebSocket connections and monitor the frames being sent and received.

```typescript
page.on('websocket', ws => {
  console.log('WebSocket URL:', ws.url());

  ws.on('framesent', data => {
    console.log('Sent:', data.payload);
  });

  ws.on('framereceived', data => {
    console.log('Received:', data.payload);
  });
});
```

---

## What to Validate

When testing WebSockets, verify the following:

- ✅ WebSocket connection is established successfully
- ✅ Correct messages are sent to the server
- ✅ Correct messages are received from the server
- ✅ Message format and payload are correct
- ✅ Real-time updates are reflected in the UI
- ✅ Connection is automatically re-established after a disconnect
- ✅ Error messages are handled gracefully
- ✅ No unexpected connection closures occur

---

## Example Test Scenario

Suppose you're testing a live chat application:

1. Open the chat application.
2. Verify the WebSocket connection is established.
3. Send a chat message.
4. Validate that the message is sent over the WebSocket.
5. Verify the server responds with the correct message.
6. Confirm the message appears in the chat UI.

---

## Example Assertion

```typescript
let messageReceived = false;

page.on('websocket', ws => {
  ws.on('framereceived', frame => {
    if (frame.payload.includes('Hello')) {
      messageReceived = true;
    }
  });
});

await expect.poll(() => messageReceived).toBe(true);
```

---

## Common WebSocket Test Cases

- 🔹 Verify successful connection establishment.
- 🔹 Validate authentication during connection.
- 🔹 Verify messages are sent and received correctly.
- 🔹 Validate message payload and format.
- 🔹 Test server push notifications.
- 🔹 Verify reconnection after network interruption.
- 🔹 Test handling of invalid or malformed messages.
- 🔹 Verify behavior when the server disconnects unexpectedly.
- 🔹 Ensure multiple users receive real-time updates correctly.

---

## Best Practices

- ✅ Validate both sent and received frames.
- ✅ Avoid fixed delays; use Playwright's event listeners.
- ✅ Test network interruptions and automatic reconnection.
- ✅ Verify UI updates after receiving WebSocket messages.
- ✅ Check for proper error handling and timeout behavior.
- ✅ Test under multiple concurrent client connections if applicable.

---

# Interview Summary (2-Minute Answer)

> **Question:** *How do you test WebSockets in Playwright?*

**Answer:**

> "To test WebSockets in Playwright, I listen for the `websocket` event and monitor the frames being sent and received using the `framesent` and `framereceived` event handlers. I validate that the WebSocket connection is established successfully, the correct messages are exchanged, and the UI updates in real time based on those messages. I also test reconnection scenarios, error handling, and unexpected disconnections to ensure the application behaves reliably under different network conditions."

# 9. How do you verify emails received after registration?

Email verification is a common end-to-end testing scenario in web applications. The goal is to ensure that the application sends the correct email after a user registers and that the email content is accurate.

---

## Common Tools for Email Testing

Some popular tools used to capture and validate emails during automation are:

- 📧 **MailSlurp**
- 📧 **MailHog**
- 📧 **Mailtrap**
- 📧 **Gmail API** (for real Gmail accounts)

---

## Email Verification Flow

```text
Register User
      │
      ▼
Wait for Email
      │
      ▼
Open Email
      │
      ▼
Validate Subject
      │
      ▼
Validate Email Body
      │
      ▼
Extract OTP or Verification Link
      │
      ▼
Complete Email Verification
```

---

## Example Using MailSlurp

Wait for the latest email after registration:

```typescript
const email = await mailSlurp.waitForLatestEmail(inboxId);
```

---

## Validations to Perform

After receiving the email, verify the following:

- ✅ Email is received successfully
- ✅ Sender email address is correct
- ✅ Recipient email address is correct
- ✅ Subject line is correct
- ✅ Email body contains the expected content
- ✅ OTP is present and correctly formatted
- ✅ Verification or activation link is present
- ✅ Link redirects to the correct page
- ✅ Email is received within the expected time

---

## Example Assertions

```typescript
expect(email.subject).toBe('Verify Your Account');

expect(email.body).toContain('Welcome');

expect(email.body).toContain('verification');

expect(email.body).toMatch(/https?:\/\/.+/);
```

---

## If the Email Contains an OTP

Extract and validate the OTP before using it.

```typescript
const otp = email.body.match(/\d{6}/)?.[0];

expect(otp).toBeTruthy();
```

---

## If the Email Contains a Verification Link

Extract the link and navigate to it.

```typescript
const link = email.body.match(/https?:\/\/[^\s]+/)?.[0];

await page.goto(link!);

await expect(page).toHaveURL(/verified/);
```

---

## Best Practices

- ✅ Use disposable inboxes for automation.
- ✅ Wait for emails using polling instead of fixed delays.
- ✅ Validate both the email subject and body.
- ✅ Verify OTP or activation links.
- ✅ Ensure emails are received within an acceptable time.
- ✅ Clean up test inboxes after execution.
- ✅ Avoid using personal email accounts for automated tests.

---

# Interview Summary (2-Minute Answer)

> **Question:** *How do you verify emails received after registration?*

**Answer:**

> "To verify registration emails, I typically use tools like **MailSlurp**, **MailHog**, **Mailtrap**, or the **Gmail API**, depending on the project requirements. After registering a user, I wait for the email to arrive, then validate the sender, recipient, subject, and email body. If the email contains an OTP, I extract and verify it. If it contains a verification link, I navigate to the link and confirm that the account is successfully activated. I also ensure the email is delivered within the expected time and use disposable inboxes to keep the tests isolated and reliable."

# 10. How do you debug a flaky Playwright test?

Debugging flaky tests requires a systematic approach to identify the root cause instead of simply adding retries. Below is the step-by-step process I follow.

---

## Step 1: Run the Test in Headed Mode

Running the test in headed mode allows you to visually observe the browser behavior and identify where the test is failing.

```bash
npx playwright test --headed
```

---

## Step 2: Run the Test in Debug Mode

Debug mode pauses the execution, allowing you to inspect each action interactively.

```bash
npx playwright test --debug
```

---

## Step 3: Analyze the Trace Using Trace Viewer

Playwright's Trace Viewer provides a detailed timeline of actions, screenshots, network requests, and DOM snapshots.

```bash
npx playwright show-trace trace.zip
```

---

## Step 4: Record Videos for Failed Tests

Enable video recording to review test execution after failures.

```typescript
use: {
  video: 'retain-on-failure'
}
```

---

## Step 5: Capture Screenshots

Take screenshots at critical points or when a test fails.

```typescript
await page.screenshot({
  path: 'failed.png'
});
```

---

## Step 6: Inspect Network Requests and Responses

Monitor API calls to detect slow or failed network requests.

```typescript
page.on('request', request => {
  console.log(request.url());
});

page.on('response', response => {
  console.log(response.status(), response.url());
});
```

---

## Step 7: Capture Browser Console Logs and Errors

Console logs and JavaScript errors often reveal application-side issues.

```typescript
page.on('console', msg => {
  console.log(msg.text());
});

page.on('pageerror', error => {
  console.log(error.message);
});
```

---

## Step 8: Check for Common Causes of Flaky Tests

The most common reasons include:

- ❌ Unstable or dynamic locators
- ❌ Hard waits (`waitForTimeout()`)
- ❌ Missing assertions
- ❌ Race conditions
- ❌ Slow API responses
- ❌ Shared or inconsistent test data
- ❌ Tests that depend on execution order
- ❌ Timing or synchronization issues

---

# Best Practices to Reduce Flakiness

- ✅ Prefer Playwright's **auto-waiting** over hard waits.
- ✅ Use resilient locators such as:
  - `getByRole()`
  - `getByTestId()`
  - `getByLabel()`
- ✅ Keep tests independent and isolated.
- ✅ Mock unstable external APIs when appropriate.
- ✅ Use explicit assertions with Playwright's `expect()`.
- ✅ Avoid shared state between tests.
- ✅ Retry only after identifying and fixing the root cause.

---

# Interview Summary (2-Minute Answer)

> **Question:** *How do you debug flaky Playwright tests?*

**Answer:**

> "I first reproduce the issue by running the test in headed mode and then in debug mode to observe exactly where it fails. Next, I use Playwright Trace Viewer to analyze each action, along with videos and screenshots for failed executions. I also inspect browser console logs, JavaScript errors, and network requests to identify any application or API-related issues.
>
> After gathering the evidence, I check for common causes such as unstable locators, synchronization issues, hard waits, race conditions, slow API responses, or shared test data. I replace hard waits with Playwright's built-in auto-waiting and assertions, use reliable locators like `getByRole()` or `getByTestId()`, and ensure each test is independent. This systematic approach helps eliminate flaky tests by addressing the root cause instead of simply masking failures with retries."




