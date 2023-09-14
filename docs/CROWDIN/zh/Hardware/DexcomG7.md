# Dexcom G7

```{admonition} Only available in dev branch
:class: note

This feature is only available in the in dev branch and not in master.

Please be aware of the warnings and follow the instructions in [building a dev version](../Installing-AndroidAPS/Dev_branch.md).

```

## Fundamental in advance

In spring 2022, the Dexcom G7 received its CE certificate and was sold at the end of October '22.

Noteworthy is the fact that the G7 system, compared to the G6, does not smooth the values, neither in the app, nor in the reader. More details about this [here](https://www.dexcom.com/en-us/faqs/why-does-past-cgm-data-look-different-from-past-data-on-receiver-and-follow-app). Consequently, the values have to be smoothed to be able to use them sensibly in AAPS.

There are **two** possibilities (as of 02/'23).

![DexcomG7.md](../images/DexcomG7.png)

## 1.  Patched Dexcom G7 App

### Install a new patched (!) G7 app and start the sensor

A patched Dexcom G7 app gives acess to the Dexcom G7 data. This is not the BYODA app as this app can not receive G7 data at the moment.

Uninstall the original Dexcom app if you used it before (A running sensor session can be continued - note the sensor code before removal of the app!)

Download and install the patched.apk [here](https://github.com/authorgambel/g7/releases).

Enter sensor code in the patched app.

Follow the general recommendations for CGM hygiene and sensor placement found [here](../Hardware/GeneralCGMRecommendation.md).

After the warm-up phase, the values are displayed as usual in the G7 app.

### build a new signed APK from the dev branch

To be able to receive the values from the G7 App in AAPS and to smooth the received values, a change in AAPS is necessary.

Therefore build a new signed APK from the official dev branch and install it on your mobile.

For the configuration in AAPS
- Select 'BYODA' in the configuration generator - even if it is not the BYODA app!
- If AAPS does not receive any values, switch to another BG source and then back to 'BYODA' to invoke the query for approving data exchange between AAPS and BYODA.

The smoothing of glucose values can be activated by enabling the "Average smoothing" or "Exponential Smoothing" plugin in the Config Builder. To disable select the "No Smoothing" option. "Exponential smoothing" is more aggressive and rewrites the newest Glucose Value but is good in dealing with heavy noise. "Average smoothing" is much like the back smoothing that was in BYODA G6 and only rewrites the past values but not the current value and therefore has a faster response time.

**Exponential Smoothing** **MUST** be enabled for meaningful use of the G7 values.

## 2. Xdrip+ (companion mode)

-   Download and install Xdrip+: [xdrip](https://github.com/NightscoutFoundation/xDrip)
- As data source in Xdrip "Companion App" must be selected and under Advanced Settings > Bluetooth Settings > "Companion Bluetooth" must be enabled.
- In AAPS select  > Configuration > BG source > xDrip+. Adjust the xDrip+ settings according to the explanations on the xDrip+ settings page  [xDrip+ settings](../Configuration/xdrip.md) 
