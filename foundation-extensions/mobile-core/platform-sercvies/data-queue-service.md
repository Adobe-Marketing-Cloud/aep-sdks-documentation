# DataQueue Service

## Overview

The `DataQueue Service` provides access to thread-safe FIFO queues. This service is particularly useful when used in conjunction with a `PersistentHitQueue`.

## Usage

The following code snippet shows how to create a `DataQueue` and add a `DataEntity` to the queue.

{% tabs %}
{% tab title="Android" %}

```java
import com.adobe.marketing.mobile.services.*;

DataQueue dataQueue = ServiceProvider.getInstance().getDataQueueService().getDataQueue(name);
DataEntity dataEntity = new DataEntity(mydata);
dataQueue.add(dataEntity);
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
import AEPServices

// Create a `DataQueue`
guard let dataQueue = ServiceProvider.shared.dataQueueService.getDataQueue(label: name) else {
  Log.error(label: "\(name):\(#function)", "Failed to create Data Queue")
  return
}

// Create a `DataEntity`
let entity = DataEntity(data: myData)

// Add entity to `dataQueue`
dataQueue.add(entity)
```

{% endtab %}
{% endtabs %}
