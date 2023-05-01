#The default input method on Windows was changed to others after reboot.

#Fix
Delete the registry key ```HKEY_USERS\.DEFAULT\Keyboard Layout\Preload```, and reboot.

``` bat
reg delete "HKEY_USERS\.DEFAULT\Keyboard Layout\Preload" /f
```
