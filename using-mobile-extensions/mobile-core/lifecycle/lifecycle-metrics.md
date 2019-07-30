# Lifecycle metrics

## Install

| **Metric** | **Key** | **DescriptIon** |
| :--- | :--- | :--- |
| First Launches | a.InstallEvent | Triggered at the first run after installation or re-installation. |
| Install Date | a.InstallDate | Date of first launch after installation. The format is `M/d/yyyy`, and an example is `5/3/2017`. |

## Upgrade

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Upgrades | a.UpgradeEvent | Triggered at the first run after upgrade or when the version number changes. |
| Days since last upgrade | a.DaysSinceLastUpgrade | Number of days since the application version number changed.             **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric.|
| Launches since last upgrade | a.LaunchesSinceUpgrade | Number of launches since the application version number changed.          **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric.|

## Launch

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Daily Engaged Users | a.DailyEngUserEvent | Triggered when the application is used on a particular day.      **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Monthly Engaged Users | a.MonthlyEngUserEvent | Triggered when the application is used during a particular month.      **Important**: This metric is not automatically stored in an Analytics metric. You must create a processing rule that sets a custom event to capture this metric. |
| Launches | a.LaunchEvent | Triggered on every run, including crashes and installs. Also triggered when the app is resumed from the background after the lifecycle session timeout is exceeded. |
| Previous Session Length | a.PrevSessionLength | Reports the number of seconds that a previous application session lasted based on how long the application was open and in the foreground. |
| Ignored Session Length | a.ignoredSessionLength | If the last session is set to last longer than `lifecycle.sessionTimeout`, that session length is ignored and recorded here. |
| Launch Number | a.Launches | Number of times the application was launched or brought out of the background. |
| Days since first use | a.DaysSinceFirstUse | Number of days since first run. |
| Days since last use | a.DaysSinceLastUse | Number of days since last use. |
| Hour of Day | a.HourOfDay | Measures the hour the app was launched and uses the 24-hour numerical format. Used for time parting to determine peak usage times. |
| Day of Week | a.DayOfWeek | Measures the day of the week the app was launched. |

## Crash

| **Metric** | **Key** | **Description** |
| :--- | :--- | :--- |
| Crashes | a.CrashEvent | Triggered when the application crashed before closing. The event is sent when the application is started again after the crash. |

## Device Information

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Metric</b>
      </th>
      <th style="text-align:left"><b>Key</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">App ID</td>
      <td style="text-align:left">a.AppID</td>
      <td style="text-align:left">Stores the application name and version in the following format: <code>AppName BundleVersion (app version code)</code> .
        An example of this format is <code>MyAppName 1.1(1)</code>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Device Name</td>
      <td style="text-align:left">a.DeviceName</td>
      <td style="text-align:left">Stores the device name.</td>
    </tr>
    <tr>
      <td style="text-align:left">Operating System Version</td>
      <td style="text-align:left">a.OSVersion</td>
      <td style="text-align:left">Operating system name and version.</td>
    </tr>
    <tr>
      <td style="text-align:left">Carrier Name</td>
      <td style="text-align:left">a.CarrierName</td>
      <td style="text-align:left">
        <p>Stores the name of the mobile service provider as provided by the device.
          <br
          />
        </p>
        <p><b>Important</b>: This metric is not automatically stored in an Analytics
          variable. You must create a processing rule to copy this value to an Analytics
          variable for reporting.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Resolution</td>
      <td style="text-align:left">a.Resolution</td>
      <td style="text-align:left">Width x Height in pixels.</td>
    </tr>
    <tr>
      <td style="text-align:left">Locale</td>
      <td style="text-align:left">a.locale</td>
      <td style="text-align:left">Locale set for this device, for example, <em>en-US</em>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Run mode</td>
      <td style="text-align:left">a.RunMode</td>
      <td style="text-align:left">The SDK running mode, for example, <code>Application / Extension</code>.</td>
    </tr>
  </tbody>
</table>
