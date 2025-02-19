---
title: Page Object Model Pattern for Selenium WebDriver and Java
date: 2025-02-16T23:07:59+07:00
lastmod: 2025-02-19T09:07:59+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
# image geneated from chatGPT https://chatgpt.com/share/67b53d89-af4c-8009-9797-1a85386afe08
cover: webdriver-selenium-pom-java.png
# images:
#   - /img/cover.jpg
categories:
  - automation
tags:
  - selenium
  - webdriver
  - page-object-model
  - java
  - software-engineer
# nolastmod: true
draft: false
---

This summary from the Udemy course "Page Object Model pattern for Selenium WebDriver & Java".

<!--more-->

<p align="center"><b>﷽</b></p>

## Section 1 : Introduction

### What is Page Object Model?

Page Object Model is a Design pattern for writing Selenium automated test scripts.

- Web element handling code moved into separate classes.
- One class/object for each web page,

  - e.g :
    `Login Page class`
    `Home Page class`

### Why we use Page Object Model?

- Maintainability
- Faster test script development
- Agile delivery
- Evolve the framework easily
- Beauty, Quality & Morale

## Section 2 : Creating a Simple Page Object Model

### Before using POM Design

The automated test scripts looks like (Linear test script) :

      1 import static org.junit.jupiter.api.Assertions.assertEqual;
      2 import org.openqa.selenium.By;
      3 import org.openqa.selenium.WebDriver;
      4 import org.openqa.selenium.WebElement;
      5 import org.openqa.selenium.chrome.ChromeDriver;
      6 import org.junit.Test;
      7 import org.openqa.selenium.support.ui.ExpectedConditions;
      8 import org.openqa.selenium.support.ui.WebDriverWait;
      9
      10 import java.util.List;
      11
      12 // Linear Shopping Cart tests for Java
      13 public class LinearCartTests {
      14
      15     @Test
      16     public void LinearAddToCartTest() {
      17
      18         // initialisation
      19         WebDriver browser = new ChromeDriver();
      20         WebDriverWait wait = new WebDriverWait(browser, 10);
      21         browser.manage().window().maximize();
      22
      23         // go to website
      24         browser.get("http://automationpractice.com/");
      25
      26         // navigate to login page
      27         WebElement signInLink = browser.findElement(By.cssSelector("a.login"));
      28         signInLink.click();
      29
      30         // log in
      31         wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("email")));
      32         WebElement emailTextbox = browser.findElement(By.id("email"));
      33         emailTextbox.sendKeys("petejenkins@test.com");
      34         WebElement passwordTextbox = browser.findElement(By.id("passwd"));
      35         passwordTextbox.sendKeys("Password1234");
      36         WebElement signInButton = browser.findElement(By.id("SubmitLogin"));
      37         signInButton.click();
      38
      39         // navigate back to home page
      40         wait.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector("a.home")));
      41         WebElement homeLink = browser.findElement(By.cssSelector("a.home"));
      42         homeLink.click();
      43
      44         // select the first product
      45         List<WebElement> productLinks = browser.findElements(By.cssSelector("a.product-name"));
      46         wait.until(ExpectedConditions.elementToBeClickable(productLinks.get(0)));
      47         productLinks.get(0).click();
      48
      49         // add 1 item to the shopping cart
      50         wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//p[@id='add_to_cart']/button")));
      51         WebElement addToCartButton = browser.findElement(By.xpath("//p[@id='add_to_cart']/button"));
      52         addToCartButton.click();
      53
      54         // proceed to checkout
      55         wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//a[@title='Proceed to checkout']")));
      56         WebElement proceedToCheckoutButton = browser.findElement(By.xpath("//a[@title='Proceed to checkout']"));
      57         proceedToCheckoutButton.click();
      58
      59         // verify we have 1 item in the shopping cart
      60         String numProductsLabelText = browser.findElement(By.id("summary_products_quantity")).getText();
      61         int spaceLocation = numProductsLabelText.indexOf(" ");
      62         int numProducts = Integer.parseInt(numProductsLabelText.substring(0, spaceLocation));
      63         assertEquals(numProducts, 1, "Expected number of products in shopping cart was 1 but actual value was: " +
      64             Integer.toString(num));
      65
      66         browser.quit();
      67 }

The script above (Linear test script) are put all process in one class, like : `initialisation`, `go to website`, `log in`,
`navigate back to home page`, `select the first product`, `add 1 item to the shopping cart`, `proceed to checkout`,
`verify we have 1 item in the shopping cart and last` and `quit the browser`.

**_How about if we have 50 test cases and there is an element id changed like in_**
`passwd` changed to `password` or we want to change `account` to login. It’s very time-consuming wasting time because we should
open edit all classes one by one.

