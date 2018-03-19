---
title: 'Updating Android when rooted'
date: 2015-04-21 00:00:00 
tags: 
layout: post
---
1. Download current version factory image - https://developers.google.com/android/nexus/images

2. Download OTA for the new version - e.g. http://www.androidpolice.com/2015/04/13/flash-all-the-things-android-5-1-ota-roundup-for-nexus-devices/

3. Download TWRP - http://twrp.me/Devices/

3. Uninstall SuperSU

4. Reboot into bootloader - `adb reboot bootloader`

5. Extract current factory image - `tar xf <filename>.tgz` - and then unzip the images - `unzip image-*.zip`

6. Flash original image parts and reboot - `fastboot flash recovery recovery.img && fastboot flash bootloader bootloader*.img && fastboot reboot-bootloader`

7. Select `Recovery Mode` from the bootloader

8. Press `power + volume up` to get the recovery menu

9. Select `apply update from ADB`

10. Install the OTA update - `adb sideload <really-long-file-name>.zip`

11. Reboot, check everything is okay and it's on the new very and then reboot again - `adb reboot bootloader`

12. Flash TWRP recovery - `fastboot flash recovery twrp*.img`

13. Reboot back to the bootloader - `fastboot reboot-bootloader`

14. Select `Recovery Mode` and check TWRP is there

15. Reboot from within TWRP and it should ask if you want to install root. Say yes

If you get any errors about file content mismatches then at the bootloader menu you may need to run `fastboot flash system system.img`

---

Shorter list of commands in order

```
adb reboot bootloader
tar xf <factory-image>.tgz
cd <folder>
unzip image-*.zip
fastboot flash bootloader bootloader*.img
fastboot flash recovery recovery.img
fastboot reboot-bootloader
```

Select recovery mode, `power + volume up`

```
adb sideload <file>.zip
```

Check all is okay after rebooting

```
adb reboot bootloader
fastboot flash recovery twrp*.img
fastboot reboot-bootloader
```

Boot into recovery again and check TWRP is there. Reboot from within TWRP and install root when prompted.
