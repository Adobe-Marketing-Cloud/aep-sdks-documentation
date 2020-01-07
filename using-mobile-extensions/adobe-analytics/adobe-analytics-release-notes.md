# Release Notes

## October 28, 2019
The following change was made in this release:

### iOS Analytics 2.2.1
* Analytics response content events now contain two new fields:
  * `hitHost`
  * `hitUrl`

These fields contain the host and URL of the of the hit responsible for dispatching the response event.

### Android Analytics 1.2.2
* Analytics response content events now contain two new fields:
  * `hitHost`
  * `hitUrl`

These fields contain the host and URL of the of the hit responsible for dispatching the response event.

## October 7, 2019
The following updates were made in this release:

### Android Analytics 1.2.1
* Fixed a bug where, on start up, the Analytics database was being modified by multiple threads.

## September 10, 2019
The following updates were made in this release:

### Android Analytics 1.2.0
* Added the following new pieces of data when reporting a crash:
  * `previousosversion`
  * `previousappid`

* Added support for the Griffon debug API.
* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.

### iOS Analytics 2.2.0
* Added support for Griffon debug API.
* The `global.ssl` configuration settings are ignored, and SSL is enabled by default.

## July 9, 2019
The following updates were made in this release:

### iOS Analytics 2.1.2
* ACPAnalytics now correctly identifies Acquisition link event types.
* Fixes a compile-time error when using the “-all_load” linker flag.


