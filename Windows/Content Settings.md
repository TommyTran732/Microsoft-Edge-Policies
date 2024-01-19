# Content Settings

`Computer Configuration\Policies\Administrative Templates\Microsoft Edge\Content Settings`

- Block cookies on specific sites -> ntp.msn.com `CookiesBlockedForUrls": [ "ntp.msn.com" ]`
- Default geolocation setting -> Enabled -> Don't allow any site to track users' physical location `DefaultGeolocationSetting: 2`
- Control use of insecure content Exceptions -> Enabled -> Do not allow any sites to load mixed content `DefaultInsecureContentSetting: 2`
- Configure cookies -> Enabled -> Keep cookies for the duration of the session, except ones listed in "SaveCookiesOnExit" `DefaultCookiesSetting: 4`
- Default setting for third-party storage partitioning -> Let third-party storage partitioning to be enabled. `DefaultThirdPartyStoragePartitioningSetting: 1`
- Control the use of File System API for reading -> Don't allow any site to request and read access to files and directories via the File System API `DefaultFileSystemReadGuardSetting: 2`
- Control the use of File System API for writing -> Don't allow any site to request and write access to files and directories via the File System API `DefaultFileSystemWriteGuardSetting: 2`
- Control use of the Web Bluetooth API -> Don't allow any site to request access to Bluetooth devices via the Web Bluetooth API `DefaultWebBluetoothGuardSetting: 2`
- Allow notifications to set Microsoft Edge as default PDF reader -> Disabled `ShowPDFDefaultRecommendationsEnabled: false`