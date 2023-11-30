# Microsoft Edge Policies

## Linux

The mandatory prolicies should be put in `/etc/opt/edge/policies/managed/managed.json`, and the recommended policies should be put in `/etc/opt/edge/policies/recommended/recommended.json`

## macOS

The mandatory prolicies should be put in `/Library/Managed Preferences/com.microsoft.Edge.plist`, and the recommended policies should be put in `/Library/Preferences/com.microsoft.Edge.plist`

macOS is problematic, as it will wipe `/Library/Managed Preferences` every boot if you are not using an MDM. I work around this by putting the policies in `/Library/Tomster Corporation`, and use a cronjob as root to copy it every boot:

```
@reboot sleep 5 && cp -r '/Library/Tomster Corporation/' '/Library/Managed Preferences'
```

I have also noticed that Microsoft Edge does not seem to reload Managed Preferences probably until the computer reboots. Note that this may not work after a macOS update, and you will need to reboot the computer again for the policies to apply. I am not sure if this is a macOS behavior or if it is caused because my machine is not enrolled in an MDM.

Alternatively, you can try to convert the .plist files to .mobileconfig files and install them as profiles.