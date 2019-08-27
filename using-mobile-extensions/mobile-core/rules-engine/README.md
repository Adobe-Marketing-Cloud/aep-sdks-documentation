# Rules Engine

The Rules Engine is provided by Adobe Experience Platform Mobile SDK as part of the MobileCore (Android)/ACPCore (iOS) extension.

If you are using the Experience Platform Mobile SDKs, the Rules Engine enables you to integrate the data and functionality of marketing and ad tech to help disparate products communicate. The Rules Engine looks for the user interaction and associated data, and when the criteria that you defined in the rules are met, the actions that you specified are triggered.

The Rules Engine, with [Experience Platform Launch](https://launch.adobe.com/)'s tag management system, allows for complex if/then/else workflows that can combine multiple solution and extension related behaviors. You can define and capture the necessary user data and orchestrate how each solution contributes to the user's experience.

**Data Elements** 

Data elements are the building blocks for the applications data dictionary and are used to collect, organize, and deliver data across marketing and ad technology.

A data element is a variable where the value can be mapped to a Visitor ID, a Carrier Name, an Advertising ID, a Push ID and so on. In Experience Platform Launch, you can reference this value by its variable name. This collection of data elements becomes the dictionary of defined data that you can use to build your rules (events, conditions, and actions). This data dictionary is shared across Experience Platform Launch where it can be used with any extension in your property.

**Rules**

You can define a set of rules in the [Experience Platform Launch](https://launch.adobe.com/) interface to find specific events or conditions and specify what actions should be triggered when those conditions are met.

![](Rule_Example.png)

**Events (If)** 

The event is defined by selecting an event, the applicable conditions, and the exceptions. An event is what the rules look for, which determines the actions that should be triggered. You can also add multiple event types that can be joined with an OR, and when any of the events are met, the rule's conditions are evaluated.

**Conditions (AND/NOT)**

You can narrow the event by configuring the conditions that must be true for an event to trigger the rule. Use the AND/NOT conditions in the following ways:

- Multiple conditions are joined with an AND, also called Regular Logic Type. 
- For included exceptions, use the NOT condition, also called Exception Logic Type. 

**Exception** 

An exception is defined as a NOT condition, and this condition excludes a specific behavior that might be included as part of the defined conditions.

**Actions (Then)**

An action, also known as a consequence, triggers an event after a rule's events have occurred, and the conditions in the rule have evaluated to `true`. A rule in Experience Platform Launch can trigger as many discrete actions as you want. For example, a rule can be triggered to set and send a data element’s value to Adobe Analytics and send the same set of data to a third-party extension. You do not need to create separate rules for each extension or tag. 

Rules include data elements, events, conditions, and actions that are provided by the relevant extensions. These rules can be modified at any time and are saved and published as a new library that the SDK downloads as the latest set of rules.

**Loading and Processing rules JSON file by the Rules Engine** 

At the start of a new application session that includes the Experience Platform Mobile SDK, the Rules Engine gets the static endpoint of the Rules JSON file that is defined as part of the SDK configuration, loads the latest version of this rules file, and monitors the events in the SDK. When an event matches the defined conditions in the rules, the Rules Engine sends an action to the respective extensions with an extension-specific payload. Rule matching is completed by checking whether a defined set of conditions is met.

**Tip**: Conditions can be a one match or a group of matches.

Technical details of the Rules Engine can be found from [Rules Engine technical details page](rules-engine-details.md)