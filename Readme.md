CIX P1 BIOS Community Version base on O6 Ecosystem Board
========================================================

# Summary

This is a port of ARM64 Tiano Core UEFI firmware, ATF and OPTEE for the O6 Ecosystem Board based on the CIX P1 SoC.

CIX P1 BIOS open source code is base on as follows:
- [edk2](https://github.com/tianocore/edk2): `fb493ac84ebc6860e1690770fb88183effadebfb`
- [edk2-platforms](https://github.com/tianocore/edk2-platforms): `8ea6ec38da8812f0703e8845fe639b8845704f96`
- [arm-trusted-firmware](https://github.com/ARM-software/arm-trusted-firmware): v2.7.0
- [optee-os](https://github.com/OP-TEE/optee_os/commits): v3.17.0

# How to download BIOS source code
  `git clone https://github.com/cixtech/bios.git -b cix_p1_community_dev ${YOUR_WORKSPACE} --recursive`

# How to build (X86 & ARM64 Linux Environment)
  From ${YOUR_WORKSPACE} run the following commands to download tools and setup environment:
  ```
  ln -s cix_package-tool/cix-build.sh cix-build.sh

  mkdir tools
  cd tools
  git clone https://github.com/acpica/acpica.git --branch R2024_12_12

  mkdir gcc
  cd gcc
  wget "https://developer.arm.com/-/media/files/downloads/gnu-a/10.2-2020.11/binrel/gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz?revision=79f65c42-1a1b-43f2-acb7-a795c8427085&rev=79f65c421a1b43f2acb7a795c8427085&hash=D1F7530466A8D7D3C25BA1D7D82C743C" -O gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz

  tar -xf gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz

  cd ../..

  ./cix-build.sh
  ```
  Found "cix_flash_all.bin" and "SKY1_BL33_UEFI.fd" in output folder

# How to Change OEM Key for sign ATF, TEE and UEFI code
  1. Directly replace OEM private key and pubic key in cix_package-tool/Keys
    Or
    Customize sign process in cix-build.sh

  2. Run build script cix-build.sh to re-generate new binary

# How to Flash Firmware
  1. Use SPI Flash Programmer(like DediProg SF100) by flash file "cix_flash_all.bin"

  2. Run FlashUpdate.efi(edk2-non-osi/Platform/CIX/Sky1/FlashTool/FlashUpdate.efi) under UEFI shell
    For Example:

    FS0:\>FlashUpdate.efi -f cix_flash_all.bin