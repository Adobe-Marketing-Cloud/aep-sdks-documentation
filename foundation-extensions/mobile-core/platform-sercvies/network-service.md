# Network Service

## Overview

The `Network Service` provides shared functionality to make asynchronous network requests and handle their responses.

## Usage

The following code snippet details how to make a simple network request and handle the response.

{% tabs %}
{% tab title="Android" %}

```java
AndroidNetworkService androidNetworkService = new AndroidNetworkService(ServiceProvider.getInstance().getNetworkService());
androidNetworkService.connectUrlAsync(url,
											  POST, payload,
		null, 10000, 10000, new NetworkService.Callback() {
			@Override
			public void call(NetworkService.HttpConnection connection) {
				// handle `httpConnection`
			}
});
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
// Create your `NetworkRequest`, for more details see `NetworkRequest.swift`
let networkRequest = NetworkRequest(url: url, httpMethod: .get, httpHeaders: headers)

// Get an instance of the current network service
let networkService = ServiceProvider.shared.networkService

// Make a request
networkService.connectAsync(networkRequest: networkRequest) { httpConnection in
  // handle `httpConnection`
}
```

{% endtab %}
{% endtabs %}