### After using POM Design

The automated test scripts will looks like :

- Create new folder called `pages`, this will be place for some pages classes.

  - create `BasePage`, with the `BasePage` we can extend all pages classes to the `BasePage` so we no need to create `WebDriver` and
    `WebDriverWait` object.

    ```java
    1 package pages;
    2
    3 import org.openqa.selenium.WebDriver;
    4 import org.openqa.selenium.support.ui.WebDriverWait;
    5
    6 public class BasePage {
    7     WebDriver browser;
    8     WebDriverWait wait;
    9
    10     public BasePage(WebDriver browserDriver) {
    11         browser = browserDriver;
    12         // wait for page to load
    13         wait = new WebDriverWait(browser, 10);
    14     }
    15
    16 }
    ```

  - create `LoginPage`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.WebElement;
    6  import org.openqa.selenium.support.ui.ExpectedConditions;
    7
    8  public class LoginPage extends BasePage {
    9      private By emailAddressLocator = By.id("email");
    10     private By passwordTextboxLocator = By.id("passwd");
    11     private By signInButtonLocator = By.id("SubmitLogin");
    12
    13     public LoginPage(WebDriver browserDriver) {
    14         super(browserDriver);
    15         wait.until(ExpectedConditions.visibilityOfElementLocated(emailAddressLocator));
    16     }
    17
    18     public UserAccountPage login(String emailAddress, String password) {
    19         setEmailAddress(emailAddress);
    20         setPassword(password);
    21         return clickSignInButton();
    22     }
    23
    24     private LoginPage setEmailAddress(String emailAddress) {
    25         wait.until(ExpectedConditions.visibilityOfElementLocated(emailAddressLocator));
    26         WebElement emailTextbox = browser.findElement(emailAddressLocator);
    27         emailTextbox.clear();
    28         emailTextbox.sendKeys(emailAddress);
    29         return this;
    30     }
    31
    32     private LoginPage setPassword(String password) {
    33         wait.until(ExpectedConditions.visibilityOfElementLocated(passwordTextboxLocator));
    34         WebElement passwordTextbox = browser.findElement(passwordTextboxLocator);
    35         passwordTextbox.clear();
    36         passwordTextbox.sendKeys(password);
    37         return this;
    38     }
    39
    40     private UserAccountPage clickSignInButton() {
    41         wait.until(ExpectedConditions.elementToBeClickable(signInButtonLocator));
    42         browser.findElement(signInButtonLocator).click();
    43         return new UserAccountPage(browser);
    44     }
    45 }

    ```

  - create `HomePage`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.WebElement;
    6  import org.openqa.selenium.support.ui.ExpectedConditions;
    7
    8  import java.util.List;
    9
    10 public class HomePage extends BasePage {
    11     private By signInLinkLocator = By.cssSelector("a.login");
    12     private By productLinksLocator = By.cssSelector("a.product-name");
    13
    14     public HomePage(WebDriver browserDriver) {
    15         super(browserDriver);
    16         // wait for page to load
    17         wait.until(ExpectedConditions.visibilityOfElementLocated(signInLinkLocator));
    18     }
    19
    20     public void clickSignInButton() {
    21         wait.until(ExpectedConditions.visibilityOfElementLocated(signInLinkLocator));
    22         WebElement signInLink = browser.findElement(signInLinkLocator);
    23         signInLink.click();
    24     }
    25
    26     public List<WebElement> getProductNameLinks() {
    27         wait.until(ExpectedConditions.elementToBeClickable(productLinksLocator));
    28         List<WebElement> productLinks = browser.findElements(productLinksLocator);
    29         return productLinks;
    30     }
    31 }
    ```

  - create `UserAccountPage`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.WebElement;
    6  import org.openqa.selenium.support.ui.ExpectedConditions;
    7
    8  public class UserAccountPage extends BasePage {
    9      private By homeLinkLocator = By.cssSelector("a.home");
    10
    11     public UserAccountPage(WebDriver browserDriver) {
    12         super(browserDriver);
    13         // wait for page to load
    14         wait.until(ExpectedConditions.visibilityOfElementLocated(homeLinkLocator));
    15     }
    16
    17     public void navigateToHomePage() {
    18         wait.until(ExpectedConditions.visibilityOfElementLocated(homeLinkLocator));
    19         WebElement homeLink = browser.findElement(homeLinkLocator);
    20         homeLink.click();
    21     }
    22 }
    ```

  - create `ProductDetailsPage`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.WebElement;
    6  import org.openqa.selenium.support.ui.ExpectedConditions;
    7
    8  public class ProductDetailsPage extends BasePage {
    9      private By addToCartButtonLocator = By.xpath("//p[@id='add_to_cart']/button");
    10
    11     public ProductDetailsPage(WebDriver browserDriver) {
    12         super(browserDriver);
    13         // wait for page to load
    14         wait.until(ExpectedConditions.visibilityOfElementLocated(addToCartButtonLocator));
    15     }
    16
    17     public void clickAddToCartButton() {
    18         wait.until(ExpectedConditions.elementToBeClickable(addToCartButtonLocator));
    19         WebElement addToCartButton = browser.findElement(addToCartButtonLocator);
    20         addToCartButton.click();
    21     }
    22 }
    ```

  - create `AddToCartConfirmationPopup`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.WebElement;
    6  import org.openqa.selenium.support.ui.ExpectedConditions;
    7
    8  public class AddToCartConfirmationPopup extends BasePage {
    9      private By proceedToCheckoutButtonLocator = By.xpath("//a[@title='Proceed to checkout']");
    10
    11     public AddToCartConfirmationPopup(WebDriver browserDriver) {
    12         super(browserDriver);
    13         // wait for page to load
    14         wait.until(ExpectedConditions.visibilityOfElementLocated(proceedToCheckoutButtonLocator));
    15     }
    16
    17     public void clickProceedToCheckoutButton() {
    18         wait.until(ExpectedConditions.elementToBeClickable(proceedToCheckoutButtonLocator));
    19         WebElement proceedToCheckoutButton = browser.findElement(proceedToCheckoutButtonLocator);
    20         proceedToCheckoutButton.click();
    21     }
    22 }
    ```

  - create `ShoppingCartSummaryPage`

    ```java
    1  package pages;
    2
    3  import org.openqa.selenium.By;
    4  import org.openqa.selenium.WebDriver;
    5  import org.openqa.selenium.support.ui.ExpectedConditions;
    6
    7  public class ShoppingCartSummaryPage extends BasePage {
    8
    9      private By productQuantityLocator = By.id("summary_products_quantity");
    10
    11     public ShoppingCartSummaryPage(WebDriver browserDriver) {
    12         super(browserDriver);
    13         // wait for page to load
    14         wait.until(ExpectedConditions.visibilityOfElementLocated(productQuantityLocator));
    15     }
    16
    17     public int getQuantity() {
    18         wait.until(ExpectedConditions.visibilityOfElementLocated(productQuantityLocator));
    19         String numProductsLabelText = browser.findElement(productQuantityLocator).getText();
    20         int spaceLocation = numProductsLabelText.indexOf(" ");
    21         int numProducts = Integer.parseInt(numProductsLabelText.substring(0, spaceLocation));
    22         return numProducts;
    23     }
    24
    25 }
    ```

  - Finally create single class test case called `POMCartTests` the script looks like :

    ```java
    1 import Pages.*;
    2 import org.junit.jupiter.api.Test;
    3 import org.openqa.selenium.WebDriver;
    4 import org.openqa.selenium.WebElement;
    5 import org.openqa.selenium.chrome.ChromeDriver;
    6 import org.openqa.selenium.support.ui.WebDriverWait;
    7
    8 import java.util.List;
    9
    10 import static org.junit.jupiter.api.Assertions.assertEquals;
    11
    12 public class POMCartTests {
    13
    14     @Test
    15     public void POMAddToCartTest() {
    16
    17         // initialisation
    18         browser.manage().window().maximize();
    19         // go to website
    20         browser.get("http://automationpractice.com/");
    21         // navigate to login page
    22         HomePage homePage = new HomePage(browser);
    23         homePage.clickSignInButton();
    24         // log in
    25         LoginPage loginPage = new LoginPage(browser);
    26         loginPage.setEmailAddress("petejenkins@test.com");
    27         loginPage.setPassword("Password1234");
    28         loginPage.clickSignInButton();
    29
    30         // navigate back to home page
    31         UserAccountPage userAccountPage = new UserAccountPage(browser);
    32         userAccountPage.navigateToHomePage();
    33         // select the first product
    34         List<WebElement> productNameLinks = homePage.getProductNameLinks();
    35         productNameLinks.get(0).click();
    36         // add 1 item to the shopping cart
    37         ProductDetailsPage productDetailsPage = new ProductDetailsPage(browser);
    38         productDetailsPage.clickAddToCartButton();
    39         // proceed to checkout
    40         AddToCartConfirmationPopup confirmPopup = new AddToCartConfirmationPopup(browser);
    41         confirmPopup.clickProceedToCheckoutButton();
    42         // verify we have 1 item in the shopping cart
    43         ShoppingCartSummaryPage shoppingCartSummaryPage = new ShoppingCartSummaryPage(browser);
    44         int numProducts = shoppingCartSummaryPage.getQuantity();
    45         assertEquals(numProducts, 1, "Expected number of products in shopping cart was 1 but actual value was: " +
    46             Integer.toString(numProducts));
    47
    48         browser.quit();
    49     }
    50 }
    ```

This simple POM design above has already answered that if we have 50 test cases and we want to change the element id of `passwd` to
`password`. We only need to update in the `LoginPage` line 11. We don't need to open all the classes and update all the element id of `passwd` to `password`. Also if we want to change the account to login in test case scenario, we can change it in `POMCartTests`more simple right.

## Section 3 : Advanced Page Object Model

### Fluid Syntax

Fluid Syntax is demonstrated through method chaining, where each method call is made on the result of the previous method call. This
allows for a more compact and readable representation of the automation steps.

          1 driver = new ChromeDriver(options);
          2 driver
          3     .manage()
          4     .timeouts()
          5     .implicitlyWait(5, TimeUnit.SECONDS);
          6 driver
          7     .manage()
          8     .window()
          9     .maximize();

See the snippet script above, especially in line 2 till 9. The script called as `Fluid Syntax`. By using `fluid syntax`, you can chain together
various actions and element identification methods to create a concise and expressive automation script. Which makes the script nice
and compact readable.

To make this work, we need to change our `LoginPage` objects so these methods here return a `LoginPage` object. We do that. Instead of
having void methods. So `LoginPage` with Fluid Syntax will looks like `(Added return keyword)` :

          1 package pages;
          2
          3 import org.openqa.selenium.By;
          4 import org.openqa.selenium.WebDriver;
          5 import org.openqa.selenium.WebElement;
          6 import org.openqa.selenium.support.ui.ExpectedConditions;
          7
          8 public class LoginPage extends BasePage {
          9     private By emailAddressLocator = By.id("email");
          10     private By passwordTextboxLocator = By.id("passwd");
          11     private By signInButtonLocator = By.id("SubmitLogin");
          12
          13     public LoginPage(WebDriver browserDriver) {
          14         super(browserDriver);
          15         // wait for page to load
          16         wait.until(ExpectedConditions.visibilityOfElementLocated(emailAddressLocator));
          17     }
          18
          19     public UserAccountPage login(String emailAddress, String password) {
          20         setEmailAddress(emailAddress);
          21         setPassword(password);
          22         clickSignInButton();
          23         return new UserAccountPage(browser);
          24     }
          25
          26     private LoginPage setEmailAddress(String emailAddress) {
          27         wait.until(ExpectedConditions.visibilityOfElementLocated(emailAddressLocator));
          28         WebElement emailTextbox = browser.findElement(emailAddressLocator);
          29         emailTextbox.clear();
          30         emailTextbox.sendKeys(emailAddress);
          31         return this;
          32     }
          33
          34     private LoginPage setPassword(String password) {
          35         wait.until(ExpectedConditions.visibilityOfElementLocated(passwordTextboxLocator));
          36         WebElement passwordTextbox = browser.findElement(passwordTextboxLocator);
          37         passwordTextbox.clear();
          38         passwordTextbox.sendKeys(password);
          39         return this;
          40     }
          41
          42     private UserAccountPage clickSignInButton() {
          43         wait.until(ExpectedConditions.elementToBeClickable(signInButtonLocator));
          44         WebElement signInButton = browser.findElement(signInButtonLocator);
          45         signInButton.click();
          46         return new UserAccountPage(browser);
          47     }
          48 }

and we can call like this :

          1 //LoginPage
          2 LoginPage loginPage = new LoginPage(browser);
          3 loginPage.setEmailAddress("petejenkins@test.com")
          4          .setPassword("Password1234")
          5          .clickSignInButton();

## Section 4 : Tips and Tricks

### YAGNI You Ain’t Gonna Need It

- A Coding principle from Extreme Programming (XP)
- Don't write code you don't need now
- In POM it happens most when creating new classes
- Don't write code to handle web elements if we don't need to use those elements at the moment
- Don't create page object classes until we need them

### Design POM from Requirements

### KISS Keep It Simple, Stupid

- Put >95% of code in tests or page object classes
- Have a simple class hierarchy for page objects and tests
- Create a simple and intuitive folder structure
- Keep your page objects as simple as possible

### Refactor little and Often

- To make your code maintainable, you should refactor the code as often as possible

### Get familiarized POM error handling

- Page Object Model is not perfect, so you should get used to handling errors

## Section 5 : Course Roundup

- You should be able to create your own automation framework using Page Object Model
- You should understand WHY we use it
- Apply the advanced techniques to make your POM maintainable and robust
- Practice - Use it for your own application

That's all summary from this course.
