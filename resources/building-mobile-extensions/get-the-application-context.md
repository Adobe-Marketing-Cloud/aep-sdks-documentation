# Get the Application Context

In Android, you can retrieve the `android.app.Application` instance using the `MobileCore.getApplication()` API. The returned `android.app.Application` represents the base class which maintains the global application state. For more information, see [Moble Core API Reference](../../using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md)

{% tabs %}
{% tab title="Android" %}

### Android

### getApplication

{% hint style="warning" %}

`MobileCore.getApplication` might return `null` if the `android.app.Application` object was destroyed or if `MobileCore.setApplication`was not previously called.

{% endhint %}

#### Syntax

```java
public static Application getApplication()
```

#### Example

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```

{% endtab %}

{% endtabs %}

