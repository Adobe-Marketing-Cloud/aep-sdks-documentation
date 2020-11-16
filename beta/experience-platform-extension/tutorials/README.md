# Tutorials

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more and get access to the materials for these tutorials.
{% endhint %}

## Beta Schedule

### Assignment 1 (week Oct 20)

In this assignment you will learn how to:

1. Create a schema, a dataset and generate a configuration identifier in Adobe Experience Platform Launch 
2. Get familiar with the sample demo applications \(iOS Swift, Android\)
3. Setup Project Griffon and use it for validating XDM events
4. Query the commerce events in Adobe Experience Platform
5. Implement new XDM Experience events for a given XDM schema

Get started with [Assignment 1 - AEP Edge extension setup and XDM usage](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-1-edge-extension-setup).

#### Prepare to provide feedback on:

* [ ] Overall setup and implementation workflow
* [ ] Ease of use for the AEP Edge SDK APIs \(creating and sending XDM Experience events\)
* [ ] XDM implementation validation
* [ ] Clarity of documentation during the beta review call

### Assignment 2 (week Oct 27)

In this assignment you will learn how to:

1. Install Swift Core library using Cocoapods
2. Initialize SDK with new API
3. Start/Stop lifecycle
4. Make an Identity call

Get started with [Assignment 2 - Swift Core setup](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-2-swift-core-setup).

#### Prepare to provide feedback on:

* [ ] Overall setup and implementation workflow of AEPCore SDK
* [ ] In `Podfile`, instead of just including ACPCore, you now need to include AEPCore, AEPServices, AEPLifecycle, AEPIdentity, and AEPSignal. This allows greater flexibility for both developers and consumers of the SDK to only include what they need. Do you feel the trade-off is an overall benefit?
* [ ] SPM vs Cocoapod - which dependency mangament tool are you using today? Are you considering adopting or changing dependency management tools in the near future?
* [ ] Are your apps currently built with Obj-C, Swift, or a combination of the two?

Feedback or questions can be posted to [Experience Edge Beta - Swift SDK Feedback](https://github.com/adobe/aepsdk-core-ios/issues/427).

### Assignment 3 (week Nov 3)

In this assignment you will learn how to:

1. Implement XDM Experience Events using Schema representations or dictionaries
2. Use multiple schemas and datasets
3. Sync identities in XDM format
4. View the Real-time Customer Profile in Adobe Experience Platform

Get started with [Assignment 3 - XDM implementation](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-3-xdm-implementation).

#### Prepare to provide feedback on:

* [ ] Ease of use for the AEP Edge SDK APIs and select datasets
* [ ] Use-cases when XDM client-side events can be used over remote rules
* [ ] Use-cases where multiple schemas and/or datasets can be used
* [ ] What type of visitor identifiers do you currently sync using the AEP SDK?
* [ ] Do you prefer syncing the visitor identifiers using a specialized API (example [syncIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#syncidentifier)), XDM format, remote rules or a combination of these?

### Assignment 4 (week Nov 10)

In this assignment you will learn how to:

1. Update an existing XDM Schema
2. Create data elements and rules for mobile properties in Adobe Experience Launch
3. Attach new data to XDM events
4. Validate the rules are executed correctly with AEP Assurance (Project Griffon).

Get started with [Assignment 4 - Rules for XDM events](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-4-rules-xdm-events).

#### Prepare to provide feedback on:

* [ ] General feedback about mobile data elements and rules usage
* [ ] Examples of mobile rules used in your experience
* [ ] Ease to validate rules execution when using the AEP Mobile SDK
* [ ] What validation techniques do you use when configuring rules remotely

### Assignment 5 (week Nov 17)

In this assignment you will learn how to:

1. Configure Analytics using the Edge Configuration.
2. Include Analytics Edge extension in sample apps
3. Review trackAction and trackState calls​

Get started with [Assignment 5 - Analytics edge extension](./tutorial-5-analytics-edge-extension.md).

#### Prepare to provide feedback on:

* [ ] General feedback about setup and configuration of AnalyticsEdge extension
* [ ] Support existing analytics workflows with this extension 
