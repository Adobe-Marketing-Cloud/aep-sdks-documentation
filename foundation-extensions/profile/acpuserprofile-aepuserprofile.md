# Migrating to AEPUserProfile

This document is a reference comparison of ACPUserProfile (2.x) APIs against their equivalent APIs in AEPUserProfile (3.x).

## Primary `Classes`

| Type | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| :--- | :--- | :--- | :--- |
| Primary Class | UserProfile | AEPMobileUserProfile | ACPUserProfile |

## UserProfile extension APIs

For more information, please read the [Profile API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references).

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

### updateUserAttributes

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
public static func updateUserAttributes(attributeDict: [String: Any])
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
+ (void)updateUserAttributesWithAttributeDict:(NSDictionary<NSString *, id> * _Nonnull)attributeDict;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
+ (void) updateUserAttribute: (nonnull NSString*) attributeName withValue: (nullable NSString*) attributeValue;
```
{% endtab %}
{% endtabs %}

### removeUserAttribute

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
public static void removeUserAttribute(String attributeName)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
+ (void)removeUserAttributesWithAttributeNames:(NSArray<NSString *> * _Nonnull)attributeNames;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
+ (void) removeUserAttribute: (nonnull NSString*) key
```
{% endtab %}
{% endtabs %}

### getUserAttributes

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
+ (void)getUserAttributesWithAttributeNames:(NSArray<NSString *> * _Nonnull)attributeNames completion:(void (^ _Nonnull)(NSDictionary<NSString *, id> * _Nullable, enum AEPError))completion;
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
+ (void) getUserAttributes: (nullable NSArray <NSString*>*) attributNames withCompletionHandler: (nonnull void (^) (NSDictionary* __nullable userAttributes, NSError* _Nullable error)) completionHandler
```
{% endtab %}
{% endtabs %}

