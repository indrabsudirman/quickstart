---
title: Automation With Pytest
date: 2025-02-26T23:06:07+07:00
lastmod: 2025-02-27T23:09:47+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
# https://chatgpt.com/share/67b8a04f-6e84-8009-8a50-7f02c82812ed
cover: pytest-logo.png
# images:
#   - /img/cover.jpg
categories:
  - automation
  - python
  - pytest
tags:
  - pytest
  - automation
  - python
  - qa-automation
  - software-engineer
# nolastmod: true
draft: false
---

Another popular Python testing framework, pytest is known for its simplicity and powerful features. It supports unit, API, UI, and mobile testing with built-in assertions, fixtures, and parameterization.

<!--more-->

<p align="center">﷽</p>

### Background

Who has ever waited? Sometimes, waiting can be boring because we don’t know when what we’re waiting for will arrive. But nowadays, waiting is no longer dull, as we can still do some enjoyable activities while waiting, such as scrolling through social media (Instagram, Facebook, TikTok, etc.), watching our favorite movies on YouTube or Netflix, or even browsing and checking out items on online marketplaces.

Including myself—when waiting for something, I also do these things. However, on February 26, 2025, it was a bit different. While waiting for something, I decided to explore one of Python's automation frameworks using my phone. I kept going back and forth reading the documentation and testing it directly in [Termux](https://termux.dev/en/). I explored Pytest, a very popular framework in Python that many companies use.

![pytest-swtitching-app](/posts/2025/02/automation-with-pytest/termux-switching-app.jpeg)

## Let's get started

### Installation

To install Pytest, it's very straightforward. If you're using pip, you can use the following command:

```bash
pip install pytest
```

![pytest-docs-install](/posts/2025/02/automation-with-pytest/pytest-docs-installation.jpg)

let's try it out in my phone.

![pytest-install-pip](/posts/2025/02/automation-with-pytest/pytest-install-pip.jpeg)

once you have pytest installed, you can try it out by running the following command:

```bash
pytest --version
```

_as shown in the image above_

### Create a first test

again based on the documentation, let's create a simple test. To do this, I'm using [lazyvim](http://www.lazyvim.org/) in my termux. Create file test file `test_sample.py` with the following content:

```python
# content of test_sample.py
1 def func(x):
2    return x + 1
3
4
5 def test_answer():
6    assert func(3) == 4
```

![simple-test-pytest](/posts/2025/02/automation-with-pytest/simple-test-pytest.jpeg)

please note that on line 6, I use value `4` instead of `5`. So the test expected should be passed.

### Run the test

To run the test, you can use the following command:

```bash
pytest
```

the command above will run all the tests in the current directory and its subdirectories, as mentioned in the documentation.

> `pytest` will run all files of the form `test_*.py` or `*_test.py` in the current directory and its subdirectories

![pytest-run-test](/posts/2025/02/automation-with-pytest/run-pytest.jpeg)

as you can see in the image above, I run the `pytest` command twice. The first time, the test failed because the expected value is `4` but the actual value is `5`. The second time, the test passed because the expected value is `4` and the actual value is `4` as in the [Create a first test.](#create-a-first-test)

### Raise helper

Next, in the pytest documentation, I discovered something new: pytest can test whether a function throws a specific exception using the `raises` helper. I gained this insight! 😁

Yes, in the pytest documentation you can take a look [Assert that a certain exception is raised](https://docs.pytest.org/en/stable/getting-started.html#assert-that-a-certain-exception-is-raised), here’s an example :

```python
1 # content of test_sysexit.py
2 import pytest
3
4
5 def f():
6    raise SystemExit(1)
7
8
9 def test_mytest():
10    with pytest.raises(SystemExit):
11        f()
```

In lines 5-6, a function `f()` is created. This function uses `raise` _to trigger an exception_, specifically SystemExit(1).

In lines 9-10, a test function `test_mytest()` is created. The test function uses `pytest.raises(SystemExit)` to assert that calling `f() raises a SystemExit exception` (line 11). Which means same exception (SystemExit). If `f()` raises the expected exception, the test will pass. Otherwise, the test will fail.

![raises-pytest-sample-pass](/posts/2025/02/automation-with-pytest/raises-pytest-sample-pass.jpeg)

and if we try to run the test, we will get the result as shown in the image below.

![raises-run-terminal-passed-failed](/posts/2025/02/automation-with-pytest/raises-run-terminal-passed-failed.jpeg)

the green square indicates that the test passed, and the red square indicates that the test failed, because I made change function `f()` to `print("This an exception")` as image below.
![updated-the-raises-test-exception](/posts/2025/02/automation-with-pytest/updated-the-raises-test-exception.jpeg)

## Summary

Pytest is a very popular framework in Python that many companies use. It supports unit testing, API, UI, and mobile testing (with Appium both Android and iOS) with built-in assertions, fixtures, and parameterization.

That's my notes.
