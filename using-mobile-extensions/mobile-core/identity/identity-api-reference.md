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

