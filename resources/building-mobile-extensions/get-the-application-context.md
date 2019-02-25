# Get the Application Context

In Android, you can retrieve the `android.app.Application` instance using the `MobileCore.getApplication()` API. The returned Application represents the base class which maintains the global application state.

{% tabs %}
{% tab title="Android" %}

### Android

### getApplication

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

