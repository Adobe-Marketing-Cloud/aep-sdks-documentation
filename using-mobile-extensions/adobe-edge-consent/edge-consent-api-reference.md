# Consent Collection API reference

## extensionVersion <a id="extensionversion"></a>

Returns the version of the client-side Edge Consent extension.

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

{% tab title="iOS" %}
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

```objective-c
[AEPMobileEdgeConsent extensionVersion];
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

{% tab title="iOS" %}

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

```objective-c
[AEPMobileCore registerExtensions:@[AEPMobileEdgeConsent.class, ...] completion:^{
  // processing after registration
}];
```

{% endtab %}
{% endtabs %}

## getConsents<a id="getconsents"></a>

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

{% tab title="iOS" %}
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

```objective-c
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

#### Example

```objective-c
[AEPMobileEdgeConsent getConsents:^(NSDictionary *currentConsents, NSError *error){
	// handle currentConsents
}];
```
{% endtab %}
{% endtabs %}

## updateConsents<a id="updateConsents"></a>

Merges the existing consents with the given consents. Duplicate keys will take the value of those passed in the API.

> After a user has selected collect consent no (n), the SDK will not allow you to set the users collect consent to yes (y).

{% tabs %}
{% tab title="Android" %}

### Java

#### Syntax

```java
public static void update(final Map<String, Object> xdmFormattedConsents);
```

* *xdmFormattedConsents* - A `Map` of consents in predefined [Profile Consents XDM schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

#### Examples

```java
// example 1, updating users collect consent to 'yes'
final Map<String, Object> consents = new HashMap<String, Object>() {
	{
		put("consents", new HashMap<String, Object>() {
			{
				put("collect", new HashMap<String, String>() {
					{
						put("val", "y");
					}
				});
			}
		});
	}
};

Consent.update(consents);

// example 2, updating users collect consent to 'no'
final Map<String, Object> consents = new HashMap<String, Object>() {
	{
		put("consents", new HashMap<String, Object>() {
			{
				put("collect", new HashMap<String, String>() {
					{
						put("val", "n");
					}
				});
			}
		});
	}
};

Consent.update(consents);
```

{% endtab %}

{% tab title="iOS" %}

### Swift

#### Syntax

```swift
static func update(with consents: [String: Any])
```

* *consents* - A `[String: Any]` of consents in predefined [Profile Consents XDM schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md).

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

```objective-c
static func update(with consents: [String: Any])
```

#### Examples

```objective-c
// example 1, updating users collect consent to 'yes'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"y"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];

// example 2, updating users collect consent to 'no'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"n"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];
```

{% endtab %}
{% endtabs %}