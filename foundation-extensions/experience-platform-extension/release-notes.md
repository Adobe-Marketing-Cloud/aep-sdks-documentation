# Release Notes

## Sept 3, 2021

### Adobe Experience Platform Edge Network Launch extension v1.0.12

- New `Forward to Edge Network` action to be used with Mobile Core Application Lifecycle events.

## Sept 2, 2021

### iOS AEPEdge 1.1.2

* Edge Network Extension now honors the timestamp set in XDM payload of Experience Event. If no timestamp is set, then timestamp of `Edge.sendEvent()` API call is used.

### Android Edge 1.1.2

* Edge Network Extension now honors the timestamp set in XDM payload of Experience Event. If no timestamp is set, then timestamp of `Edge.sendEvent()` API call is used.

## June 10, 2021

### iOS AEPEdge 1.1.1

* Development testing enhancements for Experience Edge.

### Android Edge 1.1.1

* Adds support for events persistence for use-cases with low network connectivity or unexpected network errors.
* Development testing enhancements for Experience Edge.

This SDK is compatible with Android Core 1.8.2 and above.

## April 8, 2021

### iOS AEPEdge 1.1.0

* Integration with AEPEdgeConsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
* Adds required dependency on AEPEdgeIdentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

### Android Edge 1.1.0

* Integration with edgeconsent 1.0.0 and collect consent preferences enforcement on requests to AEP Edge Network.
* Adds required dependency on edgeidentity 1.0.0 that brings XDM IdentityMap support for custom identifiers.

## January 19, 2021

### iOS AEPEdge 1.0.0

The Adobe Experience Platform Edge Network (AEPEdge) mobile extension is now available in iOS! This extension allows for sending XDM formatted data to Adobe Experience Platform and Adobe Experience Cloud solutions, by leveraging Experience Edge capabilities.

The included features with this release are:

* Ability to create XDM Experience Events and send them to Experience Edge Network. An optional Experience Edge response callback can be registered per event.
* The XDM Experience Events can be sent to individual Adobe Experience Platform datasets when a custom dataset identifier is set at event level.
* Events persistence.
* ECID is automatically attached on each XDM Experience Event request.
* Integration with AEPAssurance extension enabling new insights in Project Griffon about the XDM Experience Event processing and XDM data validation for an improved validation and debugging experience. 
* Detailed warning/error messages are available through Project Griffon UI and logs.

Learn more about the AEP Edge extension in the open sourced [adobe/aepsdk-edge-ios](https://github.com/adobe/aepsdk-edge-ios) GitHub repository. The iOS SDK is available for installation through SPM, XCFramework and Cocoapods and can be used in Swift and Objective-C applications. This SDK is compatible with latest swift AEPCore 1.0.0.

### Android Edge 1.0.0

The Adobe Experience Platform Edge Network (Edge) mobile extension is now available in Android! This extension allows for sending XDM formatted data to Adobe Experience Platform and Adobe Experience Cloud solutions, by leveraging Experience Edge capabilities.

The included features with this release are:

* Ability to create XDM Experience Events and send them to Experience Edge Network. An optional Experience Edge response callback can be registered per event.
* The XDM Experience Events can be sent to individual Adobe Experience Platform datasets when a custom dataset identifier is set at event level.
* ECID is automatically attached on each XDM Experience Event request.
* Integration with Assurance extension enabling new insights in Project Griffon about the XDM Experience Event processing and XDM data validation for an improved validation and debugging experience. 
* Detailed warning/error messages are available through Project Griffon UI and logs.

This SDK is compatible with Android Core 1.5.7 and above.

### Adobe Experience Platform Edge Network Launch Extension 1.0.2

* Selector for the Edge Configuration.
* AEP Request Event with optional XDM event type is available for Launch rules.

