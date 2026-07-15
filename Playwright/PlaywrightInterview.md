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

``` await page.getByRole('button').click(); ```
No explicit wait required.

# 6. What are Locators?
Locators are Playwright's recommended way to find elements.

Examples
```
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
```locator()```
Lazy evaluation
Auto wait
Retry
Recommended
```page.$()```
Returns ElementHandle
No retry
Deprecated approach
# 9. Difference between fill() and type()
```fill()```
Clears textbox first
```type()```
Types character by character
# 10. Difference between click() and dblclick()
```
await locator.click();
await locator.dblclick();
```
## Intermediate Questions
# 11. How does Playwright handle synchronization?
Using

Auto waiting
expect()
waitForSelector()
waitForURL()
waitForLoadState()
# 12. What are different wait methods?
waitForSelector()
waitForLoadState()
waitForTimeout()
waitForURL()
waitForEvent()
waitForResponse()
waitForRequest()
# 13. Why avoid waitForTimeout()?
Hard waits

Slow execution
Flaky tests
# 14. Difference between waitForSelector() and expect()
await page.waitForSelector('#msg');
Only waits.

await expect(locator).toBeVisible();
Waits + verifies.

# 15. How to upload a file?
await page.setInputFiles('input', 'sample.pdf');
# 16. Handle multiple tabs
const pagePromise = context.waitForEvent('page');
await page.click('#open');
const newPage = await pagePromise;
# 17. Handle alerts
page.on('dialog', async dialog => {
   await dialog.accept();
});
# 18. Handle frames
const frame =
page.frameLocator('#frame');
await frame.locator('#name').fill('Sunil');
# 19. Handle dropdown
await locator.selectOption('India');
# 20. Handle dynamic elements?
Smart locators
Auto waiting
Relative locators
Retry assertions
Advanced Questions
# 21. Explain Browser Context.
Each context is an isolated session.

Useful for

Parallel execution
Multiple users
Incognito sessions
# 22. API Testing in Playwright
const request =
await playwright.request.newContext();
const response =
await request.get(url);
# 23. Mock API Response
await page.route(
'**/users',
route => route.fulfill({
status:200,
body:JSON.stringify(data)
}));
# 24. Block Network Calls
await page.route(
'**/*.png',
route => route.abort()
);
25. Capture Screenshot
await page.screenshot({
path:'home.png'
});
26. Record Video
use:{
video:'on'
}
27. Trace Viewer
use:{
trace:'on-first-retry'
}
Open

npx playwright show-trace trace.zip
28. Retry Failed Tests
retries:2
29. Parallel Execution
workers:4
30. Serial Execution
test.describe.configure({
mode:'serial'
});
Framework Questions
31. Explain your Playwright framework architecture.
Mention:

Page Object Model
Fixtures
Utilities
Config
Test Data
API Layer
Reports
CI/CD
Logger
32. How do you manage test data?
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
Scenario-Based Questions
How would you automate OTP login?
How would you test file downloads?
How do you handle CAPTCHA in automation?
How would you automate infinite scrolling?
How would you test a table with 10,000 rows?
How would you test a React application?
How do you handle shadow DOM?
How do you test WebSockets?
How do you verify emails received after registration?
How do you debug a flaky Playwright test?
1. How would you automate OTP login?
Expected Answer
OTP should not be automated by reading the actual SMS or email in UI automation because it depends on external systems and makes tests flaky.

Instead, I would use one of these approaches:

Approach 1 (Preferred) — Test Environment Bypass
Ask developers to provide:

Static OTP
API to fetch OTP
Disable OTP in QA
Test-only authentication endpoint
This is the most reliable approach.

Approach 2 — Read OTP from Database
If OTP is stored in DB:

const otp = await getOtpFromDB(phoneNumber);
await page.getByLabel('OTP').fill(otp);
Approach 3 — Read OTP from Email
Using Gmail API or MailSlurp.

const otp = await mailSlurp.getLatestOTP();
Approach 4 — Read OTP from SMS Service
Twilio API

AWS SNS

MessageBird

Interview Tip

“I avoid UI automation of actual SMS because it creates dependency on third-party services. I prefer backend APIs or test hooks.”

2. How would you test file downloads?
Playwright provides download events.

const downloadPromise =
page.waitForEvent('download');
await page.click('text=Download');
const download =
await downloadPromise;
await download.saveAs('downloads/report.pdf');
Validate

File exists
File name
File size
Extension
Content
Example

expect(download.suggestedFilename())
.toContain('.pdf');
3. How do you handle CAPTCHA?
Never automate CAPTCHA.

CAPTCHA exists specifically to prevent automation.

Instead use

Disable CAPTCHA in QA
Test bypass token
Whitelist automation IP
Mock CAPTCHA validation
If interviewer insists

Google reCAPTCHA provides test keys.

Good interview answer

“CAPTCHA itself shouldn’t be automated. In QA we normally bypass it or mock its validation.”

4. How would you automate infinite scrolling?
Keep scrolling until no more content loads.

let previousHeight = 0;
while (true) {
const currentHeight =
await page.evaluate(() =>
document.body.scrollHeight);
if(currentHeight===previousHeight)
break;
previousHeight=currentHeight;
await page.evaluate(()=>
window.scrollTo(0,document.body.scrollHeight));
await page.waitForTimeout(1000);
}
Better approach

Wait for API response instead of timeout.

5. How would you test a table with 10,000 rows?
Never validate all rows.

Instead

Pagination testing
Search functionality
Sorting
Filtering
Random sampling
API validation
Example

const rows =
page.locator('table tbody tr');
await expect(rows)
.toHaveCount(50);
Validate backend data instead of every UI row.

Interview Tip

“UI should validate representative data while backend/API validates the full dataset.”

6. How would you test a React application?
Focus on

Dynamic DOM updates
Component rendering
State changes
API calls
Loading spinner
Lazy loading
Use

getByRole()
getByLabel()
getByTestId()
Avoid XPath.

React updates DOM frequently.

Use auto waiting.

Interview Tip

Prefer accessibility-based locators because they remain stable across UI changes.

7. How do you handle Shadow DOM?
Playwright automatically supports open Shadow DOM.

Example

await page
.locator('custom-element')
.locator('#submit')
.click();
or

page.locator(
'custom-element >> button');
Closed Shadow DOM cannot be accessed directly. In such cases, ask developers to expose test hooks or test the behavior through the public UI.

8. How do you test WebSockets?
Listen for WebSocket events.

page.on('websocket', ws => {
console.log(ws.url());
ws.on('framereceived',
data=>console.log(data));
ws.on('framesent',
data=>console.log(data));
});
Validate

Connection established
Correct messages
Reconnection
Error handling
9. How do you verify emails received after registration?
Preferred options

MailSlurp
MailHog
Mailtrap
Gmail API
Flow

Register User
↓
Wait for Email
↓
Open Email
↓
Validate Subject
↓
Validate Body
↓
Click Verification Link
Example

const email =
await mailSlurp.waitForLatestEmail();
Validate

Subject
Sender
OTP
Verification link
10. How do you debug a flaky Playwright test?
My debugging approach:

Step 1
Run headed

npx playwright test --headed
Step 2
Run in debug mode

npx playwright test --debug
Step 3
Trace Viewer

npx playwright show-trace trace.zip
Step 4
Record video

use:{
video:'retain-on-failure'
}
Step 5
Capture screenshots

await page.screenshot({
path:'failed.png'
});
Step 6
Check network requests

page.on('request', request => {
    console.log(request.url());
});
page.on('response', response => {
    console.log(response.status(), response.url());
});
Step 7
Inspect logs and console errors

page.on('console', msg => console.log(msg.text()));
page.on('pageerror', error => console.log(error.message));
Step 8
Look for common causes

Unstable locators
Hard waits (waitForTimeout)
Missing assertions
Race conditions
Slow API responses
Shared test data
Tests that depend on execution order
Interview Summary (2-minute answer)
If asked, “How do you debug flaky tests?”, you can answer:

“I first reproduce the issue by running the test in headed and debug mode. Then I use Playwright Trace Viewer, videos, screenshots, browser console logs, and network logs to identify where it fails. I verify whether the failure is due to unstable locators, synchronization issues, slow APIs, or shared test data. I replace hard waits with Playwright’s auto-waiting and assertion mechanisms, use resilient locators like getByRole or getByTestId, and isolate tests to ensure they are independent. This systematic approach helps eliminate flakiness rather than just masking it with retries."





