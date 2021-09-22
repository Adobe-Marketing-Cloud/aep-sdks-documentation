# Platform Services

The Platform Services are provided by the Adobe Experience Platform Mobile SDKs as part of the Mobile Core extension. These services provide shared functionality throughout the SDK that can be shared by extensions. For example, services provide shared functionality for networking, data queuing, caching, and more.

{% hint style="info" %}
This feature is only available in [Android Core 1.8.0](https://aep-sdks.gitbook.io/docs/release-notes#android-core-1-8-0) or later and [iOS Core 3.0.0](https://aep-sdks.gitbook.io/docs/release-notes#adobe-experience-platform-ios-core-sdks) or later.
{% endhint %}

## Accessing Services

The MobileCore extension provides a shared `ServiceProvider`, responsible for accessing the current set of provided services.

The following code snippet shows how to import `ServiceProvider` in your souce code.

{% tabs %}
{% tab title="Android" %}

```java
import com.adobe.marketing.mobile.services.ServiceProvider;

// Get the instance of the ServiceProvider
ServiceProvider serviceProvider = ServiceProvider.getInstance();
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
import AEPServices

// Get the instance of the ServiceProvider
let serviceProvider = ServiceProvider.shared
```

{% endtab %}
{% endtabs %}

### Networking

The `Networking` service provides shared functionality to make asynchronous network requests and handle their responses.

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

### DataQueuing

The `DataQueuing` service provides access to thread-safe FIFO queues. This service is particularly useful when used in conjunction with a `PersistentHitQueue`.

The following code snippet shows how to create a `DataQueue` and add a `DataEntity` to the queue.

{% tabs %}
{% tab title="Android" %}

```java
DataQueue dataQueue = ServiceProvider.getInstance().getDataQueueService().getDataQueue(name);
DataEntity dataEntity = new DataEntity(mydata);
dataQueue.add(dataEntity);
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
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

### SystemInfoService (iOS) & DeviceInforming (Android)

The `SystemInfoService` (iOS) and the `DeviceInforming`(Android) service let you access critical pieces of information related to the user's device, such as carrier name, device name, locale, and more. 

The following code snippet shows how to invoke the API to retrieve the user's active locale.

{% tabs %}
{% tab title="Android" %}

```java
DeviceInforming deviceInfoService = ServiceProvider.getInstance().getDeviceInfoService();
String localName = deviceInfoService.getLocaleString();
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
// Add a computed variable to your type or use it directly in the function where required
private var systemInfoService: SystemInfoService {
  return ServiceProvider.shared.systemInfoService
}

// ...
let locale = systemInfoService.getActiveLocaleName()
```

{% endtab %}
{% endtabs %}

#### Public Interfaces

{% tabs %}
{% tab title="Android" %}

```java
public interface DeviceInforming {

	/**
	 * Represents the possible network connection status for the Adobe SDK.
	 *
	 */
	enum ConnectionStatus {
		/**
		 * Network connectivity exists.
		 */
		CONNECTED,
		/**
		 * No Network connectivity.
		 */
		DISCONNECTED,
		/**
		 * Unknown when unable to access the connectivity status.
		 */
		UNKNOWN
	}

	/**
	 * Represents the possible device types.
	 */
	enum DeviceType {
		PHONE,
		TABLET,
		WATCH,
		UNKNOWN
	}

	interface NetworkConnectionActiveListener {
		/**
		 * Invoked when the connection has become active.
		 */
		void onActive();
	}

	interface DisplayInformation {

		/**
		 * Returns absolute width of the available display size in pixels.
		 *
		 * @return width in pixels if available. -1 otherwise.
		 */
		int getWidthPixels();

		/**
		 * Returns absolute height of the available display size in pixels.
		 *
		 * @return height in pixels if available. -1 otherwise.
		 */
		int getHeightPixels();

		/**
		 * Returns the screen dots-per-inch
		 *
		 * @return dpi if available. -1 otherwise.
		 */
		int getDensityDpi();

	}

	/**
	 * Returns the directory which can be used as a application data directory.
	 *
	 * @return A {@link File} representing the application data directory, or null if not available on the platform
	 */
	File getApplicationBaseDir();

	/**
	 * Returns active locale's value in string format. The default value is en-US
	 *
	 * @return Locale as {@code String}
	 */
	String getLocaleString();

	/**
	 * Returns the default platform/device user agent value
	 *
	 * @return {@link String} containing the default user agent
	 */
	String getDefaultUserAgent();

	/**
	 * Returns the application specific cache directory. The application will be able to read and write to the
	 * directory, but there is no guarantee made as to the persistence of the data (it may be deleted by the system
	 * when storage is required).
	 *
	 * @return A {@link File} representing the application cache directory, or null if not available on the platform.
	 */
	File getApplicationCacheDir();

	/**
	 * Open the requested asset returns an InputStream to read its contents.
	 *
	 * @param fileName asset's name which is to be retrieved
	 * @return an {@link InputStream} to read file's content, or null if not available on the platform
	 */
	InputStream getAsset(String fileName);

	/**
	 * Returns the property value specific to the key from the manifest file.
	 *
	 * @param resourceKey resource key
	 * @return A {@link String} value of the requested property, or null if there is no value defined for the key
	 */
	String getProperty(String resourceKey);

	/**
	 * Returns the application name.
	 *
	 * @return A {@link String} representing Application name if available, null otherwise
	 */
	String getApplicationName();

	/**
	 * Returns the application package name.
	 *
	 * @return A {@link String} representing Application package name if available, null otherwise
	 */
	String getApplicationPackageName();

	/**
	 * Returns the application version.
	 *
	 * @return A {@link String} representing Application version if available, null otherwise
	 */
	String getApplicationVersion();

	/**
	 * Returns the application version code as a string.
	 *
	 * @return application version code formatted as {@link String} using the active locale, if available. null otherwise
	 */
	String getApplicationVersionCode();

	/**
	 * Returns the currently selected / active locale value (as set by the user on the system).
	 *
	 * @return A {@link Locale} value, if available, null otherwise
	 */
	Locale getActiveLocale();

	/**
	 * Returns information about the display hardware, as returned by the underlying OS.
	 *
	 * @return {@link DeviceInforming.DisplayInformation} instance, or null if application context is null
	 *
	 * @see DeviceInforming.DisplayInformation
	 */
	DeviceInforming.DisplayInformation getDisplayInformation();

	/**
	 * Returns the current screen orientation
	 *
	 * @return a {@code int} value indicates the orientation. 0 for unknown, 1 for portrait and 2 for landscape
	 */
	int getCurrentOrientation();

	/**
	 * Returns the string representation of the canonical platform name.
	 *
	 * @return Platform name {@link String}.
	 */
	String getCanonicalPlatformName();

	/**
	 * Returns the string representation of the operating system version.
	 *
	 * @return Operating system version {@link String}.
	 */
	String getOperatingSystemVersion();

	/**
	 * The device manufacturer's name.
	 *
	 * @return Device manufacturer name {@link String} if available. null otherwise
	 */
	String getDeviceManufacturer();

	/**
	 * Returns the device name.
	 *
	 * @return {@link String} Device name if available, null otherwise
	 */
	String getDeviceName();

	/**
	 * Returns the device type.
	 *
	 * <ul>
	 *     <li>If {@link DeviceInforming.DeviceType#PHONE}, for a Phone type device</li>
	 *     <li>If {@link DeviceInforming.DeviceType#TABLET}, for a Tablet type device</li>
	 *     <li>If {@link DeviceInforming.DeviceType#WATCH}, for a Watch type device</li>
	 *     <li>If {@link DeviceInforming.DeviceType#UNKNOWN}, when device type cannot be determined</li>
	 * </ul>
	 *
	 * @return {@link DeviceInforming.DeviceType} representing the device type
	 * @see DeviceInforming.DeviceType
	 */
	DeviceInforming.DeviceType getDeviceType();

	/**
	 * Returns a string that identifies a particular device OS build. This value may be present on
	 * Android devices, with a value like "M4-rc20". The value is platform dependent and platform specific.
	 *
	 * @return {@link String} Build ID string if available. null otherwise
	 */
	String getDeviceBuildId();

	/**
	 * Returns the device's mobile carrier name.
	 *
	 * @return A {@link String} representing the carrier name. null if this value is not available
	 */
	String getMobileCarrierName();

	/**
	 * Indicates whether network connectivity exists and it is possible to establish connections and pass data.
	 * <p>Always call this before attempting to perform data transactions.
	 *
	 * <ul>
	 *     <li>If {@link DeviceInforming.ConnectionStatus#CONNECTED}, if we have network connectivity.</li>
	 *     <li>If {@link DeviceInforming.ConnectionStatus#DISCONNECTED}, if do not have network connectivity.</li>
	 *     <li>If {@link DeviceInforming.ConnectionStatus#UNKNOWN}, if unable to determine the network connectivity.</li>
	 * </ul>
	 *
	 * @return {@link DeviceInforming.ConnectionStatus} representing the current network status
	 * @see DeviceInforming.ConnectionStatus
	 */
	DeviceInforming.ConnectionStatus getNetworkConnectionStatus();

	/**
	 * Invokes a callback when the network connection status changes.
	 *
	 * @param listener {@link DeviceInforming.NetworkConnectionActiveListener} listener that will get invoked once when the connection status changes.
	 * @see #getNetworkConnectionStatus()
	 *
	 * @return whether the registration was successful
	 */
	boolean registerOneTimeNetworkConnectionActiveListener(DeviceInforming.NetworkConnectionActiveListener listener);

	/**
	 * Returns a string that identifies the SDK running mode, e.g. Application, Extension.
	 *
	 * @return {@link String} containing running mode
	 */
	String getRunMode();

	/**
	 * Returns the current version of the Core, as provided by the platform.
	 *
	 * @return {@link String} containing the SDK Core version
	 */
	String getCoreVersion();

}
```

{% endtab %}

{% tab title="iOS(AEP 3.x)" %}

```swift
/// This service provides system info as needed
public protocol SystemInfoService {
    /// Gets a system property for the given key
    ///  - Parameter key: The key to be used to get the property value
    ///  - Return: `String` representation of the property
    func getProperty(for key: String) -> String?

    /// Gets a system asset for the given path
    ///  - Parameter fileName: The asset's name
    ///  - Parameter fileType: The file's extension e.g "txt", "json"
    ///  - Return: `String?` representation of the asset,
    func getAsset(fileName: String, fileType: String) -> String?

    /// Gets a system asset for the given path
    ///  - Parameter fileName: The asset's name
    ///  - Parameter fileType: The file's extension e.g "txt", "json"
    ///  - Return: `[UInt8]?` representation of the asset
    func getAsset(fileName: String, fileType: String) -> [UInt8]?

    /// Gets the device name
    /// - Return: `String` the device name
    func getDeviceName() -> String

    /// Gets the mobile carrier name
    /// - Return: `String` the mobile carrier name
    func getMobileCarrierName() -> String?

    /// Gets the run mode (Extension, or Application) as a string
    /// - Return: `String` the run mode as a string
    func getRunMode() -> String

    /// Gets the application name
    /// - Return: `String` the application name
    func getApplicationName() -> String?

    /// Gets the application's build number
    /// - Return: `String` the application's build number
    func getApplicationBuildNumber() -> String?

    /// Gets the application's version number
    /// - Return: `String` the application's version number
    func getApplicationVersionNumber() -> String?

    /// Gets the operating system's name
    /// - Return: `String` the operating system's name
    func getOperatingSystemName() -> String

    /// Gets the operating system's version
    /// - Return: `String` the operating system's version
    func getOperatingSystemVersion() -> String

    /// Gets the string representation of the canonical platform name
    /// - Return: `String` the platform name name
    func getCanonicalPlatformName() -> String

    /// Gets the display information for the system
    /// - Return: `DisplayInformation` the system's display information
    func getDisplayInformation() -> (width: Int, height: Int)

    /// Gets the default platform/device user agent
    /// - Return: `String` representing the default user agent
    func getDefaultUserAgent() -> String

    /// Returns the currently selected / active locale name (as set by the user on the system).
    /// - Return: `String` representation of the locale name
    func getActiveLocaleName() -> String

    /// Returns the device type
    /// - Return: `DeviceType` the type of the Apple device
    func getDeviceType() -> DeviceType

    /// Returns the application bundleId.
    /// - Return: `String` Application bundle id
    func getApplicationBundleId() -> String?

    /// Returns the application version.
    /// - Return: `String` Application version
    func getApplicationVersion() -> String?

    /// Returns the current orientation of the device
    /// - Return: `DeviceOrientation` the current orientation of the device
    func getCurrentOrientation() -> DeviceOrientation

    /// Returns the current device model number
    /// - Return: `String` representation of the current model number of the device
    func getDeviceModelNumber() -> String
}

public enum DeviceType {
    case PHONE
    case PAD
    case TV
    case CARPLAY
    case UNKNOWN
}

public enum DeviceOrientation {
    case PORTRAIT
    case LANDSCAPE
    case UNKNOWN
}
```

{% endtab %}
{% endtabs %}

## Override network stack

This section walks through the steps necessary to create a custom network override, and register it with the SDK.

{% hint style="info" %}
This feature is only available in Android Core version 2.5.0 or later and iOS Core version 2.6.0 or later.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

### 1. Create custom HTTPConnectionPerformer implementation

The `HTTPConnectionPerformer` class is an abstract base class that must be subclassed. This class contains one required method, `connect`, which must be overridden. Optionally, it's possible to override the `shouldOverride` method if you want to conditionally override network requests (if you do not override this method, all requests will be overridden by default).

#### Example

{% hint style="warning" %}
This is just an implementation example. For more information about handling network requests correctly in your mobile application, see [HttpURLConnection](https://developer.android.com/reference/java/net/HttpURLConnection).
{% endhint %}

```java
package com.adobe.example;

import java.io.BufferedOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;
import java.net.HttpURLConnection;
import java.net.MalformedURLException;
import java.net.URL;
import java.util.Map;
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider.HTTPConnectionPerformer;
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider.Connection;

// Sample implementation of HTTPConnectionPerformer for AEP SDK Network Override.
class SampleHTTPConnectionPerformer extends HTTPConnectionPerformer {        
  // Modifications here would allow for conditional overriding based on the url/method.
  // Overriding this method is optional, by default it will always return true (meaning
  // all network requests should be overridden).
  @Override
  public boolean shouldOverride(String url, String method) {
    return true;
  }

  // Overriding the connect method is required.  This method must perform a synchronous
  // (blocking) network request and return an object conforming to the
  // Connection interface.
  @Override
  public Connection connect(String url, String method, byte[] payload, Map<String, String> headers, int connectionTimeoutSeconds, int readTimeoutSeconds) {
    try {
      final URL dest = new URL(url);
      final HttpURLConnection con = (HttpURLConnection) dest.openConnection();
      con.setReadTimeout(readTimeoutSeconds * 1000);
      con.setConnectTimeout(connectionTimeoutSeconds * 1000);

      con.setRequestMethod(method);

      for (final Map.Entry<String, String> entry : headers.entrySet()) {
        con.setRequestProperty(entry.getKey(), entry.getValue());
      }

      if (method.equals("POST") && payload != null) {
        con.setFixedLengthStreamingMode(payload.length);
      }

      con.connect();

      if (method.equals("POST") && payload != null) {
        final OutputStream os = new BufferedOutputStream(con.getOutputStream());
        os.write(payload);
        os.flush();
        os.close();
      }

      final InputStream inputStream = con.getInputStream();
      final int responseCode = con.getResponseCode();
      final String responseMessage = con.getResponseMessage();

      return new AndroidNetworkServiceOverrider.Connection() {
        @Override
        public InputStream getInputStream() {
          return inputStream;
        }

        @Override
        public int getResponseCode() {
          return responseCode;
        }

        @Override
        public String getResponseMessage() {
          return responseMessage;
        }

        @Override
        public String getResponsePropertyValue(String responsePropertyKey) {
          final String responseHeaderValue = con.getHeaderField(responsePropertyKey);
          return responseHeaderValue;
        }

        @Override
        public void close() {
          if (inputStream != null) {
            try {
              inputStream.close();
            } catch (final Exception ex) {
            }
          }
          con.disconnect();
        }
      };


    } catch (final MalformedURLException ex) {
      return CONNECTION_ERROR_URL;

    } catch (final IOException ex) {
      return CONNECTION_ERROR_IO;
    }
  }
}
```

{% hint style="info" %}
Your implementation must return an object conforming to the `Connection` interface when the connection has succeded. If the connection does not succeed, you will need to return these constants (depending on the scenario):

* For all URL parsing / malformed URL issues, return `HTTPConnectionPerformer.CONNECTION_ERROR_URL`. 
* For any IOExceptions or any other errors, return `HTTPConnectionPerformer.CONNECTION_ERROR_IO`.
{% endhint %}

### 2. Register your interface with the SDK.

This step should occur prior to any other interactions with the AEP SDK. While it's possible to register the network override at any point during the application lifecycle, the override will only function for network requests performed after the registration has taken place.

```java
import com.adobe.marketing.mobile.AndroidNetworkServiceOverrider;
import com.adobe.marketing.mobile.MobileCore;

public void onCreate() {
    super.onCreate();

  // Register network override prior to making any other calls to the AEP SDK
  AndroidNetworkServiceOverrider.setHTTPConnectionPerformer(new SampleHTTPConnectionPerformer());

  // First call to AEP SDK
  MobileCore.setApplication(this);
  //... continue with initialization / registering extensions.
}
```
{% endtab %}

{% tab title="iOS" %}
### 1. Conform to the ACPHttpConnectionPerformer protocol

The `ACPHttpConnectionPerformer` is a protocol which must be conformed to in order to override the network stack. It provides two methods which must be implemented:

1. `shouldOverride`, which takes a URL and an HTTP method. Return true if you want the network stack to be overridden by the performer, or false if not. 
2. `requestUrl`, which is the URL request override with a completion block.

### 2. Create an ACPHttpConnection and pass relevant data from your NSURLSessionDataTask completion block

The completion block for the `requestUrl` method takes an `ACPHttpConnection` as its parameter. The `ACPHttpConnection` is used when overriding the network stack in place of the internal network connection implementation and represents the response to an HTTP request. It is to be created using the NSURLResponse and NSData from your url request response. In the case of a Network Error, or timeout, the `ACPHttpConnection*` is expected to be nil.

#### Example

{% hint style="warning" %}
This is just an implementation example. For more information about handling network requests correctly in your mobile application, see [NSURLSessionConfiguration](https://developer.apple.com/documentation/foundation/nsurlsessionconfiguration) and [NSMutableURLRequest](https://developer.apple.com/documentation/foundation/nsmutableurlrequest).
{% endhint %}

**Objective-C**

```objectivec
#import <Foundation/Foundation.h>
#import "ACPNetworkServiceOverrider.h"

@interface SamplePerformerOverrider : NSObject<ACPHttpConnectionPerformer>

@end

@implementation SamplePerformerOverrider {
    void (^requestUrlCompletion)(ACPHttpConnection*);
}

  // Modifications here would allow for conditional overriding based on the url/method.
  // In this example it always returns true to override all network requests.
- (BOOL) shouldOverride: (NSURL*) url method: (NSString*) method {
    return true;
}

    // Network request override with a completion block. The provided parameters should be configured on the network request.
- (void) requestUrl: (NSURL*) url httpCommand: (NSString*) command connectPayload: (NSString*) payload requestPropertyDict: (NSDictionary<NSString*, NSString*>*) requestProperty connectTimeout: (NSTimeInterval) connectTimeout readTimeout: (NSTimeInterval) readTimeout completion: (void (^) (ACPHttpConnection*)) completion {

    requestUrlCompletion = completion;

    // Create the NSURLSessionConfiguration with the provided timeouts
    NSURLSessionConfiguration* config = [NSURLSessionConfiguration ephemeralSessionConfiguration];
    config.URLCache = nil;
    config.timeoutIntervalForRequest = readTimeout;
    config.timeoutIntervalForResource = connectTimeout;

    NSURLSession* session = [NSURLSession sessionWithConfiguration:config];

    // Create an NSURLRequest with the provided request parameters
    NSMutableURLRequest* request = [NSMutableURLRequest new];
    [request setCachePolicy:NSURLRequestReloadIgnoringLocalCacheData];
    [request setHTTPMethod:command];
    [request setURL:url];

      if (payload.length > 0 && [@"POST" isEqualToString:[command uppercaseString]]) {
       [request setHTTPBody:[payload dataUsingEncoding:NSUTF8StringEncoding]];
    }

    for (NSString *key in requestProperty) {
        NSString* value = requestProperty[key];
        [request setValue:value forHTTPHeaderField:key];
    }

    // Start the request
    NSURLSessionDataTask* task;
    task = [session dataTaskWithRequest:request
                      completionHandler: ^ (NSData * data, NSURLResponse * response, NSError * error) {
                if(!error) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;

            // ***** NOTE the creation of the ACPHttpConnection outlined in step 2.*****
            ACPHttpConnection* connOverride = [[ACPHttpConnection alloc] initWithResponse:httpResponse data:data];
            completion(connOverride); 
        } else {
            completion(nil);
        }
    }];
    [task resume];
}

