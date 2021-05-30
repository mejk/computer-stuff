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

```
sudo kextunload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext
```
renable
```
sudo kextload /System/Library/Extensions/AppleUSBTopCase.kext/Contents/PlugIns/AppleUSBTCKeyboard.kext
```
