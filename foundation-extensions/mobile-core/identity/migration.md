# Migrating to AEPIdentity reference

This document is a reference comparison of AEPIdentity (3.x) APIs against their equivalent APIs in ACPIdentity (2.x) for an iOS mobile application implementation.

## Public Classes

| Type | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| :--- | :--- | :--- | :--- |
| Primary Class | Identity | AEPMobileIdentity | ACPIdentity |
| Class | MobileCore | AEPMobileCore | ACPCore |

## Identity extension APIs

For more information, please read the [Identity API reference](identity-api-reference.md).

### appendToUrl

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}

```swift
static func appendTo(url: URL?, completion: @escaping (URL?, Error?) -> Void)
```

{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}

```objectivec
+ (void) appendToUrl: (NSURL * _Nullable baseUrl) 
					completion: ^(NSURL * _Nullable urlWithVisitorData, NSError * _Nullable error) completion;
```

{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCompletionHandler: (nullable void (^) (NSURL* __nullable urlWithVersionData, NSError* __nullable error)) completionHandler;
```

{% endtab %}
{% endtabs %}

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

### getExperienceCloudId

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static func getExperienceCloudId(completion: @escaping (String?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) getExperienceCloudId: ^(NSString * _Nullable ecid, NSError * _Nullable error) completion;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) getExperienceCloudId: (nonnull void (^) (NSString* __nullable experienceCloudId)) callback;
+ (void) getExperienceCloudIdWithCompletionHandler: (nonnull void (^) (NSString* __nullable experienceCloudId, NSError* __nullable error)) completionHandler;
```
{% endtab %}
{% endtabs %}

### getIdentifiers

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static func getIdentifiers(completion: @escaping ([Identifiable]?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) getIdentifiers: ^(NSArray<id<AEPIdentifiables>> * _Nullable identifiers, NSError * _Nullable error) completion;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) getIdentifiers: (nonnull void (^) (NSArray<ADBMobileVisitorId*>* __nullable visitorIDs)) callback;
+ (void) getIdentifiersWithCompletionHandler: (nonnull void (^) (NSArray<ACPMobileVisitorId*>* __nullable visitorIDs, NSError* __nullable error)) completionHandler;
```
{% endtab %}
{% endtabs %}

### getUrlVariables

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static func getUrlVariables(completion: @escaping (String?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) getUrlVariables: ^(NSString * _Nullable urlVariables, NSError * _Nullable error) completion:
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) getUrlVariables: (nonnull void (^) (NSString* __nullable urlVariables)) callback;
+ (void) getUrlVariablesWithCompletionHandler: (nonnull void (^) (NSString* __nullable urlVariables, NSError* __nullable error)) completionHandler;
```
{% endtab %}
{% endtabs %}

### setAdvertisingIdentifier

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
public static func setAdvertisingIdentifier(_ identifier: String?)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) setAdvertisingIdentifier: (NSString * _Nullable identifier);
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) setAdvertisingIdentifier: (nullable NSString*) adId;
```
{% endtab %}
{% endtabs %}

### setPushIdentifier

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) setPushIdentifier: (NSString * _Nullable deviceToken);
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```
{% endtab %}
{% endtabs %}

### syncIdentifier

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static func syncIdentifier(identifierType: String, identifier: String, authenticationState: MobileVisitorAuthenticationState)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) syncIdentifierWithType: (NSString * _Nonnull identifierType) 
										 identifier: (NSString * _Nonnull identifier) 
								 authentication: (enum AEPAuthenticationState authenticationState);
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) syncIdentifier: (nonnull NSString*) identifierType             
             identifier: (nonnull NSString*) identifier
         authentication: (ADBMobileVisitorAuthenticationState) authenticationState;
```
{% endtab %}
{% endtabs %}

### syncIdentifiers

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}

```swift
static func syncIdentifiers(identifiers: [String: String]?)
static func syncIdentifiers(identifiers: [String: String]?, authenticationState: MobileVisitorAuthenticationState)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```objectivec
+ (void) syncIdentifiers: (NSDictionary<NSString *, NSString *> * _Nullable identifiers);
+ (void) syncIdentifiers: (NSDictionary<NSString *, NSString *> * _Nullable identifiers) 
					authentication: (enum AEPAuthenticationState authenticationState);
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```objectivec
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers;
+ (void) syncIdentifiers: (nullable NSDictionary*) identifiers authentication: (ACPMobileVisitorAuthenticationState) authenticationState;
```
{% endtab %}
{% endtabs %}
