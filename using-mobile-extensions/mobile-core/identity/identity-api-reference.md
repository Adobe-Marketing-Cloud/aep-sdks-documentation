# Identity API Reference

## Synch Identifiers

Updates the specified customer ID with the Adobe Experience Cloud ID service.

This API synchronizes the provided customer identifier type key and value with the given [authentication state](https://docs.adobelaunch.com/extension-reference/mobile/identity/identity-methods-in-android#authenticationstate) to the Adobe Experience Cloud ID Service. If the specified customer ID type exists in the service, this ID type is updated with the new ID and authentication state. Otherwise, a new customer ID is added. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

{% tabs %}
{% tab title="Android" %}
### syncidentifier

**Syntax**

```text
public static void syncIdentifier(final String identifierType,
                                      final String identifier,
                                      final VisitorID.AuthenticationState authenticationState);

```

**Example**

```java
Identity.syncIdentifier("idType", "idValue", VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchidentifiers

**Tip**: The `identifiers` map contains IDs with the Identifier type as the key, and the string identifier as the value.

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers,
                                       final VisitorID.AuthenticationState authenticationState)
```

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers, VisitorID.AuthenticationState.AUTHENTICATED);
```

### synchidentifiers \(overloaded\)

**Tip**: All given customer IDs are given the default authentication state of `UNKNOWN`.

These IDs are preserved between app upgrades, are saved and restored during the standard application backup process, and are removed at uninstall. If the current SDK privacy status is `optedout`, calling this method results in no operations being performed.

**Tip**: The `identifiers` dictionary contains IDs with the Identifier type as the key, and the string identifier as the value.

**Syntax**

```java
public static void syncIdentifiers(final Map<String, String> identifiers);
```

**Example**

```java
Map<String, String> identifiers = new HashMap<String, String>();
identifiers.put("idType", "idValue");
Identity.syncIdentifier(identifiers);
```
{% endtab %}

{% tab title="iOS" %}
### synchidentifier
{% endtab %}
{% endtabs %}

## Append Visitor Data to a URL

{% tabs %}
{% tab title="Android" %}
## appendVisitorInfoForURL {#appendvisitorinfoforurl}

Appends Adobe visitor data to a URL string. If the provided URL is null or empty, it is returned as is. Otherwise, the following information is added to the url string that is returned in the [AdobeCallback](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/identity/identity-methods-in-android#adobecallback) instance:

* The `adobe_mc` attribute is an URL encoded list containing:
  * Experience Cloud ID \(ECID\)
  * Experience Cloud Org ID
  * A timestamp taken when this request was made
* The optional adobe\_aa\_vid attribute is the URL encoded Analytics Custom Visitor ID, if available

### **Syntax** {#syntax-3}

```java
public static void appendVisitorInfoForURL(final String baseURL, final AdobeCallback<String> callback);
```

### **Example** {#example-3}

```java
Identity.appendVisitorInfoForURL("http://myurl.com", new AdobeCallback<String>() {    @Override    public void call(String urlWithAdobeVisitorInfo) {        //handle the new URL here        //For example, open the URL on the device browser        //        Intent i = new Intent(Intent.ACTION_VIEW);        i.setData(Uri.parse(urlWithAdobeVisitorInfo));        startActivity(i);    }});
```

##   {#getidentifiers}
{% endtab %}

{% tab title="iOS" %}
## appendToURL {#appendtourl}

Appends Adobe visitor data to a URL.

If the provided URL is nil or empty, it is returned as is. Otherwise, the following information is added to the url string that is returned via the callback:

* The adobe\_mc attribute is an URL encoded list containing:
  * Experience Cloud ID \(ECID\)
  * Experience Cloud Org ID
  * A timestamp taken when this request was made
* The optional `adobe_aa_vid` attribute is the URL-encoded Analytics Custom Visitor ID, if available.

### **Syntax** {#syntax-3}

```objectivec
+ (void) appendToUrl: (nullable NSURL*) baseUrl withCallback: (nullable void (^) (NSURL* __nullable urlWithVisitorData)) callback;
```

### **Examples** {#examples-3}

#### Objective-C {#objective-c-3}

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"www.myUrl.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here}
];
```

#### Swift {#swift-3}

```swift
ACPIdentity.append(to:URL(string: "www.myUrl.com"), withCallback: {(appendedURL) in    
    // handle the appended url here

});
```
{% endtab %}
{% endtabs %}

