# Identity API Reference

## getExperienceCloudId

{% tabs %}
{% tab title="Android" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the [AdobeCallback](../mobile-core/mobile-core-api-reference.md#public-classes).

When [AdobeCallbackWithError](../mobile-core/mobile-core-api-reference.md#public-classes) is provided, and you are fetching the ECID from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core/mobile-core-api-reference.md#public-classes).

**Java**

**Syntax**

```java
public static void getExperienceCloudId(final AdobeCallback<String> callback);
```

* _callback_ is invoked after the ECID is available. The callback may be invoked on a different thread.

**Example**

```java
Identity.getExperienceCloudId(new AdobeCallback<String>() {    
    @Override    
    public void call(String id) {        
         //Handle the ID returned here    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getExperienceCloudId

This API retrieves the ECID that was generated when the app was initially launched.

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. The values are returned via the callback.

**Syntax**

```swift
@objc(getExperienceCloudId:)
static func getExperienceCloudId(completion: @escaping (String?, Error?) -> Void)
```

* _completion_ is invoked after the ECID is available.  The default timeout is 1000ms.

**Examples**

**Objective-C**

```objectivec
[AEPEdgeIdentity getExperienceCloudId:^(NSString * _Nullable ecid, NSError * error) {   
    // handle the retrieved ID here    
}];
```

**Swift**

```swift
Identity.getExperienceCloudId { (ecid, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved ID here
  }
}
```
{% endtab %}
{% endtabs %}

## getIdentities
{% tabs %}
{% tab title="Android" %}
### getIdentities

Get all identities in the Identity for Edge Network extension, including customer identifiers which were previously added.

When [AdobeCallbackWithError](../mobile-core/mobile-core-api-reference.md#public-classes) is provided, and you are fetching the identities from the Mobile SDK, the timeout value is 500ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate [AdobeError](../mobile-core/mobile-core-api-reference.md#public-classes).

**Java**

**Syntax**

```java
public static void getIdentities(final AdobeCallback<IdentityMap> callback);
```

* _call_ is invoked after the identities are available. The return format is an instance of [IdentityMap](#identitymap). The callback may be invoked on a different thread.

**Example**

```java
Identity.getIdentities(new AdobeCallback<IdentityMap>() {    
    @Override    
    public void call(IdentityMap identityMap) {        
         //Handle the IdentityMap returned here    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getIdentities

Get all identities in the Identity for Egde Network extension, including customer identifiers which were previously added.

**Syntax**

```swift
@objc(getIdentities:)
static func getIdentities(completion: @escaping (IdentityMap?, Error?) -> Void)
```

* _completion_ is invoked after the identities are available.  The default timeout is 1000ms. The return format is an instance of [IdentityMap](#identitymap)

**Examples**

**Objective-C**

```objectivec
[AEPEdgeIdentity getIdentities:^(AEPIdentityMap *map, NSError * error) {   
    // handle the retrieved identities here    
}];
```

**Swift**

```swift
Identity.getIdentities { (identityMap, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the retrieved identitites here
  }
}
```
{% endtab %}
{% endtabs %}

## updateIdentities
{% tabs %}
{% tab title="Android" %}
### updateIdentities

Update the currently known identities within the SDK. The Identity extension will merge the received identifiers with the previously saved ones in an additive manner, no identities are removed from this API.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Updating identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

- ECID
- IDFA
- GAID


**Java**

**Syntax**

```java
public static void updateIdentities(final IdentityMap identityMap);
```

**Example**

```java
IdentityItem item = new IdentityItem("user@example.com");
IdentityMap identityMap = new IdentityMap();
identityMap.addItem(item, "Email")
Identity.updateIdentities(identityMap);
```
{% endtab %}

{% tab title="iOS" %}
### updateIdentities

Update the currently known identities within the SDK. The Identity extension will merge the received identifiers with the previously saved ones in an additive manner, no identities are removed from this API.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Updating identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

- ECID
- IDFA
- GAID

**Syntax**

```swift
@objc(updateIdentities:)
static func updateIdentities(with map: IdentityMap)
```

**Examples**

**Objective-C**

```objectivec
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
AEPIdentityMap *map = [[AEPIdentityMap alloc] init];
[map addItem:item withNamespace:@"Email"];
[AEPMobileEdgeIdentity updateIdentities:map];
```

**Swift**

```swift
let identityMap = IdentityMap()
map.addItem(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")
Identity.updateIdentities(with: identityMap)
```
{% endtab %}
{% endtabs %}

## removeIdentity
{% tabs %}
{% tab title="Android" %}
### removeIdentity

Remove the identity from the stored client-side [IdentityMap](#identitymap). The Identity extension will stop sending the identifier to the Edge Network. Using this API does not remove the identifier from the server-side User Profile Graph or Identity Graph.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Removing identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

- ECID
- IDFA
- GAID


**Java**

**Syntax**

```java
public static void removeIdentity(final IdentityItem item, final String namespace);
```

**Example**

```java
IdentityItem item = new IdentityItem("user@example.com");
Identity.removeIdentity(item, "Email");
```
{% endtab %}

{% tab title="iOS" %}
### removeIdentity

Remove the identity from the stored client-side [IdentityMap](#identitymap). The Identity extension will stop sending the identifier to the Edge Network. Using this API does not remove the identifier from the server-side User Profile Graph or Identity Graph.

Identities with an empty _id_ or _namespace_ are not allowed and are ignored.

Removing identities using a reserved namespace is not allowed using this API. The reserved namespaces are:

- ECID
- IDFA
- GAID

**Syntax**

```swift
@objc(removeIdentityItem:withNamespace:)
static func removeIdentity(item: IdentityItem, withNamespace: String)
```

**Examples**

**Objective-C**

```objectivec
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[AEPMobileEdgeIdentity removeIdentityItem:item withNamespace:@"Email"];
```

**Swift**

```swift
Identity.removeIdentity(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")
```
{% endtab %}
{% endtabs %}

## resetIdentities

Clears all identities stored in the Identity extension and generates a new Experience Cloud ID (ECID) .  Using this API does not remove the identifiers from the server-side User Profile Graph or Identity Graph.

{% hint style="warning" %}
The Identity for Edge Network extension does not read the Mobile SDK's privacy status and therefor setting the SDK's privacy status to opt-out will not clear the identities from the Identity for Edge Network extension.
{% endhint %}

See [MobileCore.resetIdentities](../mobile-core/mobile-core-api-reference#resetidentities) for more details.

## Public Classes
### IdentityMap
Defines a map containing a set of end user identities, keyed on either namespace integration code or the namespace ID of the identity. The values of the map are an array, meaning that more than one identity of each namespace may be carried.

The format of the IdentityMap class is defined by the [XDM Identity Map Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/identitymap.schema.md).

For more information, please read an overview of the [AEP Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html).

```text
"identityMap" : {
    "Email" : [
      {
        "id" : "user@example.com",
        "authenticatedState" : "authenticated",
        "primary" : false
      }
    ],
    "Phone" : [
      {
        "id" : "1234567890",
        "authenticatedState" : "ambiguous",
        "primary" : false
      },
      {
        "id" : "5557891234",
        "authenticatedState" : "ambiguous",
        "primary" : false
      }
    ],
    "ECID" : [
      {
        "id" : "44809014977647551167356491107014304096",
        "authenticatedState" : "ambiguous",
        "primary" : true
      }
    ]
  }
```

{% tabs %}
{% tab title="Android" %}

**Examples**

**Java**
```java
// Construct
IdentityMap identityMap = new IdentityMap();

// Add an item
IdentityItem item = new IdentityItem("user@example.com");
identityMap.addItem(item, "Email");

// Remove an item
IdentityItem item = new IdentityItem("user@example.com");
identityMap.removeItem(item, "Email");

// Get a list of items for a given namespace
List<IdentityItem> items = identityMap.getIdentityItemsForNamespace("Email");

// Get a list of all namespaces used in current IdentityMap
List<String> namespaces = identityMap.getNamespaces();

// Check if IdentityMap has no identities
boolean hasNotIdentities = identityMap.isEmpty();
```

{% endtab %}

{% tab title="iOS" %}

**Examples**

**Objective-C**
```objectivec
// Initialize
AEPIdentityMap *identityMap = [[AEPIdentityMap alloc] init];

// Add an item
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[identityMap addItem:item withNamespace:@"Email"];

// Remove an item
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"user@example.com" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];
[identityMap removeItem:item withNamespace:@"Email"];

// Get a list of items for a given namespace
NSArray* items = [identityMap getItemsWithNamespace:@"Email"];

// Get a list of all namespaces used in current IdentityMap
NSArray* namespaces = identityMap.namespaces;

// Check if IdentityMap has no identities
bool hasNoIdentities = identityMap.isEmpty;
```

**Swift**
```swift
// Initialize
let identityMap: IdentityMap = IdentityMap()

// Add an item
identityMap.add(item: IdentityItem(id: "user@example.com"), withNamespace: "Email")

// Remove an item
identityMap.remove(item: IdentityItem(id: "user@example.com", withNamespace: "Email"))

// Get a list of items for a given namespace
let items: [IdentityItem] = identityMap.getItems(withNamespace: "Email")

// Get a list of all namespaces used in current IdentityMap
let namespaces: [String] = identityMap.namespaces

// Check if IdentityMap has no identities
let hasNoIdentities: Bool = identityMap.isEmpty
```

{% endtab %}
{% endtabs %}
### IdentityItem
Defines an identity to be included in an [IdentityMap](#identitymap).

The format of the IdentityItem class is defined by the [XDM Identity Item Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/identityitem.schema.md).

{% tabs %}
{% tab title="Android" %}

**Examples**

**Java**
```java
// Construct
IdentityItem item = new IdentityItem("identifier");

IdentityItem item = new IdentityItem("identifier", AuthenticatedState.AUTHENTICATED, false);


// Getters
String id = item.getId();

AuthenticatedState state = item.getAuthenticatedState();

boolean primary = item.isPrimary();
```

{% endtab %}

{% tab title="iOS" %}

**Examples**

**Objective-C**
```objectivec
// Initialize
AEPIdentityItem *item = [[AEPIdentityItem alloc] initWithId:@"identity" authenticatedState:AEPAuthenticatedStateAuthenticated primary:false];

// Getters
NSString *id = primaryEmail.id;

long state = primaryEmail.authenticatedState;

bool primary = primaryEmail.primary;
```

**Swift**
```swift
// Initialize
let item = IdentityItem(id: "identifier")

let item = IdentityItem(id: "identifier", authenticatedState: .authenticated, primary: false)

// Getters
let id: String = item.id

let state: AuthenticatedState = item.authenticatedState

let primary: Bool = item.primary
```

{% endtab %}
{% endtabs %}

### AuthenticatedState
Defines the state an [Identity Item](#identityitem) is authenticated for.

The possible authenticated states are:
- Ambiguous - the state is ambiguous or not defined
- Authenticated - the user is identified by a login or similar action
- LoggedOut - the user was identified by a login action at a previous time, but is not logged in now

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public enum AuthenticatedState {
	AMBIGUOUS("ambiguous"),
	AUTHENTICATED("authenticated"),
	LOGGED_OUT("loggedOut");
}
```

{% endtab %}

{% tab title="iOS" %}

**Syntax**

```swift
@objc(AEPAuthenticatedState)
public enum AuthenticatedState: Int, RawRepresentable, Codable {
    case ambiguous = 0
    case authenticated = 1
    case loggedOut = 2
}
```

{% endtab %}
{% endtabs %}

