<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Installing Windows

### Prerequisites
- [Mass storage image](https://github.com/n00b69/woa-betalm/releases/download/Files/msc.img)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)
  
- [Drivers](https://github.com/n00b69/woa-betalm/releases/tag/Drivers)

- [UEFI image](https://github.com/n00b69/woa-betalm/releases/tag/UEFI)

### Reboot into fastboot mode
- With the device turned off, hold the **volume down** button, then plug the cable in.

#### Boot into the mass storage mode image
> Replace `path\to\msc.img` with the actual path of the image
```cmd
fastboot boot path\to\msc.img
```

#### Enabling mass storage mode
> Once booted into the UEFI, use the volume buttons to navigate the menu and the power button to confirm
- Select **UEFI Boot Menu**.
- Select **USB Attached SCSI (UAS) Storage**.
- Press the **power** button twice to confirm.

> [!Note]
> If you are facing issues (e.g your device randomly reboots), follow [the steps described in this guide](https://github.com/n00b69/woa-betalm/blob/main/guide/troubleshooting.md#the-device-reboots-in-mass-storage-mode) for an alternative way of entering mass storage mode.

### Diskpart
> [!WARNING]
> DO NOT ERASE, CREATE OR OTHERWISE MODIFY ANY PARTITION WHILE IN DISKPART!!!! THIS CAN ERASE ALL OF YOUR UFS OR PREVENT YOU FROM BOOTING TO FASTBOOT!!!! THIS MEANS THAT YOUR DEVICE WILL BE PERMANENTLY BRICKED WITH NO SOLUTION! (except for flashing it with EDL, which is complicated)
```cmd
diskpart
```

#### Select the Windows volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **WINBETALM**
```diskpart
select volume $
```

#### Assign the letter X
```diskpart
assign letter x
```

#### Select the ESP volume of the phone
> Use `list volume` to find it, replace `$` with the actual number of **ESPBETALM**
```diskpart
select volume $
```

#### Assign the letter Y
```diskpart
assign letter y
```

#### Exit diskpart
```cmd
exit
```

### Installing Windows
> [!Warning]
> DO NOT USE 24H2!!!

> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim or 22631.2861.XXXXXXX.esd)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Copying your boot.img into Windows
- Drag and drop the **rooted_boot.img** from the **platform-tools** folder into the **WINBETALM** disk in Windows Explorer, then rename it to **boot.img**

### Installing drivers
- Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINBETALM** (which should be **X**), then press enter
  
#### Create the Windows bootloader files
> If any error shows up, such as "Failure when attempting to copy boot files", open `diskpart` again and assign any new letter to **ESPBETALM**, then replace the letter `Y` in the next commands with the letter that you just added.
```cmd
bcdboot X:\Windows /s Y: /f UEFI
```

#### Enabling test signing
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" testsigning on
```

#### Disabling recovery
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" recoveryenabled no
```

#### Disabling integrity checks
```cmd
bcdedit /store Y:\EFI\Microsoft\BOOT\BCD /set "{default}" nointegritychecks on
```

#### Remove the drive letter for ESP
> If this does not work, ignore it and skip to the next command. This phantom drive will disappear the next time you reboot your PC.
```cmd
mountvol y: /d
```

### Rebooting into fastboot mode
- Reboot into fastboot mode by holding the **volume down** + **power** buttons until the text on the screen disappears, then immediately release the **power** button whilst continuing to hold **volume down**.
> If your phone turns on instead, turn it off while the cable is plugged in, and keep holding tbe **volume down** button until it enters fastboot mode.

### Boot into the UEFI
> Replace `path\to\betalm-uefi.img` with the actual path of the image
```cmd
fastboot boot path\to\betalm-uefi.img
```

> After around 15 minutes your screen will go black. When it does, force reboot your device using **volume down** + **power**, then boot back into fastboot mode and boot the UEFI image one more time and wait until you see the language selection screen in Windows.

> You may notice that everything feels very slow. This is normal and will be fixed in the next step.

### Enabling GPU
> Currently, GPU drivers are not installed when you first boot Windows. To fix this, we do the following
- Open **Device Manager**, click on **Display Adapters**, then double click on **Microsoft Basic Display Adapter**.
- Press `Update Driver` > `Browse my computer for drivers` > `Let me pick from a list of available drivers on my computer`, then select **LG G8S Adreno 640 GPU** and press `Next`.
- Your screen should go black for a few seconds, after which you'll have succesfully installed the GPU drivers.

#### Reboot back into Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access)

## [Last step: Setting up dualboot](4-dualboot.md)






















