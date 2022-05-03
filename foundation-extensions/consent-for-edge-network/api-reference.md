# API Reference

## extensionVersion

The extensionVersion() API returns the version of the client-side Consent extension.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
String extensionVersion = Consent.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static var extensionVersion: String
```

**Example**

```swift
let extensionVersion = Consent.extensionVersion
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
NSString *extensionVersion = [AEPMobileEdgeConsent extensionVersion];
```
{% endtab %}
{% endtabs %}

## getConsents

Retrieves the current consent preferences stored in the Consent extension.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void getConsents(final AdobeCallback<Map<String, Object>> callback);
```

* _callback_ - callback invoked with the current consents of the extension. If an `AdobeCallbackWithError` is provided, an `AdobeError`, can be returned in the eventuality of any error that occurred while getting the user consents. The callback may be invoked on a different thread.

**Example**

```java
Consent.getConsents(new AdobeCallback<Map<String, Object>>() {
    @Override
    public void call(Map<String, Object> currentConsents) {
        // handle currentConsents
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

**Syntax**

```swift
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

* _completion_ - Invoked with the current consent preferences or an `AEPError` if an unexpected error occurs or the request timed out. It may be invoked on a different thread.

**Example**

```swift
Consent.getConsents { currentConsents, error in
    // handle currentConsents
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) getConsents:^ (NSDictionary<NSString *,id> * _Nullable, NSError * _Nullable)
```

**Example**

```objectivec
[AEPMobileEdgeConsent getConsents:^(NSDictionary *currentConsents, NSError *error){
    // handle currentConsents
}];
```
{% endtab %}
{% endtabs %}

## registerExtension

Registers the Edge Consent extension with the Mobile Core SDK.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void registerExtension();
```

**Example**

```java
Consent.registerExtension();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

Use the MobileCore API to register the Edge Consent extension.

**Syntax**

```swift
static func registerExtensions(_ extensions: [NSObject.Type], 
                               _ completion: (() -> Void)? = nil)
```

**Example**

```swift
import AEPEdgeConsent

...
MobileCore.registerExtensions([Consent.self])
```

### Objective-C

Use the AEPMobileCore API to register the Edge Consent extension.

**Syntax**

```objectivec
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                  completion: (void (^ _Nullable)(void)) completion;
```

**Example**

```objectivec
@import AEPEdgeConsent;

...
[AEPMobileCore registerExtensions:@[AEPMobileEdgeConsent.class] completion:nil];
```
{% endtab %}
{% endtabs %}

## updateConsents <a id="updateConsents"></a>

Merges the existing consents with the given consents. Duplicate keys will take the value of those passed in the API.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static void update(final Map<String, Object> consents);
```

* _consents_ - A `Map` of consents defined based on [Privacy/Personalization/Marketing Preferences \(Consents\) XDM Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

**Example**

```java
// example 1, updating users collect consent to 'yes'
final Map<String, Object> collectConsents = new HashMap<>();
collectConsents.put("collect", new HashMap<String, String>() {
    {
        put("val", "y");
    }
});

final Map<String, Object> consents = new HashMap<>();
consents.put("consents", collectConsents);

Consent.update(consents);

// example 2, updating users collect consent to 'no'
final Map<String, Object> collectConsents = new HashMap<>();
collectConsents.put("collect", new HashMap<String, String>() {
    {
        put("val", "n");
    }
});

final Map<String, Object> consents = new HashMap<>();
consents.put("consents", collectConsents);

Consent.update(consents);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

**Syntax**

```swift
static func update(with consents: [String: Any])
```

* _consents_ - A `[String: Any]` of consents defined based on [Privacy/Personalization/Marketing Preferences \(Consents\) XDM Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

**Example**

```swift
// example 1, updating users collect consent to 'yes'
let collectConsent = ["collect": ["val": "y"]]
let currentConsents = ["consents": collectConsent]
Consent.update(with: currentConsents)

// example 2, updating users collect consent to 'no'
let collectConsent = ["collect": ["val": "n"]]
let currentConsents = ["consents": collectConsent]
Consent.update(with: currentConsents)
```

### Objective-C

**Syntax**

```objectivec
+ (void) updateWithConsents:(NSDictionary<NSString *,id> * _Nonnull)
```

**Example**

```text
// example 1, updating users collect consent to 'yes'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"y"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];

// example 2, updating users collect consent to 'no'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"n"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];
```
{% endtab %}
{% endtabs %}

