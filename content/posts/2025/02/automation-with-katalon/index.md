---
title: Automation With Katalon
date: 2025-02-28T19:19:10+07:00
lastmod: 2025-02-28T19:19:10+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
# https://chatgpt.com/share/67b8a04f-6e84-8009-8a50-7f02c82812ed
cover: katalon-logo-part-1.png
# images:
#   - /img/cover.jpg
categories:
  - automation
  - katalon
tags:
  - katalon
  - automation
  - qa-automation
  - software-engineer
# nolastmod: true
draft: false
---

My automation notes this time focus on one of the robust and popular automation frameworks, which is Katalon.

<!--more-->

<p align="center">﷽</p>

مَرْحَبًا يَا رَمَضَان I'm starting write my automation notes at the first of Ramadhan 1446H.

Katalon provides a comprehensive testing solution that covers web, API, mobile, and desktop applications.

- **_Web Testing,_** users can create automated test cases, debug efficiently, and execute tests across multiple browsers.
- **_API Testing_** allows for streamlined validation of various API architectures while integrating seamlessly with web and mobile testing.
- **_Mobile Testing_** supports automation for Android and iOS applications, ensuring compatibility across different devices, browsers, and operating systems.
- **_Desktop Testing_** enables testing of Windows applications, simplifying workflows and facilitating smooth transitions between different applications within a single tool.

This time I will focus on mobile testing.

**_Disclaimer_**
I'm testing in my local machine using Mac M1. If you are using other OS, the steps, commands, and tools may be different.

## Installation

To install Katalon, it's very straightforward. In macOS you just to download it from [here](https://www.katalon.com/download/) then drag it to your applications folder. I'm using Katalon Studio Enterprise (Free trail version) as follow.
![katalon-studio-enterprise](/posts/2025/02/automation-with-katalon/katalon-studio-enterprise.png)

I'm facing some issues when to start Katalon Studio for mobile testing. Some issues are:

- **_Katalon Studio in Mobile Object Spy_**
- Issue: When click start in Mobile Object Spy, I encounter error `Unable to start application Reason: Fail to start Appium server in 60 seconds`

![error-appium-unable-to-start-application](/posts/2025/02/automation-with-katalon/error-appium-unable-to-start-application.png)

I update all appium and node to the latest version as follow:
![node-and-appium-version](/posts/2025/02/automation-with-katalon/node-and-appium-version.png)

If you encounter issue like this:
![katalon-mobile-error-appium-dir-invalid](/posts/2025/02/automation-with-katalon/katalon-mobile-error-appium-dir-invalid.png)

you need to update the appium directory in Katalon Studio. In my case it's in `homebrew`
![appium-directory](/posts/2025/02/automation-with-katalon/appium-directory.png)

_**Before this, I used the [volta](https://docs.volta.sh/guide/getting-started) to manage my node and appium version. But this approach is not working for me.**_

## Mobile Testing

After installing Katalon Studio, I'm able to start my first mobile test. To start a new test, I do some steps:

- click on Katalon sample project
  - click on `Sample Android Mobile Tests Project` wait until the project is loaded
    ![katalon-sample-project](/posts/2025/02/automation-with-katalon/katalon-sample-project.png)
  - Fill the fill new project form then click `OK`
    ![new-project-mobile](/posts/2025/02/automation-with-katalon/new-project-mobile.png)
- click Record Mobile
  ![record-mobile-icon](/posts/2025/02/automation-with-katalon/record-mobile-icon.png)
- In the mobile recorder, you need to configure your device and the `apk` first.
  ![mobile-recorder](/posts/2025/02/automation-with-katalon/mobile-recorder.png)
  **_make sure you emulator or real device already attached and you could test by adb command_**

  ```bash
  adb devices
  ```

  ![adb-devices](/posts/2025/02/automation-with-katalon/adb-devices.png)
  if the device is not attached, you can try to click the `refresh button`

- After that you need to attach the apk file (like in the image above).
- After that you can click `Start` button in the top of the mobile recorder.
- Wait for a while till the app successfully loaded.
  ![app-successfully-loaded-mobile-recorder](/posts/2025/02/automation-with-katalon/app-successfully-loaded-mobile-recorder.png)

- After that you can start to record your test case. In my case, I'm try to search on the search bar. Click search text (marked in no 1) then click `Tap` (marked in no 2) then click `Set Text` (marked in no 3) fill the value to `Android`.
  ![click-element-search](/posts/2025/02/automation-with-katalon/click-element-search.png)

- After that you can see the step already recorded.

![record-actions](/posts/2025/02/automation-with-katalon/record-actions.png)
in my case, I'm continue to create simple step to search and set text `Android`. I'm also try to use the `Tap At Position` and lastly close the app.

![final-result-mobile](/posts/2025/02/automation-with-katalon/final-result-mobile.png)

- Here is the result of my test case `Passed`.

![final-result-passed](/posts/2025/02/automation-with-katalon/final-result-passed.png)

That's it my notes.
