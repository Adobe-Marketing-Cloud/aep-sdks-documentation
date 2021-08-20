# Migrating to AEPMobileServices reference

This document is a reference comparison of ACPMobileServices(1.x) APIs against their equivalent APIs in AEPMobileServices(3.x).

## Primary `Classes`

| Type | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| :--- | :--- | :--- | :--- |
| Primary Class | AEPMobileServices | AEPMobileServices | ACPMobileServices |

## Mobile Services extension APIs

For more information, please read the [Mobile Services API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services/mobileservices-api-reference).

### trackAdobeDeepLink

{% tabs %}
{% tab title="AEP 3.x (Objective-C)" %}
```objc
  + (void) trackAdobeDeepLink: (NSURL* _Nonnull) deeplink;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objc
  + (void) trackAdobeDeepLink: (NSURL*) url;
```
{% endtab %}
{% endtabs %}

