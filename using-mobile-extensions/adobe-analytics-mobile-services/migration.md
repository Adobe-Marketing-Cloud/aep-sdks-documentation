# Migration to AEPMobileServices

This document is a reference comparison of ACPMobileServices(1.x) APIs against their equivalent APIs in AEPMobileServices(3.x).

## Primary `Classes`

The class name containing public APIs is different depending on which SDK and language combination is being used.

| SDK version | Language | Class name |
| :--- | :--- | :--- |
| ACPMobileServices | Objective-C | ACPMobileServices |
| AEPMobileServices | Swift | AEPMobileServices |
| AEPMobileServices | Objective-C | AEPMobileServices |

## Mobile Services extension APIs

For more information, please read the [Mobile Services API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services/mobileservices-api-reference).

### trackAdobeDeepLink

* ACPMobileServices

  ```objective-c
  + (void) trackAdobeDeepLink: (NSURL*) url;
  ```

* AEPMobileServices

  ```objective-c
  + (void) trackAdobeDeepLink: (NSURL* _Nonnull) deeplink;
  ```

