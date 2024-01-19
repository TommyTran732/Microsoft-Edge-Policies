# Extensions

`Computer Configuration\Policies\Administrative Templates\Microsoft Edge\Extensions`

| Group Policy                                                         | Policy equivalent                     |
|----------------------------------------------------------------------|-------------------------------------|
| Control which extensions cannot be installed -> Enabled -> Show -> * | ExtensionInstallBlocklist": [ "*" ] |
| Configure extension management settings -> Enabled -> {"ddkjiahejlhfcafbddmgiahcphecmpfh": {"installation_mode": "allowed", "update_url": "https://clients2.google.com/service/update2/crx", "override_update_url": true, "sidebar_auto_open_blocked": true}} |   ExtensionSettings: {"ddkjiahejlhfcafbddmgiahcphecmpfh": {"installation_mode": "allowed", "update_url": "https://clients2.google.com/service/update2/crx", "override_update_url": true, "sidebar_auto_open_blocked": true}}