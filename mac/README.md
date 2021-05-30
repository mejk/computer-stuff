## When things have gone wrong and you need to recover your Mac (happens far too often)
- [List of Mac startup key combinations](https://support.apple.com/en-us/HT201255). Some of the most important ones are:
  - Command (⌘)-R: Recovery mode
  - Option (⌥ or Alt) - Command (⌘) - R: Internet recovery. Also upgrade to latest compatible version.
  - Shift - option (⌥ or Alt) - Command (⌘) - R: Internet recovery. Install the original version of MacOS.
  - Shift (⇧): Safe mode
  - Command (⌘)-S: single user mode
  - T target mode
  - Note: Most of the internet upgrade and recovery options require ~35 GB of free space.

## How to disable the built-in keyboard on a MacBook

Why? Some MacsBooks, especially Air, have keyboard problems. If your warranty has expired there is not much to do except to use an external keyboard and in that case it is better to disabe the internal one as the faulty keys tend to lock and keep repeating the last character if you press the keys. With this fix the laptop is usable again.

Update: While the below work on older Macs, the commands seem not to work when usingh Big Sur.
```
sudo kextunload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext
```
renable
```
sudo kextload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext
```

- [Karabiner-elements](https://karabiner-elements.pqrs.org/) does the job on Big Sur too.
