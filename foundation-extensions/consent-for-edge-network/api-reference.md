# API Reference

## extensionVersion <a id="extensionversion"></a>

Returns the version of the client-side Consent extension.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static String extensionVersion();
```

#### Example

```java
Consent.extensionVersion();
```
{% endtab %}

{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
public static let extensionVersion
```

#### Example

```swift
Consent.extensionVersion
```

### Objective-C

#### Syntax

```swift
public static let extensionVersion
```

#### Example

```text
[AEPMobileEdgeConsent extensionVersion];
```
{% endtab %}
{% endtabs %}

## getConsents <a id="getconsents"></a>

Retrieves the current consent preferences stored in the Consent extension.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void getConsents(final AdobeCallback<Map<String, Object>> callback);
```

* _callback_ - callback invoked with the current consents of the extension. If an `AdobeCallbackWithError` is provided, an `AdobeError`, can be retruned in the eventuality of any error that occured while getting the user consents. The callback may be invoked on a different thread.

#### Example

```java
Consent.getConsents(new AdobeCallback<Map<String, Object>>() {
    @Override
    public void call(Map<String, Object> currentConsents) {
        // handle currentConsents
    }
});
```
{% endtab %}

{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

* _completion_ - Invoked with the current consent preferences or an `AEPError` if an unexpected error occurs or the request timed out. It may be invoked on a different thread.

#### Example

```swift
Consent.getConsents { currentConsents, error in
    // handle currentConsents
}
```

### Objective-C

#### Syntax

```text
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

#### Example

```text
[AEPMobileEdgeConsent getConsents:^(NSDictionary *currentConsents, NSError *error){
    // handle currentConsents
}];
```
{% endtab %}
{% endtabs %}

## registerExtension <a id="registerextension"></a>

Registers the Edge Consent extension with the Mobile Core SDK.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void registerExtension();
```

#### Example

```java
Consent.registerExtension();
```
{% endtab %}

{% tab title="iOS — Swift" %}
### Swift

Use the MobileCore API to register the Edge Consent extension.

#### Syntax

```swift
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```swift
MobileCore.registerExtensions([Consent.self, ...], {
  // processing after registration
})
```

### Objective-C

Use the AEPMobileCore API to register the Edge Consent extension.

#### Syntax

```swift
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```text
[AEPMobileCore registerExtensions:@[AEPMobileEdgeConsent.class, ...] completion:^{
  // processing after registration
}];
```
{% endtab %}
{% endtabs %}

## updateConsents <a id="updateConsents"></a>

Merges the existing consents with the given consents. Duplicate keys will take the value of those passed in the API.

> **Note:** After a user has selected collect consent no \(n\), the SDK will not allow you to set the users collect consent to yes \(y\).

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void update(final Map<String, Object> consents);
```

* _consents_ - A `Map` of consents defined based on [Privacy/Personalization/Marketing Preferences \(Consents\) XDM Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

#### Examples

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

{% tab title="iOS — Swift" %}
### Swift

#### Syntax

```swift
static func update(with consents: [String: Any])
```

* _consents_ - A `[String: Any]` of consents defined based on [Privacy/Personalization/Marketing Preferences \(Consents\) XDM Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

#### Examples

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

#### Syntax

```text
static func update(with consents: [String: Any])
```

#### Examples

```text
// example 1, updating users collect consent to 'yes'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"y"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];

// example 2, updating users collect consent to 'no'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"n"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConse}];
```
{% endtab %}
{% endtabs %}

