# test-playwright
This is the automation framework that is being building with Playwright library and Playwright Test Runner.

## Documentation

If you want to know more about Playwright and Playwright/Test please visit:
[Playwright Docs](https://playwright.dev/docs/intro)

## Installation

1.  You need to have **Node.js version 12** installed and **npm version greather than 7.0.0**. We are using the playwright library for executing tests, then you have to install the library and the supported browsers:

```bash
Install playwright
npm i -D @playwright/test
# install supported browsers
npx playwright install
```

2. Clone this repository
   `git clone https://github.com/APAODUQS/test-playwright.git`

3. Move to the folder:
   `cd test-playwright`

4. Install dependencies
   `npm install `

5. Run all tests locally
   `npm run test `

If you dont get any issues at this point you are ready to use the Automation Framework

## Usage

This is an small test example:

```typescript:
// Import interfaces from playwright test
import { test, expect } from '@playwright/test'
import { expect } from '@playwright/test'

// Use the test keyword to indicate you are creating a test and a proper description
// Pass the fixture you want to work in, in this case is a page that come from Playwright but you can create your own fixtures
test('basic test', async ({ page }) => {
  // Start: Navigation to a specific URL
  await page.goto('https://playwright.dev/')
  // Arrange: Find locators
  const title = page.locator('.navbar__inner .navbar__title')
  // Assert: Test validation
  await expect.soft(title, 'Some error message').toHaveText('Playwright')
})
```

## Execute the tests

For executing all tests locally, execute:

```bash
npx playwright test --config=playwright.config.ts
```

If you want to run those tests in a specific browser you can run the script adding `-- --project YOUR_BROWSER`:

```
npx playwright test --config=playwright.config.ts --project Chrome
```

Other ways to run the tests:

```bash
# To run specific test files, specify the route of the tests:
npx playwright test tests/TEST_CLASS.spec.ts --config=playwright.config.ts

# Run a set of test files
npx playwright test tests/TEST_CLASS_1/ tests/TEST_CLASS_2/

# Run files that have KEY_1 or KEY_2 in the file name
npx playwright test KEY_1 KEY_2

# Run the test with the title
npx playwright test -g "SOME_TITLE"

# Run tests in headed browsers
npx playwright test --headed

# Run tests in a particular configuration (project)
npx playwright test --project PROJECT
# Or contains multiple projects:
npx playwright test --project PROJECT1 PROJECT2

# Run in debug mode with Playwright Inspector
npx playwright test --debug

# Run only the tests that contains a tag:
npx playwright test --grep @YOUR_TAG
# Or contains multiple tag:
npx playwright test --grep "@TAG1|@TAG2"

# Or if you want the opposite, you can skip the tests with a certain tag:
npx playwright test --grep-invert @YOUR_TAG_SKIP
```

If you need help, you can execute:

```bash
npx playwright test --help
```