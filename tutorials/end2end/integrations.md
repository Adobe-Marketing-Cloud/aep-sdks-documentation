---
title: Implement Experience Cloud Integrations with Launch
description: Learn how to validate the Audiences, A4T, and Customer Attributes integrations in your Adobe Experience Cloud implementation. This lesson is part of the Implementing the Experience Cloud in Websites with Launch tutorial.
seo-description:
seo-title: Implement Experience Cloud Integrations with Launch
solution: Experience Cloud
---

# Experience Cloud Integrations

In this lesson, you will review the key integrations between the solutions you  just implemented. The good news is that by completing the earlier lessons, you have already implemented the code-aspects of the integrations! You don't need to do any additional work in this lesson besides reading and validating.

## Learning Objectives

At the end of this lesson, you will be able to:

1. Explain the basic use cases for Audience Sharing, Analytics for Target (A4T) and Customer Attributes integrations
1. Validate the basic client-side implementation aspects of these integrations

## Prerequisites

You should complete all of the previous lessons in this tutorial before following the  instructions in this lesson.

>[!NOTE] There are many user-permissions requirements, account configurations, and provisioning steps are required to fully use these integrations and which are beyond the scope of this tutorial. If you are not already using these integrations in your current implementation of the Experience Cloud, you should consider the following:
>
> * Review the full requirements of the [Core Services integrations](https://marketing.adobe.com/resources/help/en_US/mcloud/core_services.html)
> * Review the full requirements of the [Analytics for Target integration](https://marketing.adobe.com/resources/help/en_US/target/a4t/c_before_implement.html)
> * Have an Administrator of your Experience Cloud Organization [request provisioning of these integrations](https://www.adobe.com/go/audiences)

## Audiences

[Audiences](https://marketing.adobe.com/resources/help/en_US/mcloud/audience_library.html) is part of the People Core Service and allows you to share audiences between solutions. For example you can create an audience in Audience Manager and use it to deliver personalized content with Target.

The main requirements to implement A4T&mdash;which you have already done&mdash;are to:

1. Implement the Experience Cloud Id Service
1. Implement Audience Manager
1. Implement other solutions which you would like to receive or create audiences, such as Target and Analytics

### Validate the Audiences integration

The best way to validate the Audiences integration is to actually build an audience, share it to another solution, and then fully use it in the other solution (e.g. confirm that a visitor who qualifies for an AAM segment can qualify for a Target activity targeted to that segment). However, this is beyond the scope of this tutorial.

These validation steps will focus on the critical part visible in the client-side implementation--the Visitor ID.

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the XYZ

   ![Your Launch development environment shown in Debugger](images/web-switchEnvironments-debuggerOnWeRetail.png)

1. Go to the Network tab of the Debugger

1. Click **[!UICONTROL Clear All Requests]** just to clean things up

1. Reload the We.Retail page, making sure that you see both the Target and Analytics requests in the Debugger

1. Reload the We.Retail page again
  
1. You should now see four requests in the Network tab of the Debugger&mdash;two for Target and two for Analytics

1. Look in the row labeled "Experience Cloud Visitor ID." The IDs in every request by every solution should always be the same.

   ![Confirm the matching SDIDs](images/web-integrations-matchingECIDs.png)

1. The IDs are unique per visitor, which you can confirm by asking a co-worker to repeat these steps.

## Analytics for Target (A4T)

The [Analytics for Target (A4T)](https://marketing.adobe.com/resources/help/en_US/target/a4t/a4t.html) integration allows you to leverage your Analytics data as the source for reporting metrics in Target.  

The main requirements to implement A4T&mdash;which you have already done&mdash;are to:

1. Implement the Experience Cloud Id Service
1. Fire the global mbox before the Analytics page view beacon

A4T works by stitching together a server-side request from Target to Analytics with the Analytics page view beacon, which we call "hit-stitching."  Hit-stitching requires that the Target request which delivers the activity (or increments a Target-based goal metric) have a parameter which matches a parameter in the Analytics page view beacon. This parameter is called the supplemental data id (SDIDs).

### Validate the A4T Implementation

The best way to validate the A4T integration is to actually build a Target activity using A4T and validate the reporting data, however this is beyond the scope of this tutorial. This tutorial will show you how to confirm that the supplemental data ids match between the solution calls.

**To validate the SDIDs**

1. Open the [We.Retail site](https://aem.enablementadobe.com/content/we-retail/us/en.html)

1. Make sure the Debugger is mapping the Launch property to *your* Development environment, as described in the XYZ
   ![Your Launch development environment shown in Debugger](images/web-switchEnvironments-debuggerOnWeRetail.png)

1. Go to the Network tab of the Debugger

1. Click **[!UICONTROL Clear All Requests]** just to clean things up

1. Reload the We.Retail page, making sure that you see both the Target and Analytics requests in the Debugger

1. Reload the We.Retail page again
  
1. You should now see four requests in the Network tab of the Debugger&mdash;two for Target and two for Analytics

1. Look in the row labeled "Supplemental Data ID." The IDs from the first page load should match between Target and Analytics. The IDs from the second page load should also match, but be different from the first page load.

   ![Confirm the matching SDIDs](images/web-integrations-matchingSDIDs.png)

If you make additional Target requests in the scope of a page load (not including single-page apps) that are part of A4T activities, it's good to them unique names (not target-global-mbox) so that they will continue to have the same SDIDs of the initial Target and Analytics requests.

## Customer Attributes

[Customer Attributes](https://marketing.adobe.com/resources/help/en_US/mcloud/attributes.html) is a part of the People Core Service that allows you to upload data from your customer relationship management (CRM) database and leverage it in Adobe Analytics and Adobe Target.

The main requirements to implement Customer Attributes&mdash;which you have already done&mdash;are to:

1. Implement the Experience Cloud Id Service
1. Set Customer Ids via the Id Service *before* Target and Analytics fire their requests (which you accomplished using the rule ordering feature in Launch)

### Validate the Customer Attributes Implementation

You have already validated that the Customer IDs are passed to both the ID Service and to Target. No additional steps necessary!

[Next "Publish your Property" >](publish.md)