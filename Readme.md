CIX P1 BIOS
=======================================

# Summary

This is a port of ARM64 Tiano Core UEFI firmware for the CIX P1 SoC.

CIX P1 edk2 code is base on as follows:
- [edk2](https://github.com/tianocore/edk2): `fbe0805b2091393406952e84724188f8c1941837`
- [edk2-platforms](https://github.com/tianocore/edk2-platforms): `8ea6ec38da8812f0703e8845fe639b8845704f96`

# Support Board List

| Board | Code | Build Command | BIOS File Name |
| :---  | :--- | :--- | :--- |
| CIX P1 EVB Merak Board | edk2-platforms/Platform/CIX/Sky1/Merak | ./build_and_package.sh | cix_flash_all.bin |
| Radxa Orion O6 Board | edk2-platforms/Platform/Radxa/Orion/O6 | ./build_and_package.sh O6 | cix_flash_all.bin |
| CIX P1 Alcor & Rigel Board | edk2-platforms/Platform/CIX/Sky1/Alcor | ./build_and_package.sh Alcor | cix_flash_all2.bin |

# How to download BIOS source code
  `git clone https://github.com/cixtech/bios.git -b cix_p1_dev ${YOUR_WORKSPACE} --recursive`

# How to build (X86 Linux Environment)
  From ${YOUR_WORKSPACE} run the following commands to download tools and setup environment:

  ```
  ln -s edk2-non-osi/Platform/CIX/Sky1/PackageTool/build_and_package.sh build_and_package.sh

  mkdir tools
  cd tools
  git clone https://github.com/acpica/acpica.git --branch R2024_12_12

  mkdir gcc
  cd gcc
  wget "https://developer.arm.com/-/media/files/downloads/gnu-a/10.2-2020.11/binrel/gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz?revision=79f65c42-1a1b-43f2-acb7-a795c8427085&rev=79f65c421a1b43f2acb7a795c8427085&hash=D1F7530466A8D7D3C25BA1D7D82C743C" -O gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz

  tar -xf gcc-arm-10.2-2020.11-x86_64-aarch64-none-elf.tar.xz

  cd ../..

  ./build_and_package.sh or ./build_and_package.sh Alcor
  ```
  Find "cix_flash_all2.bin" and "SKY1_BL33_UEFI.fd" in output folder

# How to Change OEM Key for UEFI code
  1. Directly replace OEM private key and pubic key in edk2-non-osi/Platform/CIX/Sky1/PackageTool/Keys
    Or
    Customize sign process in build_and_package.sh

  2. Run build script build_and_package.sh to re-generate new binary

# How to Flash Firmware
  1. Use SPI Flash Programmer(like DediProg SF100) by flash file "cix_flash_all2.bin"

  2. Run FlashUpdate.efi(edk2-non-osi/Platform/CIX/Sky1/FlashTool/FlashUpdate.efi) under UEFI shell
    For Example:

    FS0:\>FlashUpdate.efi -f cix_flash_all2.bin