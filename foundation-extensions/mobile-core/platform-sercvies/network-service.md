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

## Public Interfaces

{% tabs %}
{% tab title="Android" %}

- **Networking**

```java
public interface Networking {
	/**
	 * Initiates an asynchronous network connection
	 * @param request {@link NetworkRequest} used for connection
	 * @param callback {@link NetworkCallback} that will receive the {@link HttpConnecting} instance after the connection has been made
	 */
	void connectAsync(final NetworkRequest request, final NetworkCallback callback);
}
```

- **NetworkRequest**

​       NetworkRequest class contains the data needed to initiate a network request. 

```java
public class NetworkRequest {
	private final String url;
	private final HttpMethod method;
	private final byte[] body;
	private final Map<String, String> headers;
	private final int connectTimeout;
	private final int readTimeout;

	/**
	 * Constructor for NetworkRequest
	 * @param url {@link String} containing the full url for connection
	 * @param method {@link com.adobe.marketing.mobile.services.HttpMethod}, for example "POST", "GET" etc.
	 * @param body {@code byte[]} array specifying payload to send to the server
	 * @param headers {@code Map<String, String>} containing any additional key value pairs to be used while requesting a
	 *                        connection to the url depending on the {@code method} used
	 * @param connectTimeout {@code int} indicating connect timeout value in seconds
	 * @param readTimeout {@code int} indicating the timeout, in seconds, that will be used to wait for a read to finish after a successful connect
	 */
	public NetworkRequest(final String url,
						  final HttpMethod method,
						  final byte[] body,
						  final Map<String, String> headers,
						  final int connectTimeout,
						  final int readTimeout) {
		// ...
	}

	public String getUrl() {
		return url;
	}

	public HttpMethod getMethod() {
		return method;
	}

	public byte[] getBody() {
		return body;
	}

	public Map<String, String> getHeaders() {
		return headers;
	}

	public int getConnectTimeout() {
		return connectTimeout;
	}

	public int getReadTimeout() {
		return readTimeout;
	}
}
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

- **Networking**

```swift
public protocol Networking {
    /// Initiates an asynchronous network connection to the specified NetworkRequest.url. This API uses `URLRequest.CachePolicy.reloadIgnoringLocalCache`.
    /// - Parameters:
    ///   - networkRequest: the `NetworkRequest` used for this connection
    ///   - completionHandler:Optional completion handler which is called once the `HttpConnection` is available; it can be called from an `HttpConnectionPerformer` if `NetworkServiceOverrider` is enabled.
    ///   In case of a network error, timeout or an unexpected error, the `HttpConnection` is nil
    func connectAsync(networkRequest: NetworkRequest, completionHandler: ((HttpConnection) -> Void)?)
}
```
- **NetworkRequest**

​        NetworkRequest struct to be used by the NetworkService and the HttpConnectionPerformer when initiating network calls.

```swift
public class NetworkRequest: NSObject {

    private static let REQUEST_HEADER_KEY_USER_AGENT = "User-Agent"

    public let url: URL
    public let httpMethod: HttpMethod
    public let connectPayload: Data
    public let httpHeaders: [String: String]
    public let connectTimeout: TimeInterval
    public let readTimeout: TimeInterval

    /// Initialize the `NetworkRequest`
    /// - Parameters:
    ///   - url: URL used to initiate the network connection, should use https scheme
    ///   - httpMethod: `HttpMethod` to be used for this network request; the default value is GET
    ///   - connectPayload: the body of the network request as a String; this parameter is ignored for GET requests
    ///   - httpHeaders: optional HTTP headers for the request
    ///   - connectTimeout: optional connect timeout value in seconds; default is 5 seconds
    ///   - readTimeout: optional read timeout value in seconds, used to wait for a read to finish after a successful connect, default is 5 seconds
    /// - Returns: an initialized `NetworkRequest` object
    public convenience init(url: URL, httpMethod: HttpMethod = HttpMethod.get, connectPayload: String = "", httpHeaders: [String: String] = [:], connectTimeout: TimeInterval = 5, readTimeout: TimeInterval = 5) {
      // ....
    }

    /// Initialize the `NetworkRequest`
    /// - Parameters:
    ///   - url: URL used to initiate the network connection, should use https scheme
    ///   - connectPayloadData: the body of the network request as a Data
    ///   - httpHeaders: optional HTTP headers for the request
    ///   - connectTimeout: optional connect timeout value in seconds; default is 5 seconds
    ///   - readTimeout: optional read timeout value in seconds, used to wait for a read to finish after a successful connect, default is 5 seconds
    /// - Returns: an initialized `NetworkRequest` object
    public init(url: URL, httpMethod: HttpMethod = HttpMethod.get, connectPayloadData: Data, httpHeaders: [String: String] = [:], connectTimeout: TimeInterval = 5, readTimeout: TimeInterval = 5) {
        // ....
    }
}
```
- **HttpConnection**

​        The HttpConnection represents the response to NetworkRequest, to be used for network completion handlers and when overriding the network stack in place of internal network connection implementation.

```swift
public struct HttpConnection {
    /// Returns application server response data from the connection or nil if there was an error
    public let data: Data?

    /// Response metadata provided by the server
    public let response: HTTPURLResponse?

    /// The error associated with the request failure or nil on success
    public let error: Error?

    /// Initialize an HttpConnection structure
    ///
    /// - Parameters:
    ///   - data: optional data returned from the server in the connection
    ///   - response: the response from the server
    ///   - error: an optional error if something failed
    public init(data: Data?, response: HTTPURLResponse?, error: Error?) {
        // ...
    }
}

public extension HttpConnection {
    /// Returns application server response data from the connection as string, if available.
    var responseString: String? {
        // ...
    }

    /// Returns the connection response code for the connection request.
    var responseCode: Int? {
        // ...
    }

    /// Returns application server response message as string extracted from the `response` property, if available.
    var responseMessage: String? {
        // ...
    }

    /// Returns a value for the response header key from the `response` property, if available.
    /// This is protocol specific. For example, HTTP URLs could have headers like "last-modified", or "ETag" set.
    /// - Parameter forKey: the header key name sent in response when requesting a connection to the URL.
    func responseHttpHeader(forKey: String) -> String? {
        // ...
    }
}
```

{% endtab %}
{% endtabs %}