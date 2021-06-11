# Get the application context

In Android, you can retrieve the `android.app.Application` instance by using the `MobileCore.getApplication()` API. The returned `android.app.Application` represents the base class, which maintains the global application state. For more information, please read the [Mobile Core API reference](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/ffd74a0a93867c884f4f1179ab9751c00ff8e7eb/using-mobile-extensions/mobile-core/configuration-reference/mobile-core-api-reference.md).

{% tabs %}
{% tab title="Android" %}
## Android

### getApplication

{% hint style="warning" %}
`MobileCore.getApplication` may return `null` if the `android.app.Application` object was destroyed or if `MobileCore.setApplication`was not previously called.
{% endhint %}

### Syntax

```java
public static Application getApplication()
```

### Example

```java
Application app = MobileCore.getApplication();
if (app != null) {
    ...
}
```
{% endtab %}
{% endtabs %}

