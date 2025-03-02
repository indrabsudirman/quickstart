---
title: Automation With Katalon (Mobile Testing)
date: 2025-02-28T19:19:10+07:00
lastmod: 2025-03-01T19:19:10+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
# https://chatgpt.com/share/67b8a04f-6e84-8009-8a50-7f02c82812ed
cover: katalon-logo-mobile-testing.png
# images:
#   - /img/cover.jpg
categories:
  - automation
  - katalon
tags:
  - katalon-mobile-testing
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
![katalon-studio-enterprise](/posts/2025/02/automation-with-katalon-mobile-testing/katalon-studio-enterprise.png)

I'm facing some issues when to start Katalon Studio for mobile testing. Some issues are:

- **_Katalon Studio in Mobile Object Spy_**
- Issue: When click start in Mobile Object Spy, I encounter error `Unable to start application Reason: Fail to start Appium server in 60 seconds`

![error-appium-unable-to-start-application](/posts/2025/02/automation-with-katalon-mobile-testing/error-appium-unable-to-start-application.png)

I update all appium and node to the latest version as follow:
![node-and-appium-version](/posts/2025/02/automation-with-katalon-mobile-testing/node-and-appium-version.png)

If you encounter issue like this:
![katalon-mobile-error-appium-dir-invalid](/posts/2025/02/automation-with-katalon-mobile-testing/katalon-mobile-error-appium-dir-invalid.png)

you need to update the appium directory in Katalon Studio. In my case it's in `homebrew`
![appium-directory](/posts/2025/02/automation-with-katalon-mobile-testing/appium-directory.png)

_**Before this, I used the [volta](https://docs.volta.sh/guide/getting-started) to manage my node and appium version. But this approach is not working for me.**_

## Mobile Testing (Android)

After installing Katalon Studio, I'm able to start my first mobile test. To start a new test, I do some steps:

- click on Katalon sample project
  - click on `Sample Android Mobile Tests Project` wait until the project is loaded
    ![katalon-sample-project](/posts/2025/02/automation-with-katalon-mobile-testing/katalon-sample-project.png)
  - Fill the fill new project form then click `OK`
    ![new-project-mobile](/posts/2025/02/automation-with-katalon-mobile-testing/new-project-mobile.png)
- click Record Mobile
  ![record-mobile-icon](/posts/2025/02/automation-with-katalon-mobile-testing/record-mobile-icon.png)
- In the mobile recorder, you need to configure your device and the `apk` first.
  ![mobile-recorder](/posts/2025/02/automation-with-katalon-mobile-testing/mobile-recorder.png)
  **_make sure you emulator or real device already attached and you could test by adb command_**

  ```bash
  adb devices
  ```

  ![adb-devices](/posts/2025/02/automation-with-katalon-mobile-testing/adb-devices.png)
  if the device is not attached, you can try to click the `refresh button`

- After that you need to attach the apk file (like in the image above).
- After that you can click `Start` button in the top of the mobile recorder.
- Wait for a while till the app successfully loaded.
  ![app-successfully-loaded-mobile-recorder](/posts/2025/02/automation-with-katalon-mobile-testing/app-successfully-loaded-mobile-recorder.png)

- After that you can start to record your test case. In my case, I'm try to search on the search bar. Click search text (marked in no 1) then click `Tap` (marked in no 2) then click `Set Text` (marked in no 3) fill the value to `Android`.
  ![click-element-search](/posts/2025/02/automation-with-katalon-mobile-testing/click-element-search.png)

- After that you can see the step already recorded.

![record-actions](/posts/2025/02/automation-with-katalon-mobile-testing/record-actions.png)
in my case, I'm continue to create simple step to search and set text `Android`. I'm also try to use the `Tap At Position` and lastly close the app.

![final-result-mobile](/posts/2025/02/automation-with-katalon-mobile-testing/final-result-mobile.png)

- Here is the result of my test case `Passed`.

![final-result-passed](/posts/2025/02/automation-with-katalon-mobile-testing/final-result-passed.png)

## Mobile Testing (iOS)

- click on Katalon sample project

  - click on `Sample iOS Mobile Tests Project` wait until the project is loaded
    ![katalon-sample-project](/posts/2025/02/automation-with-katalon-mobile-testing/katalon-sample-project-android-ios.png)
  - Fill the fill new project form then click `OK`
    ![new-project-mobile](/posts/2025/02/automation-with-katalon-mobile-testing/new-project-mobile-ios.png)
  - click Record Mobile
    ![record-mobile-icon](/posts/2025/02/automation-with-katalon-mobile-testing/record-mobile-icon.png)
    > There is a little bit difference between `Android` and `iOS`. In `iOS` you need to select `iOS` simulator in the `Device Type` field without run the simulator first.
    > ![device-list-name-ios-simulator](/posts/2025/02/automation-with-katalon-mobile-testing/device-list-name-ios-simulator.png)
  - click Start - Wait for a while till the app successfully loaded. - If you encounter issue like this:
    ![could-not-start-response-500](/posts/2025/02/automation-with-katalon-mobile-testing/could-not-start-response-500.png) some tips:
    - Update the Appium log level to `Debug` in Katalon Settings Mobile. This will help you to debug the issue.
    - Follow some tips in the link [common webdriveragent installation issues](https://docs.katalon.com/katalon-studio/troubleshooting/troubleshoot-mobile-automated-testing/common-webdriveragent-installation-issues)
  - Now, you can start to record your test case.
    ![mobile-recorder-successfuly-loaded-ios](/posts/2025/02/automation-with-katalon-mobile-testing/mobile-recorder-successfuly-loaded-ios.png)

  - Let's do some simple test case, similar to Android above.
    - Click on `Search Wikipedia` (marked in no 1).
      ![start-record-mobile-ios](/posts/2025/02/automation-with-katalon-mobile-testing/start-record-mobile-ios.png)
    - Click `Tap` (marked in no 2).
      ![click-tap-search-wikipedia](/posts/2025/02/automation-with-katalon-mobile-testing/click-tap-search-wikipedia.png)
    - The `Tap` action above will redirect to the Edit Text `Search Wikipedia`.
      ![edittext-search-wikipedia-ios](/posts/2025/02/automation-with-katalon-mobile-testing/edittext-search-wikipedia-ios.png)
    - Click `Set Text` and fill `Android`.
      ![fill-android-edittext-search-wikipedia-ios](/posts/2025/02/automation-with-katalon-mobile-testing/fill-android-edittext-search-wikipedia-ios.png)
    - Finally, the Android result will appear.
      ![final-page-wikipedia-ios](/posts/2025/02/automation-with-katalon-mobile-testing/final-page-wikipedia-ios.png)
    - Now you can save the script, by click `Save Script` button.
      - In my case I name the testcase as `User able to search at EditText Search`.
        ![save-the-script-and-name-the-testcase](/posts/2025/02/automation-with-katalon-mobile-testing/save-the-script-and-name-the-testcase.png)
    - So when click `Run` button, the choose IOS simulator will appear.
      ![run-ios](/posts/2025/02/automation-with-katalon-mobile-testing/run-ios.png)
    - Finally, the result will appear.
      ![ios-passed](/posts/2025/02/automation-with-katalon-mobile-testing/ios-passed.png)
      That's it my notes.
