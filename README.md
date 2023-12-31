# Microsoft Edge Policies

These policies are written with personal use in mind, so that I can configure Microsoft Edge for security and privacy on my personal systems. Certain features are disabled because I see them as unnecessary, annoying, or potentially privacy invasive. Microsoft has the tendency to implement features in the most privacy invasive way possible, so features that are not related to security are disabled unless they are explicitly documented to not have detremental effects on privacy.

Smartscreen is left as recommended to be be off, as it sends the FULL URLs of what are being visted to Microsoft. I decide whether to use it or not depending on the actual system that I am using.

For corporate environments, you will need make approprieate changes, including but not limited to:
- Disable `DeveloperToolsAvailability`. Users can be tricked into running malicious code in the browser console otherwise.
- Set `DefaultWebUsbGuardSetting` to "Block". In most cases, the websites will never need to use this API. I need it to flash GrapheneOS and StockOS on my phones.
- Set `DefaultJavaScriptJitSetting` to "Block". This will prevent users from adding exceptions to Enhanced Security Mode.
- Remove the uBlock Origin Lite extension whitelist. I am not aware of any way to block users from granting uBlock Origin Lite access to all content on a website, which is a security risk. If you know of a way to enforce that the extension runs permission-less, please let me know.
- Set `SSLErrorOverrideAllowed` to false.
- Further restrict permissions that websites can prompt for.
- Consider removing the `Disable3DAPIs` policy. Currently, WebGL is disabled in my policies and a few sites will break, so whether to do this highly depends on your organization.
- Consider mandating that `SmartScreenEnabled` is set to disabled. `TyposquattingCheckerEnabled` is also potentially invasive, though I have not confirmed this. Please make an issue to let me know of your findings.

## Linux

The mandatory policies should be put in `/etc/opt/edge/policies/managed/managed.json`, and the recommended policies should be put in `/etc/opt/edge/policies/recommended/recommended.json`

## macOS

The mandatory policies should be put in `/Library/Managed Preferences/com.microsoft.Edge.plist`, and the recommended policies should be put in `/Library/Preferences/com.microsoft.Edge.plist`

macOS is problematic, as it will wipe `/Library/Managed Preferences` every boot if you are not using an MDM. I work around this by making a fake MDM:

```zsh
umask 022
mkdir -p Library/Tomster Corporation/scripts/ Library/Tomster Corporation/prefs/
```

Create `/Library/PrivSec Corporation/scripts/apply_prefs.sh`:

```
#!/bin/zsh
/bin/sleep 5
/bin/cp -r '/Library/PrivSec Corporation/prefs/' '/Library/Managed Preferences/'
```

Set the correct permission:
```zsh
chmod 744 /Library/PrivSec Corporation/scripts/apply_prefs.sh
```

Put the managed policies at `/Library/Tomster Corporation/prefs/com.microsoft.Edge.plist`

Next, create `/Library/LaunchDaemons/io.tommytran.prefs.plist`:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>Label</key>
    <string>dev.privsec.prefs</string>
    <key>RunAtLoad</key>
    <true/>
    <key>LaunchOnlyOnce</key>
    <true/>
    <key>ProgramArguments</key>
    <array>
        <string>/Library/PrivSec Corporation/scripts/apply_prefs.sh</string>
    </array>
</dict>
</plist>
```

Finally, load in the service:

```
sudo launchctl load /Library/LaunchDaemons/dev.privsec.prefs.plist
```

I have also noticed that Microsoft Edge does not seem to reload Managed Preferences probably until the computer reboots. Note that this may not work after a macOS update, and you will need to reboot the computer again for the policies to apply. I am not sure if this is a macOS behavior or if it is caused because my machine is not enrolled in an MDM.

Alternatively, you can try to convert the .plist files to .mobileconfig files and install them as profiles.
