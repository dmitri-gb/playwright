---
id: intro
title: "Installation"
---

Playwright was created specifically to accommodate the needs of end-to-end testing. Playwright supports all modern rendering engines including Chromium, WebKit, and Firefox. Test on Windows, Linux, and macOS, locally or on CI, headless or headed with native mobile emulation.

Playwright recommends using the official [Playwright Pytest plugin](./test-runners.md) to write end-to-end tests. It provides context isolation, running it on multiple browser configurations out of the box. Alternatively you can use the [library](./library.md) to manually write the testing infrastructure with your preferred test-runner. The Pytest plugin utilizes the sync version of Playwright, there is also an async version accessible via the library.

Get started by installing Playwright and running the example test to see it in action.

<Tabs
  groupId="package-managers"
  defaultValue="pypi"
  values={[
    {label: 'PyPI', value: 'pypi'},
    {label: 'Anaconda', value: 'anaconda'}
  ]
}>
<TabItem value="pypi">

Install the [Pytest plugin](https://pypi.org/project/pytest-playwright/):

```bash
pip install pytest-playwright
```

</TabItem>
<TabItem value="anaconda">

Install the [Pytest plugin](https://anaconda.org/Microsoft/pytest-playwright):

```bash
conda config --add channels conda-forge
conda config --add channels microsoft
conda install playwright
```

</TabItem>
</Tabs>

Install the required browsers:

```bash
playwright install
```

## Add Example Test

Create a file that follows the `test_` prefix convention, such as `test_my_application.py`, inside the current working directory or in a sub-directory with the code below:

```py title="test_my_application.py"
import re
from playwright.sync_api import Page, expect


def test_homepage_has_Playwright_in_title_and_get_started_link_linking_to_the_intro_page(page: Page):
    page.goto("https://playwright.dev/")

    # Expect a title "to contain" a substring.
    expect(page).to_have_title(re.compile("Playwright"))

    # create a locator
    get_started = page.get_by_role("link", name="Get started")

    # Expect an attribute "to be strictly equal" to the value.
    expect(get_started).to_have_attribute("href", "/docs/intro")

    # Click the get started link.
    get_started.click()

    # Expects page to have a heading with the name of Installation.
    expect(page.get_by_role("heading", name="Installation")).to_be_visible()
```

## Running the Example Test

By default tests will be run on chromium. This can be configured via the CLI options. Tests are run in headless mode meaning no browser UI will open up when running the tests. Results of the tests and test logs will be shown in the terminal.

```bash
pytest
```

## System requirements

- Python 3.8 or higher.
- Windows 10+, Windows Server 2016+ or Windows Subsystem for Linux (WSL).
- MacOS 12 Monterey or MacOS 13 Ventura.
- Debian 11, Debian 12, Ubuntu 20.04 or Ubuntu 22.04.

## What's next

- [Write tests using web first assertions, page fixtures and locators](./writing-tests.md)
- [Run single test, multiple tests, headed mode](./running-tests.md)
- [Generate tests with Codegen](./codegen.md)
- [See a trace of your tests](./trace-viewer-intro.md)
