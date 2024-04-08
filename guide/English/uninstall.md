<img align="right" src="https://github.com/wormstest/src_vayu_windows/blob/main/2Poco X3 Pro Windows.png" width="350" alt="Windows 11 Running On A Poco X3 NFC">

# Running Windows on the POCO X3 NFC

## Restore stock partition table

### Why do we need it?
If you want to uninstall Windows use this to avoid human error to avoid writing a guide dedicated only to uninstall.

If you want to lock your bootloader again you need the stock partition table

### Prerequisites
- [gpt_both0.bin](../../../../releases/label/Binaries)

### Flashing the stock GPT
> Replace ```<gpt_both0.bin>``` with the directory of gpt_both0.bin
``` cmd
fastboot flash partition: 0 <gpt_both0.bin>
```

#### Format user data to avoid bootloop and restore FS weight
``` cmd
fastboot -w
```

### Reboot to Android
```cmd
fastboot reboot
```

## Finished!


















