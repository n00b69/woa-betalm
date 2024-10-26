<img align="right" src="https://github.com/n00b69/woa-betalm/blob/main/betalm.png" width="350" alt="Windows 11 running on betalm"> 

# Running Windows on the LG G8s 

## Uninstalling Windows 

### Prerequisites
- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools) 

- [Qfil](https://github.com/n00b69/woa-betalm/releases/tag/Qfil) 

- [Engineering ABL](https://github.com/n00b69/woa-betalm/releases/download/Files/engabl_ab.bin) Only needed if you don't have fastboot
  
- [Modded TWRP](https://github.com/n00b69/woa-betalm/releases/download/Files/moddedg8s.img) 

### Notes
> [!WARNING]
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!
>
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/woahelperchat). 

### Opening CMD as an admin
> Download **platform-tools** and extract the folder somewhere, then open CMD as an **administrator**.
>
> It is recommended to keep this window open and use it throughout the entire guide.
> 
> Replace `path\to\platform-tools` with the actual path to the platform-tools folder, for example **C:\platform-tools**.
```cmd
cd path\to\platform-tools
``` 

#### Setting up Qfil
> [!Note]
> If you have access to fastboot mode by default, skip to the [Reboot to fastboot mode](1-partition.md#reboot-to-fastboot-mode) step, because you do not need to use Qfil. 

- Open **Qfil**.
- In "Select Build Type", select **flat build**.
- In "Select programmer", select the downloaded firehose.
- In "Configuration", make sure the "Device Type" is set to **UFS**. 

#### Boot to EDL
- Open **Device Manager** on your PC
- With the phone turned off, hold **volume down** + **power**.
- After the LG logo appears, while still holding **volume down** + **power**, start rapidly pressing the **volume up** button.
- Keep doing this until you hear a USB connection sound on your PC, or when **Qualcomm HS-USB QDLoader 9008** appears in the **Ports (COM & LPT)** category of Device Manager.
- If the device is called **QUSB_BULK_CID** or has a ⚠️ yellow warning triangle / question mark, and is located in any other category (for example **Other devices**), you need to install EDL drivers first.
- To install EDL drivers, extract the contents of **QUD.zip** somewhere, right click on **QUSB_BULK_CID**, click on **Update driver** and **Browse my computer for drivers**, then find and select the **QUD** folder. 

#### Making sure Qfil works
- In **Qfil**, make sure the correct port is selected. If it says `No Port Available`, select the **Qualcomm HS-USB QDLoader 9008** port.
- At the top, select "Tools" > "Partition manager", and click **Ok**.
- If you see a **Download Fail:Sahara Fail** error, make sure your cable stays connected and reboot to EDL again by holding **volume down** + **power**, then start rapidly pressing the **volume up** button once the LG logo appears.
- Once you're back in EDL, try opening the Partition manager again.
- If it still fails, try to repeat the last step a few times. You can also try rebooting your phone and PC. 

#### Backing up ABL
- In the Partition manager, right click on **abl_a** > **Manage Partition Data** and press **Read Data**.
- Navigate to `C:\Users\YOURNAME\AppData\Roaming\Qualcomm\QFIL\COMPORT_#\` and rename the newly created backup to **abl_a.bin** 

### Flashing engineering ABL
- Right click on **abl_a** > **Manage Partition Data** and press **Load Image**.
- Select and flash the **engabl_ab.bin** file.
- Do the same thing for **abl_b**. 

### Reboot to fastboot mode
- Reboot your phone by holding **volume down** + **power** until it shows the LG logo, then release the buttons.
- After it has booted, unplug the cable and power it off.
- Once the device has turned off, hold the **volume down** button, then plug the cable back in.
- If the phone in device manager is called **Android** and has a ⚠️ yellow warning triangle, you need to install fastboot drivers before you can continue.
- To install fastboot drivers, extract the contents of **QUD.zip** somewhere, right click on **Android**, click on **Update driver** and **Browse my computer for drivers**, then find and select the **QUD** folder. 

#### Boot into the modded TWRP
> Replace `path\to\moddedg8s.img` with the actual path of the provided TWRP image
>
> After booting into TWRP, leave the device on the main screen. You can press the power button to turn the display off, if you want
```cmd
fastboot boot path\to\moddedg8s.img
``` 

### Preparing parted
> Replug the cable if it says "no devices/emulators found"
```cmd
adb shell parted /dev/block/sda
``` 

#### Delete Windows Partition
> Use `print all` to make sure that partition 32 is Windows
```sh
rm 32
``` 

#### Delete ESP Partition
> Use `print all` to make sure that partition 31 is ESP
```sh
rm 31
``` 

#### Resize userdata Partition
> Use `print all` to make sure that partition 30 is userdata
```sh
resizepart 30
126GB
``` 

#### Exit Parted
```sh
quit
``` 

### Reboot your phone
> Once it is booted, it should tell you decryption was unsuccesful and it will ask you to erase all data.
- Press this button to erase all data, let the phone boot back up, then reboot to make sure Android works. 

## Finished!
























