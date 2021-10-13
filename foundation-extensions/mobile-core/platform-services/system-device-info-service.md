## SystemInfo Service (iOS) & DeviceInfo Service (Android)

## Overview

The `SystemInfo Service` (iOS) / `DeviceInfo Service` (Android) provides a set of APIs for retrieving device information, such as carrier name, device name, locale, and more. 

## Usage

The following code snippet shows how to retrieve the active locale.

{% tabs %}
{% tab title="Android" %}

```java
import com.adobe.marketing.mobile.services.*;

DeviceInforming deviceInfoService = ServiceProvider.getInstance().getDeviceInfoService();
String localName = deviceInfoService.getLocaleString();
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
import AEPServices

// Add a computed variable to your type or use it directly in the function where required
private var systemInfoService: SystemInfoService {
  return ServiceProvider.shared.systemInfoService
}

// ...
let locale = systemInfoService.getActiveLocaleName()
```

{% endtab %}
{% endtabs %}
