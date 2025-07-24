# OpenCore EFI for Ivy Bridge

This repository contains a complete OpenCore EFI configuration optimized for Ivy Bridge (3rd generation Intel Core) processors, designed for Hackintosh installations running macOS.

## System Information

Based on the configuration, this EFI is configured for:

- **CPU**: Intel Xeon W-3245M CPU @ 3.20 GHz (or similar Ivy Bridge processor)
- **Architecture**: Ivy Bridge (3rd Gen Intel Core)
- **OpenCore Version**: 1.0.5
- **Target macOS**: Compatible with modern macOS versions

## What's Included

### Core Components

- **OpenCore.efi**: Main bootloader (v1.0.5)
- **config.plist**: Fully configured for Ivy Bridge systems
- **BOOTx64.efi**: UEFI boot file

### Drivers

- `HfsPlus.efi` - HFS+ filesystem support
- `OpenCanopy.efi` - GUI boot picker
- `OpenRuntime.efi` - Memory management
- `ResetNvramEntry.efi` - NVRAM reset functionality

### Kexts (Kernel Extensions)
The configuration includes essential kexts for Ivy Bridge compatibility:

| Kext | Version | Purpose |
|------|---------|---------|
| Lilu.kext | V1.7.1 | Base patching platform |
| VirtualSMC.kext | V1.3.7 | SMC emulation |
| AirportBrcmFixup.kext | V2.2.0 | Broadcom WiFi support |
| AppleALC.kext | V1.9.5 | Audio codec support |
| AtherosE2200Ethernet.kext | V2.4.0 | Atheros ethernet support |
| CryptexFixup.kext | V1.0.5 | Cryptex compatibility |
| IntelMausi.kext | V1.0.8 | Intel ethernet support |
| RealtekRTL8111.kext | V2.5.0 | Realtek ethernet support |
| RestrictEvents.kext | V1.1.6 | System event restrictions |
| SMCProcessor.kext | V1.3.7 | CPU sensor support |
| SMCSuperIO.kext | V1.3.7 | SuperIO sensor support |
| USBInjectAll.kext | V0.8.1 | USB port injection |
| WhateverGreen.kext | V1.7.0 | Graphics patches |
| NVMeFix.kext | V1.1.3 | NVMe SSD compatibility |
| CtlnaAHCIPort.kext | V341.0.2 | AHCI port support |

### ACPI

- `MaLd0n.aml` - Custom ACPI patches for Ivy Bridge

### Resources

- **Audio**: Boot chime support with VoiceOver
- **Fonts**: Custom terminal fonts (Terminus)
- **Images**: Boot picker themes (Acidanthera variants)
- **Labels**: Localized boot entry labels

## Boot Arguments

The configuration includes optimized boot arguments:

```bash
-v alcid=1 watchdog=0 dk.e1000=0 e1000=0 agdpmod=vit9696 amfi_get_out_of_my_way=0x1 ngfxcompat=0x1 ngfxgl=1 nvda_drv_vrl=1
```

### Key Arguments

- `-v`: Verbose boot for troubleshooting
- `alcid=1`: Audio layout ID
- `watchdog=0`: Disable watchdog timer
- `agdpmod=vit9696`: AMD GPU compatibility
- `ngfxcompat=0x1`: NVIDIA compatibility mode

## SMBIOS Configuration

- **System Product Name**: MacPro7,1
- **System Serial Number**: F5KY20E2P7QM
- **System UUID**: ABA6B78F-61EE-4BF0-B0B2-A5C6F116DF08
- **ROM**: 241058F7D73D

## Installation Instructions

1. **Backup**: Always backup your existing EFI partition before making changes
2. **Copy EFI**: Copy the entire EFI folder to your EFI partition
3. **BIOS Settings**: Configure your BIOS for UEFI boot and disable Secure Boot
4. **Boot**: Use this EFI to boot your macOS installer or existing installation

## BIOS/UEFI Settings Recommendations

### Enable

- UEFI Boot Mode
- AHCI for SATA drives
- Intel VT-x (if using virtualization)

### Disable

- Secure Boot
- Fast Boot
- CSM/Legacy Boot
- Intel VT-d (unless needed)

## Features

- ✅ **Full macOS Compatibility**: Optimized for Ivy Bridge processors
- ✅ **Audio Support**: Working audio with AppleALC
- ✅ **Ethernet**: Multiple ethernet drivers included
- ✅ **USB**: Full USB support with injection
- ✅ **Graphics**: WhateverGreen for GPU acceleration
- ✅ **NVMe**: Modern NVMe SSD support
- ✅ **Boot Picker**: Beautiful GUI boot interface with GoldenGate theme

## Customization

### SMBIOS

Remember to generate your own unique SMBIOS data:

- SystemSerialNumber
- SystemUUID
- ROM (MAC address)

### Audio

If audio doesn't work, try different `alcid` values in boot arguments (common values: 1, 2, 3, 7, 11, 13, 28, 29).

## Troubleshooting

1. **Boot Issues**: Enable verbose mode (`-v`) and check for errors
2. **Audio**: Verify `alcid` value matches your codec
3. **Ethernet**: Ensure the correct ethernet kext for your hardware
4. **Graphics**: Check WhateverGreen compatibility with your GPU
5. **GUI Boot Picker Not Showing**: If OpenCanopy GUI doesn't appear:
   - Check if your GPU supports UEFI GOP (Graphics Output Protocol)
   - Try changing `PickerMode` from `External` to `Builtin` in config.plist
   - Ensure your monitor is connected to the GPU (not motherboard)
   - Some older GPUs may not support OpenCanopy - use text mode instead
   - Check BIOS settings: disable CSM, enable UEFI-only mode

### GUI Boot Picker Fix

The configuration is now optimized for the beautiful OpenCanopy GUI boot picker:

**Current Settings:**
- **PickerMode**: `External` (OpenCanopy GUI)
- **PickerVariant**: `Acidanthera\GoldenGate` (Beautiful golden theme)
- **PickerAttributes**: `17` (Optimized for compatibility)
- **Resolution**: `1920x1080@32` (Fixed resolution for stability)

**If GUI still doesn't appear:**

1. **Check BIOS Settings:**
   - Disable CSM (Compatibility Support Module)
   - Enable UEFI-only mode
   - Set primary display to PCIe (if using dedicated GPU)

2. **Graphics Requirements:**
   - Ensure monitor is connected to GPU (not motherboard)
   - GPU must support UEFI GOP (Graphics Output Protocol)
   - Most modern GPUs support this, but some older cards may not

3. **Fallback Options:**
   - Change `PickerVariant` to `Acidanthera\Syrah` for alternative theme
   - If still no GUI, change `PickerMode` to `Builtin` for text mode

## Compatibility

This EFI configuration is specifically designed for:

- **3rd Generation Intel Core processors (Ivy Bridge)**
- **Intel 7-series chipsets**
- **Compatible motherboards with UEFI firmware**

## Disclaimer

This EFI configuration is provided as-is for educational purposes. Always ensure you have legitimate access to macOS and compatible hardware. The author is not responsible for any damage to your system.

## Credits

- **OpenCore Team**: For the amazing bootloader
- **Acidanthera**: For the majority of kexts and tools
- **Community Contributors**: For testing and feedback

---

**Last Updated**: July 2025  
**OpenCore Version**: 1.0.5