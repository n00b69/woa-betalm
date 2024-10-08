<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Reinstalling Windows

### Prerequisites
- [Windows on ARM image](https://arkt-7.github.io/woawin/)
  
- [Drivers](https://github.com/n00b69/woa-betalm/releases/tag/Drivers)

- [Mass storage image](https://github.com/n00b69/woa-betalm/releases/download/Files/msc.img)

- [UEFI image](https://github.com/n00b69/woa-betalm/releases/tag/UEFI)

### Reboot to fastboot mode
> If you don't have access to fastboot, use the instructions in the [partitioning guide](1-partition.md) to flash the engineering ABL.
- With the device turned off, hold the **volume down** button, then plug the cable in.
- If the phone in device manager is called **Android** and has a ⚠️ yellow warning triangle, you need to install fastboot drivers before you can continue.

#### Boot to the mass storage mode image
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
> After 1-2 minutes **WINBETALM** should automatically appear in Windows Explorer. If it does, skip to the "Formatting Windows" step, else continue with the "Diskpart" steps.

### Diskpart
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

#### Exit diskpart
```cmd
exit
```

#### Formatting Windows
> Go to Windows Explorer > This PC and select **WINBETALM**. Right click and format as NTFS.

### Installing Windows
> Replace `path\to\install.esd` with the actual path of install.esd (it may also be named install.wim)

```cmd
dism /apply-image /ImageFile:path\to\install.esd /index:6 /ApplyDir:X:\
```

> If you get `Error 87`, check the index of your image with `dism /get-imageinfo /ImageFile:path\to\install.esd`, then replace `index:6` with the actual index number of **Windows 11 Pro** in your image

### Installing Drivers
> Unpack the driver archive, then open the `OfflineUpdater.cmd` file (if an error shows up, run `OfflineUpdaterFix.cmd` instead)

> If it asks you to enter a letter, enter the drive letter of **WINBETALM** (which should be **X**), then press enter

### Boot into Windows
Reboot your phone. If you end up in Android instead of Windows, flash the UEFI again using WOA Helper.

#### Setting up Windows
> Your device will now set up Windows. This will take some time. It will eventually reboot, and after that the initial setup (oobe) should launch.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

## Finished!

































