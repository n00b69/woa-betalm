<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm">

# Running Windows on the LG G8s

## Updating drivers without a PC
> [!Warning]
> This guide currently requires you to have LineageOS 20 installed, install it first if you haven't already.
>
> Decryption in TWRP does not work on stock LG roms.

### Prerequisites
- A rooted LG G8s running LineageOS 20 with Windows already installed

- [LG G8s DriverUpdater](https://github.com/n00b69/woa-betalm/releases/download/Files/BetalmDriverUpdater.zip)

- [Modified TWRP](https://github.com/n00b69/woa-betalm/releases/download/Files/twrp-installer-3.7.1_FBE_V2-betalm-windows.zip)

- [WOA Helper app](https://github.com/Marius586/WoA-Helper-update/releases/tag/WOA)

### Notes
> [!WARNING]  
> 
> DO NOT REBOOT YOUR PHONE if you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woahelperchat).

> [!Important]
> This guide assumes you have already installed Windows. If you haven't, use the [installation guide](nopc.md) instead.

### Preparing necessary files
- Download **BetalmDriverUpdater.zip** and keep it in your internal storage.

### Flash the modified TWRP
> Or boot into TWRP if you've already installed it.
- In **Magisk**, select the **betalm-twrp-installer.zip** and flash it.
- Return to the main menu, press the rotating arrow icon in the top right, and press `Reboot Recovery`.

### Flashing DriverUpdater
- In TWRP, select **Install** and then locate **BetalmDriverUpdater.zip** and flash it.
- Once you're given the option to reboot, do so.
> [!Note]
> Wait untill all processes complete and your device boots back Windows. This will take around 20-30 minutes.

## Finished!
