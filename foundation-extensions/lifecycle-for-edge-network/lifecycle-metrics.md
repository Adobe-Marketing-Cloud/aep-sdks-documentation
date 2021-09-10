# Lifecycle for Edge Network metrics
The metrics auto-collected by the Lifecycle for Edge Network are defined in the [AEP Mobile Lifecycle Details XDM field group](https://github.com/adobe/xdm/blob/master/docs/reference/adobe/experience/aep-mobile-lifecycle-details.schema.md). 

## Lifecycle Application Foreground metrics
The following metrics are collected on each Lifecycle Application Foreground event.

### Application

| **Property** | **Type** | **DescriptIon** |
| :--- | :--- | :--- |
| xdm:id | String | Identifier of the application. |
| xdm:name | String | Name of the application. |
| xdm:version | String | Version of the application. |
| xdm:isLaunch | boolean | Launch of an application. Every application foreground event sets `isLaunch` to `true`.|
| xdm:isInstall | boolean | Install of an application. If `true`, signifies the first launch of the application. The Experience Event's timestamp property can be used as the application's install date.|
| xdm:isUpgrade | boolean | Upgrade of an application. If `true`, signifies the first launch of the application after an upgrade.|

### Device
| **Property** | **Type** | **DescriptIon** |
| :--- | :--- | :--- |
| xdm:type | String |Type of device being tracked. |
| xdm:manufacturer | String | The name of the organization who owns the design and creation of the device. |
| xdm:model | String | he name of the model for the device. |
| xdm:modelNumber | String | The unique model number designation assigned by the manufacturer for this device. |
| xdm:screenHeight | integer | The number of vertical pixels of the device's active display in the default orientation. |
| xdm:screenWidth | integer | The number of horizontal pixels of the device's active display in the default orientation. |

### Environment
| **Property** | **Type** | **DescriptIon** |
| :--- | :--- | :--- |
| xdm:type | String |The type of the application environment.|
| xdm:carrier | String | A mobile network carrier or MNO, also known as a wireless service provider, wireless carrier, cellular company, or mobile network carrier. |
| xdm:operatingSystem | String |The name of the operating system used when the observation was made.| 
| xdm:operatingsystemVersion | String |The full version identifier for the operating system used when the observation was made. |
| dc:language | String | The language of the environment to represent the user's linguistic, geographical, or cultural preferences for data presentation. |

## Lifecycle Application Background metrics
The following metrics are collected on each Lifecycle Application Background event.

### Application

| **Property** | **Type** | **DescriptIon** |
| :--- | :--- | :--- |
| xdm:isClose | boolean | Close of an application. Every application background event sets `isClose` to `true`.|
| xdm:closeType | String | Type of application close, sent on application isClose. Type is "close" on graceful termination of an application, or "unknown" when application termination source is unknown.|
| xdm:sessionLength | integer | Length of the application session in seconds. Usually referred as the time the application was in foreground. Will not be less than zero.|
