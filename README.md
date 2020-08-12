## Dell-Inspiron-759x

![ScreenShot](https://github.com/cassius425/Dell-Inspiron-7590-Hackintosh/blob/master/Assets/ScreenShot.png)

### System configuration

| Model     | MacBookPro15,3      | Version        | 10.15.6                |
| :-------- | :------------------ | :------------- | :--------------------- |
| Processor | Intel Core i7-9750H | Graphics       | UHD Graphics 630       |
| Memory    | 2666MHz DDR4 2x8GB  | OS Disk        | Toshiba 512GB PCle     |
| Audio     | Realtek ALC295      | WiFi/Bluehtoot | Intel Wireless-AC 9560 |

### About build

1. This EFI is modified based on the [Dell-Inspiron-7591-Hackintosh](https://github.com/tctien342/Dell-Inspiron-7591-Hackintosh) shared by @[tctien342](https://github.com/tctien342), thank you for sharing.
2. OC boot has been updated to 0.6.0.
3. All kext to latest.
4. Use the built-in Intel network card, Bluetooth driver : [IntelBluetoothFirmware](https://github.com/zxystd/IntelBluetoothFirmware), WiFi driver: [itlwm](https://github.com/OpenIntelWireless/itlwm) , WiFi needs to be used with [HeliPort](https://github.com/OpenIntelWireless/HeliPort) client,  first drive the driver, and then open the client.
5. If using DW1820A, Please move to [tctien342/Dell-Inspiron-7591-Hackintosh](https://github.com/tctien342/Dell-Inspiron-7591-Hackintosh) to view the configuration process, this article will not explain.

#### Not Working

- AirPods
- AirPort
- Internal Microphone
- Nvidia Geforce GTX 1650

#### To be tested

- Micro SD Card Reader

### Installation

#### BIOS

- Disk in `AHCI` mode
- Fastboot:  `Thorough`
- Power on lid: `Disabled`

#### Step

- Prepair an Mac installer in USB with bootloader you choice ( Use unibeast to create it )
- Replace EFI folder in USB EFI partition with this shipped EFI folder ( find the folder with name is `EFI` from zip file)
- Boot into USB and select MacOs installer
- After install success, run CombojackFix/install.sh in terminal
- Then you need to mount EFI partition and replace it with USB's EFI
- After System EFI replaced by your EFI, Using Opencore Configurator, Clover Configurator or update script to change SMBIOS, generate your serial and MBL
- Use NullEthernet for fixing iMess and FaceTime - Change MAC in NullEthernet with your new created one, see below

#### Fake ethernet

- Generate your MAC address in SSDT-RMNE if using NullEthernet
- You can make an MacAddress in [Mac generator online](https://www.browserling.com/tools/random-mac)
- Edit SSDT-RMNE.aml with MaciASL and replace MAC with your generated one
- Save as -> ACPI machine language (replace exited one)
- Add it to your bootloader:
  - Kext add in Kexts:
    - Copy kext to Kexts and add it into Kernel in config.plist (Use OpencoreConfigurator)
  - AML's file add to ACPI folder (Opencore need add to ACPI after copy SSDT file to ACPI, use OpencoreConfigurator)
- Reboot

