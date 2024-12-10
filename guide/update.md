<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Updating drivers

### Prerequisites
- [Modded TWRP](https://github.com/n00b69/woa-betalm/releases/download/Files/modded-twrp-g8s.img)

- [Drivers](https://github.com/n00b69/woa-betalm/releases/tag/Drivers)

- [UEFI image](https://github.com/n00b69/woa-betalm/releases/tag/UEFI)

### Reboot into fastboot mode
> If you don't have access to fastboot, use the instructions in the [partitioning guide](1-partition.md) to flash the engineering ABL.
- With the device turned off, hold the **volume down** button, then plug the cable in.

### Boot modified TWRP recovery
> Replace `path\to\modded-twrp-g8s.img` with the actual path of the image
```cmd
fastboot boot path\to\modded-twrp-g8s.img
```

#### Execute the msc script
```cmd
adb shell msc
```

> [!Note]
> **WINBETALM** should automatically appear in Windows Explorer. If it does, skip to the "Installing drivers" step, else continue with the "Diskpart" steps.

> [!Note]
> If you are facing issues (e.g your device does not enter mass storage mode), follow [the steps described in this guide](https://github.com/n00b69/woa-betalm/blob/main/guide/troubleshooting.md#mass-storage-mode-does-not-work) for alternative ways of entering mass storage mode.

### Diskpart
```cmd
diskpart
```

#### Select the phone's Windows volume
> Use `list volume` to find it, replace `$` with the actual number of **WINBETALM**
```diskpart
select volume $
```

#### Assign the letter x
```diskpart
assign letter x
```

#### Exit diskpart
```diskpart
exit
```

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINBETALM** (which should be **X**), then press enter

### Reboot your device
```cmd
adb reboot
```
> If you end up in Android instead of Windows, simply use the WOA Helper app to switch back.

## Finished!






