@end
```

**Swift**

```swift
import Foundation
import ACPCore

class SamplePerformerOverrider: NSObject, ACPHttpConnectionPerformer {

    // Modifications here would allow for conditional overriding based on the url/method.
    // In this example it always returns true to override all network requests.
    func shouldOverride(_ url: URL, method: String) -> Bool {
      return true
    }

    // Network request override with a completion block. The provided parameters should be configured on the network request.
    func request(_ url: URL, httpCommand command: String, connectPayload payload: String, requestPropertyDict requestProperty: [String : String], connectTimeout: TimeInterval, readTimeout: TimeInterval, completion: @escaping (ACPHttpConnection?) -> Void) {

      // Create the URLSessionConfiguration with the provided timeouts
      let config = URLSessionConfiguration.ephemeral
      config.urlCache = nil
      config.timeoutIntervalForRequest = readTimeout
      config.timeoutIntervalForResource = connectTimeout

      let session = URLSession(configuration: config)

      // Create an NSURLRequest with the provided request parameters
      let request = NSMutableURLRequest.init(url: url)
      request.cachePolicy = NSURLRequest.CachePolicy.reloadIgnoringLocalCacheData
      request.httpMethod = command

      if !payload.isEmpty && "POST" == command.uppercased() {
        request.httpBody = payload.data(using: .utf8)
      }

      for property in requestProperty {
        request.setValue(property.value, forHTTPHeaderField: property.key)
      }

      // Start the request
      let task = session.dataTask(with: url, completionHandler: { (data, response, error) in
        if error == nil {
          let httpResponse = response as? HTTPURLResponse
          // create ACPHttpConnection object with the data received and call the completion handler
          let connectionOverride = ACPHttpConnection(response: httpResponse, data: data)
          completion(connectionOverride)
        } else {
          completion(nil)
        }
      })
      task.resume()
    }
}
```

### 3: Register your ACPHttpConnectionPerformer with the SDK

This step should occur prior to any other interactions with the AEP SDK. While it's possible to register the network override at any point during the application lifecycle, the override will only function for network requests performed after the registration has taken place.

#### Example

**Objective-C**

```objectivec
#import "SamplePerformerOverrider.h"
#import "ACPCore.h"

@implementation AppDelegate

-(BOOL)application:(UIApplication *)application 
didFinishLaunchingWithOptions:(NSDictionary<UIApplicationLaunchOptionsKey, id> *)launchOptions {
        ...
        [ACPNetworkServiceOverrider setHttpConnectionPerformer:[[SamplePerformerOverrider alloc] init]];
        ...
        [ACPCore start:^{
        ...
        }];
```

**Swift**

```swift
import ACPCore

@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    var window: UIWindow?
    func applicationDidFinishLaunching(_ application: UIApplication) {
        ...
        ACPNetworkServiceOverrider.setHttpConnectionPerformer(SamplePerformerOverrider())
        ACPCore.start {
        ...
        }
```
{% endtab %}
{% endtabs %}

