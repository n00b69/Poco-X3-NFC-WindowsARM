<img align="right" src="https://github.com/wormstest/src_vayu_windows/blob/main/2Poco X3 Pro Windows.png" width="350" alt="Windows 11 Running On A Poco X3 NFC">

# Running Windows on the POCO X3 NFC

## Partitioning your device

### Prerequisites
- A brain (most important of all)

- [ADB & Fastboot](https://developer.android.com/studio/releases/platform-tools)
  
- [TWRP](https://mega.nz/file/zY4GCDRT#PxUKhUHkucj1oRH_Iu-R6exDak66hPeI71xJWHCTQkY) or [OrangeFox](https://drive.google.com/file/d/1eHM9ST9ni-55bbT3z-TGSZQsgE3KYr9s/view)

- [Parted](https://github.com/n00b69/woa-polaris/releases/download/Files/parted)

### Notes
> [!WARNING]  
> Do not run the same command twice unless specified.
> 
> DO NOT REBOOT YOUR PHONE! If you think you made a mistake, ask for help in the [Telegram chat](https://t.me/windows_on_pocox3_nfc).
> 
> Do not run all commands at once, execute them in order!
>
> YOU CAN BREAK YOUR DEVICE WITH THE COMMANDS BELOW IF YOU DO THEM WRONG!!!

### Booting the recovery
> Open a CMD window inside the platform-tools folder, then (while your phone is in fastboot mode) run
```cmd
fastboot boot path\to\twrp.img
```

#### Backing up important files
Use TWRP now to back up your Modem and EFS partition (as well as anything else if you have important data). Move this backup to a safe place (e.g your PC) as the next steps will wipe your data.

> [!Warning]
> All of your data will be erased. This is your last chance to back up.
> 
> **IF YOU PROCEED WITHOUT BACKING UP MODEM AND EFS, YOU ARE ON YOUR OWN IF YOU MESS UP**

### Partitioning guide
> Your Poco X3 NFC may have different storage sizes. This guide uses the values of the 128GB model as an example. When relevant, the guide will mention if other values can or should be used.

#### Unmount data
- Go to "Mount" in TWRP and unmount data, if it is mounted

#### Preparing for partitioning
> Download the parted file and move it in the platform-tools folder, then run
```cmd
adb push parted /cache/ && adb shell "chmod 755 /cache/parted" && adb shell /cache/parted /dev/block/sda
```

#### Printing the current partition table
> Parted will print the list of partitions, userdata should be the last partition in the list.
```cmd
print
```

#### Removing userdata
> Replace **$** with the number of the **userdata** partition, which should be **16**
```cmd
rm $
```

#### Recreating userdata
> Replace **10.8GB** with the former start value of **userdata** which we just deleted (it is probably 10.8GB)
>
> Replace **90GB** with the end value you want **userdata** to have
```cmd
mkpart userdata ext4 10.8GB 90GB
```

#### Creating ESP partition
> Replace **90GB** with the end value of **userdata**
>
> Replace **90.5GB** with the value you used before, adding **0.5GB** to it
```cmd
mkpart esp fat32 90GB 90.5GB
```

#### Creating Windows partition
> Replace **90.5GB** with the end value of **esp**
>
> Replace **123GB** with the end value of your disk, use `p free` to find it
```cmd
mkpart win ntfs 90.5GB 123GB
```

#### Making ESP bootable
> Use `print` to see all partitions. Replace "$" with your ESP partition number, which should be 17
```cmd
set $ esp on
```

#### Exit parted
```cmd
quit
```

#### Formatting data
- Format all data in TWRP, or Android will not boot.
- ( Go to Wipe > Format data > type yes )

#### Check if Android still starts
- Just restart the phone, and see if Android still works


## [Next step: Installing Windows](/guide/2-install.md)










































