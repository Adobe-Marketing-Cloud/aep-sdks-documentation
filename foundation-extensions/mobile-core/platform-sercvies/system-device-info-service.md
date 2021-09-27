## SystemInfo Service (iOS) & DeviceInfo Service (Android)

## Overview

The `SystemInfo Service` (iOS) and the `DeviceInfo Service`(Android) let you access critical pieces of information related to the user's device, such as carrier name, device name, locale, and more. 

## Usage

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