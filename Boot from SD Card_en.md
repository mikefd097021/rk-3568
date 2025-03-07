# SD Card Boot Guide

## Table of Contents
- [Creating a Bootable SD Card](#creating-a-bootable-sd-card)
  - [Preparation](#preparation)
  - [Steps](#steps)
  - [Notes](#notes)
- [Flashing and Configuring the Root Filesystem](#flashing-and-configuring-the-root-filesystem)
  - [Steps](#steps-1)
  - [Notes](#notes-1)
- [Booting from SD Card](#booting-from-sd-card)
  - [Steps](#steps-2)
- [Download Resources](#download-resources)
  - [System Image](#system-image)
  - [Writing Tools](#writing-tools)

# SD Card Boot Guide

## Creating a Bootable SD Card

### Preparation
1. Ensure you have downloaded the SDDiskTool and system image
2. Prepare an SD card (recommended capacity >= 32GB)
3. Connect the SD card to your computer

### Steps

1. Launch SDDiskTool
   > 💡 You may need administrator privileges when running SDDiskTool for the first time.

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/01.png?raw=true" alt="Launch SDDiskTool">
   </div>

2. Select the SD card device
   > ⚠️ Double-check that you have selected the correct SD card, as selecting the wrong device could lead to data loss on other storage devices.

3. Enable the SD Boot function
   > This step is crucial as it makes the SD card bootable

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/02.png?raw=true" alt="Enable SD Boot">
   </div>

4. Load the firmware file
   > Click the Firmware button and select the system image file (sdupdate.img).

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/03.png?raw=true" alt="Select firmware location" width="600">
   </div>

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/04.png?raw=true" alt="Load firmware file" width="600">
   </div>

5. Start creating the boot card
   > After confirming all settings, click Create to begin.
   > 
   > ⚠️ Do not remove the SD card during the process

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/05.png?raw=true" alt="Start creation">
   </div>

### Notes
1. The creation process will erase all data on the SD card. Ensure that you back up important data beforehand.
2. If the creation process fails, check the following:
   - Ensure the SD card is properly inserted.
   - Verify that you have selected the correct device.
   - Confirm that the firmware file is complete and not corrupted.
   - Try running SDDiskTool with administrator privileges.

## Flashing and Configuring the Root Filesystem

### Steps

1. Locate the rootfs partition (`/dev/sdd6`)
   > Please refer to the location shown in the image below

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/1.png?raw=true" alt="rootfs partition location">
   </div>
   
2. Check partition mount status
   > Run the following command in a terminal:
   ```bash
   mount | grep /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/2.png?raw=true" alt="Operation screenshot">
   </div>

   > If mounted, unmount using:
   ```bash
   umount /dev/sdd6
   ```
   
   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/3.png?raw=true" alt="Operation screenshot">
   </div>

3. Flash the system image onto the rootfs partition
   > Use the dd command:
   ```bash
   dd if=<image_path> of=/dev/sdd6 bs=4M status=progress
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/4.png?raw=true" alt="Operation screenshot">
   </div>

4. Create a mount directory
   > Execute:
   ```bash
   mkdir -p sd_rootfs
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/5.png?raw=true" alt="Operation screenshot">
   </div>

5. Mount the rootfs partition
   > Execute:
   ```bash
   mount /dev/sdd6 sd_rootfs
   ```

6. Resize the partition
   > Execute:
   ```bash
   resize2fs /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/6.png?raw=true" alt="Operation screenshot">
   </div>

7. Check the partition size after resizing
   > Execute:
   ```bash
   df -h /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/7.png?raw=true" alt="Operation screenshot">
   </div>

### Notes
1. Ensure you have sufficient permissions to execute these commands
2. Verify the device name (e.g., `/dev/sdd6`) is correct before proceeding
3. Backing up important data before operation is recommended

## Booting from SD Card

### Steps

1. Insert the bootable SD card

2. Hold the indicated button while powering on
   > Please refer to the highlighted area in the image below.

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/001.png?raw=true" alt="Operation screenshot" width="600">
   </div>

## Download Resources

### System Image

| Item | Content |
|------|---------|
| File Name | sdupdate.img |
| SHA256 | e5952745f70e8ade64298275c975e2bf3d6994f10b319bbc3efb50883d15f0f3 |
| Download Link | Please contact the relevant personnel to obtain it. |

### Writing Tools

| Item | Content |
|------|---------|
| File Name | SDDiskTool_v1.69.rar |
| Download Link | [Google Drive](https://drive.google.com/file/d/1r7RXZHWlw9ci0WIcBxocYn9qbAhL48nu/view?usp=sharing) |
| Password | Please contact the relevant personnel to obtain it. |