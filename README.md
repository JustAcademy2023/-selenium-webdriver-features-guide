# selenium-webdriver-features-guide

> **Top 10 Selenium WebDriver Features Every QA Must Know**
> A complete technical reference for 2026 — by JustAcademy, Mumbai.

[![Selenium](https://img.shields.io/badge/Selenium-4.x-43B02A?style=flat-square&logo=selenium&logoColor=white)](https://selenium.dev)
[![Java](https://img.shields.io/badge/Java-17+-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://java.com)
[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![JustAcademy](https://img.shields.io/badge/By-JustAcademy-C2185B?style=flat-square)](https://www.justacademy.co)

---

## Quick Links

| Resource | URL |
|---|---|
| Selenium Training Course | https://www.justacademy.co/course-detail/selenium-training |
| Free Demo Registration | https://www.justacademy.co/register-for-course-demo |
| JustAcademy Website | https://www.justacademy.co/ |

---

## Feature 1: Multi-Browser Support

```java
// Chrome
WebDriver chrome = new ChromeDriver();

// Firefox
WebDriver firefox = new FirefoxDriver();

// Edge
WebDriver edge = new EdgeDriver();

// Remote (Selenium Grid)
WebDriver remote = new RemoteWebDriver(
    new URL("http://grid:4444"), new ChromeOptions());
```

---

## Feature 2: Locator Strategies

```java
// Stability hierarchy (most → least stable)
By.id("loginBtn")                           // 1. ID — fastest
By.cssSelector("[data-testid='login']")     // 2. data-testid
By.cssSelector(".submit-btn")              // 3. CSS class
By.xpath("//button[text()='Login']")       // 4. XPath text
By.xpath("/html/body/div/button")          // 5. Absolute XPath — AVOID

// Selenium 4 Relative Locators
RelativeLocator.with(By.tagName("input")).below(By.id("usernameLabel"))
```

---

## Feature 3: Wait Strategies

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Explicit Wait (recommended)
wait = WebDriverWait(driver, 15)
element = wait.until(EC.element_to_be_clickable((By.ID, "submit")))

# Fluent Wait (advanced)
from selenium.webdriver.support.wait import WebDriverWait
wait = WebDriverWait(driver, 30,
    poll_frequency=2,
    ignored_exceptions=[NoSuchElementException])
```

---

## Feature 4: JavaScript Executor

```java
JavascriptExecutor js = (JavascriptExecutor) driver;

// Scroll to element
js.executeScript("arguments[0].scrollIntoView(true);", element);

// Click hidden element
js.executeScript("arguments[0].click();", element);

// Get computed value
String color = (String) js.executeScript(
    "return window.getComputedStyle(arguments[0]).color;", element);
```

---

## Feature 5: Actions Class

```java
Actions actions = new Actions(driver);

// Hover
actions.moveToElement(menu).perform();

// Right-click
actions.contextClick(element).perform();

// Drag and drop
actions.dragAndDrop(source, target).perform();

// Scroll (Selenium 4)
actions.scrollToElement(element).perform();
actions.scrollByAmount(0, 500).perform();

// Keyboard chord
actions.keyDown(Keys.CONTROL).sendKeys("a").keyUp(Keys.CONTROL).perform();
```

---

## Feature 6: Chrome DevTools Protocol (Selenium 4)

```java
DevTools devTools = ((ChromeDriver) driver).getDevTools();
devTools.createSession();

// Enable network
devTools.send(Network.enable(Optional.empty(), Optional.empty(), Optional.empty()));

// Mock geolocation
devTools.send(Emulation.setGeolocationOverride(
    Optional.of(28.6139), Optional.of(77.2090), Optional.of(1)));

// Network throttling
devTools.send(Network.emulateNetworkConditions(
    false, 100, 500, 1000, Optional.empty()));
```

---

## Feature 7: Screenshots

```java
// Full page screenshot
File screenshot = ((TakesScreenshot) driver)
    .getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(screenshot, new File("reports/failure.png"));

// Element screenshot (Selenium 4)
File elementShot = element.getScreenshotAs(OutputType.FILE);
```

---

## Feature 8: Window and Frame Management

```java
// New tab (Selenium 4)
driver.switchTo().newWindow(WindowType.TAB);

// Switch window
String original = driver.getWindowHandle();
driver.getWindowHandles().forEach(h -> driver.switchTo().window(h));

// Switch to iframe
driver.switchTo().frame(driver.findElement(By.id("myFrame")));

// Return to main
driver.switchTo().defaultContent();
```

---

## Feature 9: Selenium Grid 4

```yaml
# docker-compose.yml
version: "3"
services:
  selenium-hub:
    image: selenium/hub:4.18.1
    ports: ["4442:4442", "4443:4443", "4444:4444"]
  chrome:
    image: selenium/node-chrome:4.18.1
    depends_on: [selenium-hub]
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
    deploy:
      replicas: 4
```

---

## Feature 10: Framework Architecture
automation-framework/
├── src/test/java/
│   ├── base/
│   │   └── BaseTest.java          ← WebDriver init/teardown
│   ├── pages/
│   │   ├── LoginPage.java         ← Page Object classes
│   │   └── DashboardPage.java
│   ├── tests/
│   │   └── LoginTests.java        ← Test classes
│   └── utils/
│       ├── DriverFactory.java     ← Browser factory
│       └── ReportUtils.java       ← Allure integration
├── src/test/resources/
│   ├── testng.xml                 ← Parallel execution config
│   └── config.properties         ← Environment settings
└── pom.xml                       ← Maven dependencies

---

## Salary Data — India 2026

| Level | Features Known | Salary (LPA) |
|---|---|---|
| Junior | Features 1–4 | ₹4–7 |
| Mid-Level | Features 1–7 | ₹8–14 |
| Senior | All 10 | ₹15–28 |

---

## About JustAcademy

Leading IT training institute — Borivali, Mumbai.
📞 +91 99871 84296 | 📧 info@justacademy.co | 🌐 https://www.justacademy.co/

*© 2026 JustAcademy | Empowering Careers Through Quality Education*
