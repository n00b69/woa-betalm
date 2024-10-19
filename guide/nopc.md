<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Installing Windows without a PC
> [!Warning]
> This page and its files are still in its early stages of development. Do not use unless you have been asked to test it.
> 
> Seriously, do not use it.

### Prerequisites
- Unlocked bootloader & rooted LG G8s

- [LG G8s WinInstaller](https://github.com/n00b69/woa-betalm/releases/tag/WinInstaller)

- [Windows on ARM image](https://arkt-7.github.io/woawin/)

- [Modified TWRP](https://github.com/n00b69/woa-betalm/releases/download/Files/moddedtwrp.img)

- [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA)

### Notes
> [!WARNING]  
> All your data will be erased! Back up now if needed.
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woahelperchat).

> [!Important]
> This guide assumes you have already unlocked your bootloader and are already rooted, if this is not the case, you'll still need a PC to do that.
> 
> This guide also requires you to use LineageOS, due to the lack of decryption support in TWRP when using the stock LG rom. 

### Flash the modified TWRP
- In **Magisk**, select the **betalm-twrp-installer.zip** and flash it.
- Return to the main menu, press the rotating arrow icon in the top right, and press `Reboot Recovery`.

#### Opening TWRP terminal
- Once booted into TWRP press the **Advanced** button on the bottom right of the screen, then press **Terminal**.
- Run all future commands in this terminal

#### Unmount data
```cmd
umount /dev/block/by-name/userdata
```

#### Preparing for partitioning
```cmd
parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **19** or **22**
```cmd
rm $
```

#### Recreating userdata
> Replace **17.7GB** with the former start value of **userdata** which we just deleted
>
> Replace **64GB** with the end value you want **userdata** to have. In this example your available usable space in Android will be 64GB-17.7GB = 47GB
```cmd
mkpart userdata ext4 1717GB 64GB
```

#### Creating ESP partition
> Replace **64GB** with the end value of **userdata**
>
> Replace **64.35GB** with the value you used before, adding **0.35GB** to it
```cmd
mkpart esp fat32 64GB 64.35GB
```

#### Creating Windows partition
> Replace **64.35GB** with the end value of **esp**
```cmd
mkpart win ntfs 64.35GB 126GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be **31**
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

### Formatting data and rebooting
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type `yes` ).
- Press the reboot button to reboot into Android.
> [!Note]
> If Android does not start after +- 10 minutes, reboot back into stock recovery and perform a factory reset there.

### Preparing necessary files
- Download the Windows image and make sure it remains in the `Download` folder of your **internal storage**.
- Download **WinInstaller.zip** and keep it in the `Download` folder as well.
- Download and install the [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA), then open it and grant it root access. Do not do anything else inside the app yet.

### Booting into TWRP
- Press the `Reboot to Recovery` button in the top right of Magisk again.
- Once booted into TWRP, enter your password if it asks you to.

### Flashing WinInstaller
- In TWRP, select **Install** and then locate **WinInstaller.zip** and flash it.
> [!Note]
- Wait untill all processes complete and your device boots into Windows. This will take around 15-20 minutes.

> [!Tip]
> If you wish to skip the Microsoft Account login, press the **I don't have internet** button in the WiFi page, then when prompted, press the **Continue with limited setup** button.

### Enabling GPU
> Currently, GPU drivers are not installed when you first boot Windows. To fix this, we do the following
- Navigate to `C:\installer\Driver` and run **OnlineUpdater.cmd**
- If a popup asks you to install an unverified driver, click `Install this driver anyway`.
- Once it is finished, open **Device Manager**, click on **Display Adapters**, then double click on **Microsoft Basic Display Adapter**.
- Press `Update Driver` > `Browse my computer for drivers` > `Let me pick from a list of available drivers on my computer`, then select **LG G8S Adreno 640 GPU** and press `Next`.
- Your screen should go black for a few seconds, after which you'll have succesfully installed the GPU drivers.

#### Booting to Android
- Run the **Android** shortcut on your desktop (you can also pin it to your start menu / taskbar for ease of access).

#### Booting to Windows
- Press **QUICKBOOT TO WINDOWS** inside the WOA Helper app, or use the newly created toggle in your quick settings panel.

## Finished!
