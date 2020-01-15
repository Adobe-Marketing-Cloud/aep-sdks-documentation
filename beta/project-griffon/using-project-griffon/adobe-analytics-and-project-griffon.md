# Adobe Analytics and Project Griffon

## Overview

The Adobe Analytics view is focused, yet richer view of SDK events only related to your Adobe Analytics implementation. The view now shows the action/state name and event “status” along with a specifically formatted detail view. 

Status tells you when an SDK event is generated \(processed\), if the SDK has made a network request with Adobe Analytics \(queued\), and if we’ve returned post-processing information from Adobe Analytics about that event \(validated\).

Generally speaking, for a given Analytics track event – the detailed view contains 3 valuable pieces:

* Originating SDK Analytics request event
* OOTB meta and context data from the request \(such as report suite ID, SDK extension versions, OOTB context data, etc.\) and
* Post-processed information on the Analytics event \(contains mapping of revars, evars, props, etc.\).

## Using Project Griffon for Adobe Analytics

Follow these steps to get started:

1. Ensure you have implemented the latest versions of [Project Griffon](../set-up-project-griffon.md) and [Adobe Analytics](../../../using-mobile-extensions/adobe-analytics/) extensions
2. Visit https://experience.adobe.com/griffon \(not griffon.adobe.com\).
3. Connect your app to a Project Griffon session
4. Select the new Adobe Analytics view \(per the screenshot below\) to view your events.

![](../../../.gitbook/assets/screen-shot-2020-01-13-at-12.04.14-pm.png)



