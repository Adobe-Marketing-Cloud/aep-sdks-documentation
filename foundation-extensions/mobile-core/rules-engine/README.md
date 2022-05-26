# Rules Engine

The Rules Engine is provided by the Adobe Experience Platform Mobile SDKs as part of the [MobileCore \(Android\)/ACPCore \(iOS\)](https://app.gitbook.com/@aep-sdks/s/docs/~/drafts/-LzsU1nOc9yXSg36RvlZ/using-mobile-extensions/mobile-core) extension.

In the Experience Platform Mobile SDKs, the Rules Engine enables you to integrate the data and functionality of marketing and ad tech to help disparate products communicate. The Rules Engine looks for the user interaction and associated data, and when the criteria that you defined in the rules are met, the actions that you specified are triggered.

The Rules Engine, when implemented through tags in the [Data Collection UI](https://experience.adobe.com/#/data-collection/), allows for complex if/then/else workflows that can combine multiple solution and extension related behaviors. You can define and capture the necessary user data and orchestrate how each solution contributes to the user's experience.

### **Data elements**

Data elements are the building blocks for the applications data dictionary and are used to collect, organize, and deliver data across marketing and ad technology.

A data element is a variable where the value can be mapped to a Visitor ID, a Carrier Name, an Advertising ID, a Push ID and so on. In Experience Platform Launch, you can reference this value by its variable name. This collection of data elements becomes the dictionary of defined data that you can use to build your rules \(events, conditions, and actions\), and this dictionary is shared across Experience Platform Launch where it can be used with any extension in your property.

### **Rules**

You can define a set of rules in the [Experience Platform Launch](https://experience.adobe.com/#/data-collection/) interface to find specific events or conditions and specify what actions should be triggered when those conditions are met.

![](../../../.gitbook/assets/rule_example.png)

### **Events \(If\)**

The event is defined by selecting an event, the applicable conditions, and the exceptions. An event is what the rules look for, which determines the actions that should be triggered. You can also add multiple event types that can be joined with an OR, and when any of the events are met, the rule's conditions are evaluated.

### **Conditions \(AND/NOT\)**

You can narrow the event by configuring the conditions that must be true for an event to trigger the rule. The AND/NOT conditions are used in the following ways:

* Multiple conditions are joined with an AND, which is also known as the Regular Logic Type. 
* For included exceptions, use the NOT condition, which is also called the Exception Logic Type. 

### **Exception**

An exception is defined as a NOT condition, and this condition excludes a specific behavior that might be included as part of the defined conditions.

### **Actions \(Then\)**

An action, also known as a consequence, triggers an event after a rule's events have occurred, and the conditions in the rule have evaluated to `true`. A rule in Experience Platform Launch can trigger as many discrete actions as you want. For example, a rule can be triggered to set and send a data element’s value to Adobe Analytics and send the same set of data to a third-party extension. You do not need to create separate rules for each extension or tag.

Rules include data elements, events, conditions, and actions that are provided by the relevant extensions. These rules can be modified at any time and are saved and published as a new library that the SDK downloads as the latest set of rules.

### **Loading and processing the Rules JSON file by the Rules Engine**

At the start of a new application session that includes the Experience Platform Mobile SDK, the Rules Engine gets the static endpoint of the Rules JSON file that is defined as part of the SDK configuration, loads the latest version of this rules file, and monitors the events in the SDK. When an event matches the defined conditions in the rules, the Rules Engine sends an action to the respective extensions with an extension-specific payload. Rule matching is completed by checking whether a defined set of conditions is met.

**Tip**: Conditions can be one match or a group of matches.

### **Re-evaluating events**

On older versions of Experience Platform Mobile SDKs \(prior to iOS version 1.6.2, Android version 1.5.4\), after the first launch of the app, it always takes some time to download the rules from the remote servers. During this time, Rules Engine won't be able to evaluate the first several events until the rules are loaded. Starting from iOS version 1.6.2 and Android version 1.5.4, we add the capability to cache the events before the rules are downloaded and will re-evaluate those events afterward. This change is mainly to enable the trigger of Posback based on the install event.

### Using Bundled Rules (iOS AEP 3.x Only)

In addition to the remote configuration, you can also include a rules zip file in your app bundle to be used by the SDK before rules have been downloaded from the Data Collection UI. To add bundled rules to your app, follow these steps:
1. Download the rules zip file using the following URL: `https://assets.adobedtm.com/PASTE-ENVIRONMENT-ID-rules.zip` replacing `PASTE-ENVIRONMENT-ID` with your mobile property environment ID. 
2. Rename the zip file to "ADBMobileConfig-rules.zip" and place the zip anywhere that it is accessible in your app bundle.

For more information about the technical details of the Rules Engine, see [Rules Engine technical details](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-details).

## Watch the Video

{% embed url="https://www.youtube.com/watch?v=BwBeYNu5Crg" caption="Video: How to configure IFTTT mobile rules in Adobe Experience Platform Launch" %}

