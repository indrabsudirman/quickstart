---
title: Writing Better Gherkin
date: 2025-02-19T22:49:35+07:00
lastmod: 2025-02-19T22:49:35+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
# https://chatgpt.com/share/67b8a04f-6e84-8009-8a50-7f02c82812ed
cover: writing-better-gherkin-cucumber.png
# images:
#   - /img/cover.jpg
categories:
  - automation
  - gherkin
tags:
  - gherkin
  - bdd
  - cucumber
  - testing
# nolastmod: true
draft: false
---

Feel curious and want to know more, has bring me to dive deep into the world of BDD.

<!--more-->

<p align="center">﷽</p>

## Background

The story of writing better gherkin, starts when I was working on an automation test project with WebdriverIO, Cucumber, Cypress and TypeScript.

Gherkin is a language used to write automated tests (in most cases, but I found it use to write stories like PRD). It is a simple and easy to understand language. It is used to describe the behavior of a system in a human-readable way, so that it can be easily understood by non-technical people (outside engineers). Other things, it is also used as a documentation for the system. So it make sense to write better gherkin (human readable).

I found this documentation very helpful for me to understand gherkin [Writing better Gherkin](https://cucumber.io/docs/bdd/better-gherkin). Based on that documentation, there are two kinds style of gherkin imperative and declarative.

## Imperative Style vs Declarative Style

The imperative style describes _how_ something is done in detail. Typically, this approach is more technical and less focused on user behavior.

The declarative style describes _what happens_ without too many technical details. Its focus is on **user behavior and business outcomes**.

So what is the recommended way to write gherkin? again, based on the documentation [Writing better Gherkin](https://cucumber.io/docs/bdd/better-gherkin), **the recommended way is to write gherkin in declarative style.**

Here are the both examples:

**Imperative style**:

```gherkin
1 Scenario: User successfully logs in
2   Given the user is on the login page
3   And the user clicks the "haveAccountBtn" button
4   When the user fills in "editTextUsername" with "testuser"
5   And the user fills in "editTextPassword" with "password123"
6   And the user clicks the button labeled "Login"
7   Then the user sees "Welcome testuser" on the dashboard page
```

**Problems:**

```
❌ Too technical (mentions UI elements/variables like "haveAccountBtn", "editTextUsername", "editTextPassword", "loginBtn" and "button").
❌ Difficult for non-technical stakeholders to understand.
❌ If the UI or elements changes (e.g., the button label changes to "Sign In" line 6), the scenario can quickly become outdated.
```

**Declarative style**:

```gherkin
1 Scenario: User successfully logs in
2   Given User is on the login page
3   When User logs in with valid credentials
4   Then User enters the dashboard
```

**Advantages:**  
✅ Easier to understand for business teams, developers, and QA.  
✅ Not dependent on UI details, making it more resilient to design changes.  
✅ More focused on expected outcomes rather than technical steps.

## Abstract Helper

Now, the question is, how about if we want to use abstract helper in declarative style?

Here is the tips:

_Abstract helpers can still be used in a **declarative** style, as long as they focus on **clear business behavior** rather than just technical abstraction._

**Imperative style with abstract helper**:

```gherkin
Given I go to the "{page}" page
```

```java
@Given("I go to the {string} page")
public void iWantToOpenPage(String webpage) {
    webpageFactory.openPage(webpage);
}
```

**Problems:**

```
❌ Too abstract, as it does not specify a particular page in a business context.
❌ Unclear for non-technical teams, since they need to know that {page} could be "login," "dashboard," etc.
❌ Can make scenarios harder to maintain, especially if there are specific rules for each page.
```

**Declarative style with abstract helper**:

```gherkin
Given I go to the "{page}" page
```

```java
// Mapping halaman untuk menjaga skenario tetap deklaratif
private static final Map<String, String> pages = Map.of(
    "login", "https://example.com/login",
    "dashboard", "https://example.com/dashboard",
    "profile", "https://example.com/profile"
)
@Given("Given I go to the {string} page")
public void iAmOnThePage(String pageType) {
    String url = pages.get(pageType);
    if (url != null) {
        driver.get(url);
    } else {
        throw new IllegalArgumentException("Invalid page type: " + pageType);
    }
}
```

**Why is this still declarative?**

```
✅ Focuses on business logic, as it only allows navigation to valid pages in the system.
✅ Not too technical, since it explicitly defines the intended pages.
✅ More flexible than hardcoded steps while still maintaining clear business context.
```

## Scenario Outline

The other question is, how about if we want to use Scenario Outline in declarative style?

Here is the tips:

_**Scenario Outline can still be declarative** as long as the `{page}` parameter contains only valid business values._

**Declarative style with Scenario Outline**:

```gherkin
Scenario Outline: User navigates to a specific page
  Given I go to the "<page>" page

Examples:
  | page      |
  | login     |
  | dashboard |
  | profile   |
```

```java
// Mapping halaman untuk menjaga skenario tetap deklaratif
private static final Map<String, String> pages = Map.of(
    "login", "https://example.com/login",
    "dashboard", "https://example.com/dashboard",
    "profile", "https://example.com/profile"
)
@Given("Given I go to the {string} page")
public void iAmOnThePage(String page) {
    String url = pages.get(page);
    if (url != null) {
        driver.get(url);
    } else {
        throw new IllegalArgumentException("Invalid page: " + page);
    }
}
```

That all my notes.
