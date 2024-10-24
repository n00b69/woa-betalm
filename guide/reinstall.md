<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Reinstalling Windows

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)

- [Modded TWRP](https://github.com/n00b69/woa-betalm/releases/download/Files/moddedg8s.img)

### Reboot into fastboot mode
> If you don't have access to fastboot, use the instructions in the [partitioning guide](1-partition.md) to flash the engineering ABL.
- With the device turned off, hold the **volume down** button, then plug the cable in.

#### Boot into the modded TWRP
> Replace `path\to\moddedg8s.img` with the actual path of the provided TWRP image
>
> After booting into TWRP, leave the device on the main screen. You can press the power button to turn the display off, if you want
```cmd
fastboot boot path\to\moddedg8s.img
```

### Formatting Windows and ESP partitions
```cmd
adb shell mkfs.ntfs -f /dev/block/by-name/win -L WINBETALM
```

```cmd
adb shell mkfs.fat -F32 -s1 /dev/block/by-name/esp -n ESPBETALM
```

## [Next step: Reinstalling Windows](3-install.md)
































