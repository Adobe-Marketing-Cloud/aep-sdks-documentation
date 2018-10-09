# Frequently Asked Questions

## 

## How much space does the SDK take?

| Extension | iOS \(size in KB\) | Android \(size in KB\) |
| :--- | :--- | :--- |
| Mobile Core | 772 | 168 |
| Adobe Analytics | 120 | 21 |
| Adobe Audience Manager | 80 | 13 |
| Adobe Target | 130 | 27 |
| Profile Framework | 45 | 8 |
| Acquisition Framework | 60 | 12 |

### Calculation assumptions

* Core Extension is required for all other extensions, so final app size increase can be calculated by adding Core size to each of the enabled extensions. For example: iOS app distribution using Target and Analytics would have a total size increase of 1,022kb \(Mobile Core: 772 + Target: 130 + Target: 120\). 
* iOS - Calculations are based on Xcode’s App Thinning size report using a bare-bones application to establish a baseline size. 
* Android "empty" app size = 1,284 KB. Size estimates listed refer to unsigned apps and do not account for proguarding.

