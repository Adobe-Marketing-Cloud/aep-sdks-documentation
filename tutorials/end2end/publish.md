---
title: Publish your Launch Property
description: Learn how to publish your Launch property from the Development environment to the Staging and Production environments. This lesson is part of the Implementing the Experience Cloud in Websites with Launch tutorial.
seo-description:
seo-title: Publish your Launch Property
solution: Experience Cloud
---

# Publish your Launch Property

Now that you have implemented some key solutions of the Adobe Experience Cloud in your Development environment, it's time to learn the publishing workflow.

## Learning Objectives

At the end of this lesson, you will be able to:

1. Publish a Development library to the Staging environment
1. Map a Staging library to your production website using the Debugger
1. Publish a Staging library to the Production environment

## Publish to Staging

 Now that you have created and validated your library in the Development environment, it is time to publish it to Staging.

1. Go to the **[!UICONTROL Publishing]** page

1. Open the dropdown next to your library and select **[!UICONTROL Submit for Approval]**

   ![Submit for Approval](images/web-publishing-submitForApproval.png)

1. Click the **[!UICONTROL Submit]** button in the dialog:

   ![Click Submit in the Modal](images/web-publishing-submit.png)

1. Your library will now appear in the [!UICONTROL Submitted] column in an unbuilt state:

1. Open the dropdown and select **[!UICONTROL Build for Staging]**:

   ![Build for Staging](images/web-publishing-buildForStaging.png)

1. Once the green-dot icon appears, the library can be previewed in the Staging environment.

In a real-life scenario, the next step in the process would typically be to have your QA team validate the changes in the Staging library. They can do this using the Debugger.

**To Validate the Changes in the Staging Library**

1. In your Launch property, open the [!UICONTROL Environments] page

1. In the [!UICONTROL Staging] row, click the Install icon

   ![Install icon](images/web-launch-installIcon.png) to open the modal
   ![Go to the Environments page and click to open the modal](images/web-publishing-getStagingCode.png)

1. Click the Copy icon ![Copy icon](images/mobile-launch-copyIcon.png) to copy the embed code to your clipboard

1. Click **[!UICONTROL Close]** to close the modal

   ![Install icon](images/web-publishing-copyStagingCode.png)

1. Open the [We.Retail demo site](https://aem.enablementadobe.com/content/we-retail/us/en.html) in your Chrome browser

1. Open the [Experience Cloud Debugger extension](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) by clicking the ![Debugger Icon](images/web-icon-debugger.png) icon

   ![Click the Debugger icon](images/web-switchEnvironments-openDebugger.png)

1. Go to the Tools Tab

1. Click **[!UICONTROL Adobe Launch > Dynamically Insert Launch > Embed Code]** button to open the text input field (it might currently have the URL of your Development embed code):

   ![Click the Adobe Launch > Dynamically Insert Launch > Embed Code button](images/web-switchEnvironments-debugger-editEmbedCode.png)

1. Paste the Staging embed code that is in your clipboard

1. Click the disk icon to save

   ![Launch environment shown in Debugger](images/web-switchEnvironments-debugger-save.png)

1. Reload and check the Summary tab of the Debugger. Under the Launch section, you should now see your Staging Property is implemented, showing your property name (I.e. "Launch Tutorial" or whatever you named your property)!

   ![Launch environment shown in Debugger](images/web-publishing-debugger-staging.png)

In real-life, once your QA team has signed off by reviewing the changes in the Staging environment it is time to publish to production.

## Publish to Production

1. Go to the [!UICONTROL Publishing] page

1. From the dropdown, click **[!UICONTROL Approve for Publishing]**:

   ![Approve for Publishing](images/web-publishing-approveForPublishing.png)

1. Click the **[!UICONTROL Approve]** button in the dialog box:

   ![Click Approve](images/web-publishing-approve.png)

1. The library will now appear in the [!UICONTROL Approved] column in the unbuilt state (yellow dot):

1. Open the dropdown and select **[!UICONTROL **Build and Publish to Production]**:

   ![Click Build &amp; Publish to Production](images/web-publishing-buildAndPublishToProduction.png)

1. Click the **[!UICONTROL Publish]** in the dialog box:

   ![Click Publish](images/web-publishing-publish.png)

1. The library will now appear in the [!UICONTROL Published] column:

   ![Published](images/web-publishing-published.png)

That’s it! You've completed the tutorial and published your first property in Launch!