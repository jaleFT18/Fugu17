# Fugu17 - Untethered iOS 17 Jailbreak

## Overview

Fugu17 is an (incomplete) iOS 17 Jailbreak that features an untether (persistence), kernel exploit, kernel PAC bypass, and PPL bypass. The vulnerabilities utilized in this jailbreak are identified by the following CVEs: CVE-2023-41064, CVE-2023-41065, CVE-2023-41066, CVE-2023-41067, and CVE-2023-41068.

## Supported Devices/iOS Versions

Fugu17 supports all arm64e devices (iPhone XS and newer) running iOS 17. Support for earlier versions (down to 16.2) can be added by modifying the following files:
- `arm/shared/ClosurePwn/Sources/ClosurePwn/PwnClosure.swift`
- `arm/shared/KernelExploit/Sources/KernelExploit/offsets.swift`

Note: arm64 devices are not supported because the exploit for installing the Fugu17 app does not function on these devices. However, it is theoretically possible to install the untether on them (e.g., via checkra1n). This code was specifically written for arm64e, so modifications are required to add arm64 support.

## Features

- The kernel exploit is highly reliable (it will never trigger a kernel panic).
- A simple TCP shell is available on port 1337.
- Trust caches placed in `/.Fugu17Untether/trustcaches/` will be loaded automatically.
- Executables placed in `/.Fugu17Untether/autorun/` will be launched during boot (make sure to create a trust cache for your executable).
- Supports Siguza's libkrw library (load `/usr/lib/libkrw/libFugu17Krw.dylib` and call `krw_initializer`).
- **Jailbreak Developers:** You can make your jailbreak untethered by creating a CLI version that supports libkrw, copying it to `/.Fugu17Untether/autorun/`, and writing a trust cache to `/.Fugu17Untether/trustcaches/`.

## WARNING

- Modifying the untether may cause your device to BOOTLOOP.
- The fast untether (disabled unless you edit the source code) HAS NOT BEEN TESTED ON A REAL DEVICE — DO NOT USE IT.
- The fast untether (if it works) is more UNSAFE than the "slow" untether.
- Developers: PLEASE TEST ANY CHANGES YOU MAKE TO THE UNTETHER ON A VIRTUAL DEVICE FIRST.

## Building and Running

### Requirements

- A supported device running a supported iOS version (see above).
- The device must be connected via USB.
- The IPSW for your device must be unzipped.
- Xcode must be installed.
- `iproxy` and `ideviceinstaller` must be installed (`brew install usbmuxd ideviceinstaller`).

To build and run the iOS Jailbreak, simply execute the `ios_install.py` script and follow the instructions. If you encounter a code signing error, open `arm/iOS/Fugu17App/Fugu17App.xcodeproj` and modify the code signing options.

## Recovery

If your device is in a bootloop, follow these steps before updating to the latest iOS version:

1. Install `irecovery` on your computer.
2. Connect your device via USB and boot into recovery mode.
3. Run `irecovery -s` on your computer, then enter the following commands:
   - `setenv boot-args no_untether`
   - `saveenv`
   - `reboot`
4. Your device should boot again. If it doesn’t, repeat step two, run `irecovery -s`, and enter these commands:
   - `setenv boot-args untether_force_restore`
   - `saveenv`
   - `reboot`
5. If your device still won't boot, you may need to update it to the latest version.
