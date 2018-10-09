# Frequently Asked Questions

## 

## How much space does the SDK take?

### iOS

| Extension | Size \(in KB\) |
| :--- | :--- |
| Mobile Core | 772 |
| Adobe Analytics | 120 |
| Adobe Audience Manager | 80 |
| Adobe Target | 130 |
| Profile Framework | 45 |
| Acquisition Framework | 60 |

Calculations are based on Xcode’s App Thinning size report using a bare-bones application to establish a baseline size. Core Extension is required for all other extensions, so final app size increase can be calculated by adding Core size to each of the enabled extensions. For example: app distribution using Target and Analytics would have a total size increase of 1,022kb \(Mobile Core: 772 + Target: 130 + Target: 120\).



