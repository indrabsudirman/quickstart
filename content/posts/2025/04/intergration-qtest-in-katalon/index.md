---
title: Intergration QTest in Katalon Studio
date: 2025-04-19T14:12:42+07:00
lastmod: 2025-04-19T14:12:42+07:00
author: Indra Sudirman
avatar: /img/indra.png
# authorlink: https://author.site
cover: qTest-katalon-integration.png
# images:
#   - /img/cover.jpg
categories:
  - automation
  - katalon
  - qtest
tags:
  - katalon
  - automation testing
  - qa-automation
  - testing
# nolastmod: true
draft: false
---

As QA teams begin adopting Automation Testing to streamline processes like Regression Testing, one of the initial steps is often integrating their existing test management tools with an automation framework. This post provides a guide on how to integrate qTest, a popular test management tool, with Katalon, an automation testing framework.

<!--more-->

<p align="center">﷽</p>

## Background

qTest is a comprehensive test management tool that provides features such as test planning, execution, reporting, and integration with other tools. Before adopting automation testing, most QA teams rely heavily on manual testing and use test management tools to plan, execute, and track their tests—entirely manually. Over time, this leads to hundreds or even thousands of test cases being stored in the test management tool.

So, when the time comes to shift towards automation, it's essential to integrate your test management tool with your automation framework. This ensures that all those existing test cases can be effectively reused and managed within the automated testing workflow.

This notes will focus on how to integrate qTest with Katalon using the qTest plugin for Katalon.

## Download qTest Plugin

To integrate qTest with Katalon, you need to download the qTest plugin for Katalon. You can find the plugin on the qTest website: [https://store.katalon.com](https://store.katalon.com/product/136/qTest-Integration).
![qTest Plugin in Katalon Store](qtest-plugin-in-katalon-store.png)

> Please note that you need to have a Katalon account to download the plugin. The account must be same as Katalon Studio account that you use to access the plugin.

## Configure qTest Plugin for Katalon

Once you have downloaded the plugin, you need to configure it with your qTest account in the Katalon Studio. Follow the steps below to configure the plugin:

1. Open the Katalon Studio in your local machine.

   Some tips are:

   - Make sure your Katalon Studio account is the same as in Katalon Store when you download the qTest plugin.

2. To verify the plugin is installed, click user icon in the top right corner of the Katalon Studio. Try to reload the plugin by clicking the "Reload Plugins" button.
   ![Katalon Studio User Icon](reload-plugin-katalon.png)
   wait until the plugins list is reloaded. You will see the qTest plugin in successfully installed.
   ![qTest Plugin in Katalon Studio](plugins-list.png)
   then close the plugin popup.
3. Click on the `Project` then click on the `Settings` button.
   ![Katalon Studio Project Settings](project-setting.png)

4. The `Project Settings` popup will open. Expand on the `Plugins` the click on the `qTest`.
   ![qTest Plugin Settings in Katalon Studio](plugins-qTest-settings.png)

   > at this popup, you need to fill the following fields, please follow the instructions below carefully. Since I have spent some time to understand, how to configure the qTest plugin correctly. Otherwise, you might face some issues, like the qTest project won't be loaded.
   > ![qTest Project Not Loaded in Katalon Studio](qTest-project-not-loaded.png)

5. Fill the following fields:

   - Tick the `Enable Integration`.
   - Fill the `Token` with your qTest's token.
     - The `qTest` token can be found in your qTest account.
     - Choose the qTest project (any project, since the `arrow down icon` will shown if you have already selected a project), then you will find the `arrow down icon` on the right side. Click on the `arrow down icon`.
       ![qTest Project Selection](qTest-sample-project.png)
     - You will be redirected to the `Download qTest Resources` page. Click on the `API & SDK` button.
       ![qTest Download Resources](qTest-resources-page.png)
     - Now you will see the qTest `Token`. Then copy the token value.
       ![qTest Token](qTest-token.png)
   - Finally the popup should look like this:
     ![qTest Plugin Settings in Katalon Studio](qTest-plugin-settings-katalon.png)
     You could tick some options in the `Test Result` and `Report format` based on your needs.

6. Click on the `Quick Setup` text on the top right side, based on image above. The `qTest Integration Setup Wizard` will open.
   ![qTest Integration Wizard](qTest-integration-setup-wizard.png)
   Fill the following fields:

   - `qTest Version` choose the latest version. Now it's 7 or higher.
   - `Server URL` fill with your qTest server URL. For example https://Your_QTest_Subdomain.qtestnet.com
   - `Username` fill with your qTest username.
   - `Password` fill with your qTest password.
   - `Encrypt authentication data` tick the checkbox. Since this recommendation from Katalon.

7. Click on the `Connect account` button. Wait until the connection is successful.
   ![qTest Integration Wizard](qTest-integration-setup-wizard-connect-account-success.png)

8. Click on the `Next` button. If everything is correct, you will see the `qTest Project` is loaded.
   ![qTest Integration Wizard](qTest-integration-setup-wizard-project-loaded.png)
   since I haven't create any qTest project, the project list only show the `qConnect - Sample Project`.
   But is ok, since before I have an issue the qTest project won't be loaded.
   Now, choose the project that you want to use then click on the `Next` button.

9. Now you will see the `qTest Module` is loaded.
   ![qTest Integration Wizard](qTest-integration-setup-wizard-module-loaded.png)
   Choose the `qTest Module` that you want to use then click on the `Next` button.

10. Now choose the `Katalon Test Case Folder` by default, the folder will be in `Katalon Test Cases.` Leave it default then click on the `Next` button.
    ![Katalon Test Case Folder](katalon-test-case-folder.png)

11. Now choose the `Katalon Test Suites Folder` by default, the file will be in `Katalon Test Suites.` Leave it default then click on the `Next` button.
    ![Katalon Test Case File](katalon-test-suite-folder.png)

12. Now tick some options in the `Katalon Execution Options` based on your needs.
    ![Katalon Execution Options](katalon-execution-option.png)
    Then click on the `Next` button.

13. Now you will see the message `The Finish Up` successfully. Click on the `Finish` button.
    ![qTest Finish Up](finish-up-katalon-qtest.png)

That's all my notes.

Reference:

- [qTest Integration in Katalon](https://docs.katalon.com/katalon-studio/integrations/test-management/configure-qtest-integration-in-katalon-studio)(This docs missing step how to get qTest token, so it will be a little bit confusing)
