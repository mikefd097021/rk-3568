<div align="center">
  <div style="background: linear-gradient(45deg, #000428, #004e92); padding: 40px; border-radius: 10px; margin-bottom: 30px;">
    <h1 style="color: white; text-shadow: 2px 2px 4px rgba(0,0,0,0.5); font-size: 3em; margin: 0;">
      🔌 SD Card Boot Guide 💾
    </h1>
    <div style="background: url('https://github.com/mikefd097021/rk-3568/blob/main/res/b001.png?raw=true') center/cover; height: 5px; width: 80%; margin: 20px auto;"></div>
  </div>
</div>

## <span style="background: linear-gradient(to right, #00b4db, #0083b0); -webkit-background-clip: text; color: transparent;">Table of Contents</span>
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

## <span style="border-bottom: 3px solid #2196F3; padding-bottom: 5px;">Creating a Bootable SD Card</span>

### <span style="color: #1976D2;">🔧 Preparation</span>
1. Ensure you have downloaded the SDDiskTool and system image
2. Prepare an SD card (recommended capacity >= 32GB)
3. Connect the SD card to your computer

### <span style="color: #1976D2;">📝 Steps</span>

1. Launch SDDiskTool
   > 💡 You may need administrator privileges when running SDDiskTool for the first time.

   <div align="left">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/01.png?raw=true" alt="Launch SDDiskTool">
   </div>

2. Select the SD card device
   > ⚠️ WARNING: Double-check that you have selected the correct SD card. Selecting the wrong device could lead to permanent data loss on other storage devices.

3. Enable the SD Boot function
   > This step is crucial because it makes the SD card bootable.

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/02.png?raw=true" alt="Enable SD Boot option in SDDiskTool">
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

### <span style="color: #1976D2;">📌 Notes</span>
1. The creation process will erase all data on the SD card. Ensure that you back up important data beforehand.
2. If the creation process fails, check the following:
   - Ensure the SD card is properly inserted.
   - Verify that you have selected the correct device.
   - Confirm that the firmware file is complete and not corrupted.
   - Try running SDDiskTool with administrator privileges.

## <span style="border-bottom: 3px solid #2196F3; padding-bottom: 5px;">Flashing and Configuring the Root Filesystem</span>

### <span style="color: #1976D2;">📝 Steps</span>

1. Locate the rootfs partition (`/dev/sdd6`)
   > Refer to the location shown in the image below.
   > Note: Your device name might be different. Please verify the correct device name on your system.

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/1.png?raw=true" alt="Identifying rootfs partition in system">
   </div>
   
2. Check partition mount status
   > Run the following command in a terminal:
   ```bash
   mount | grep /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/2.png?raw=true" alt="Checking mount status of rootfs partition">
   </div>

   > If the partition is mounted, unmount it using:
   ```bash
   umount /dev/sdd6
   ```
   
   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/3.png?raw=true" alt="Unmounting rootfs partition">
   </div>

3. Flash the system image onto the rootfs partition
   > Replace <image_path> with the actual path to your system image file:
   ```bash
   dd if=<image_path> of=/dev/sdd6 bs=4M status=progress
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/4.png?raw=true" alt="Flashing system image using dd command">
   </div>

4. Create a mount directory
   > Create a directory to mount the rootfs partition:
   ```bash
   mkdir -p sd_rootfs
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/5.png?raw=true" alt="Creating mount directory for rootfs">
   </div>

5. Mount the rootfs partition
   > Mount the partition to verify and configure the filesystem:
   ```bash
   mount /dev/sdd6 sd_rootfs
   ```

6. Resize the partition
   > Expand the filesystem to use all available space on the partition:
   ```bash
   resize2fs /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/6.png?raw=true" alt="Resizing rootfs partition">
   </div>

7. Check the partition size after resizing
   > Verify the new partition size:
   ```bash
   df -h /dev/sdd6
   ```

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/7.png?raw=true" alt="Checking final partition size">
   </div>

### <span style="color: #1976D2;">📌 Notes</span>
1. Ensure you have root/administrator privileges to execute these commands
2. Always verify the device name (e.g., `/dev/sdd6`) matches your system
3. Back up any important data before proceeding with these operations
4. If you encounter any errors:
   - Verify all commands are executed with proper permissions
   - Check that the SD card is properly connected
   - Ensure the system image file is not corrupted

## <span style="border-bottom: 3px solid #2196F3; padding-bottom: 5px;">Booting from SD Card</span>

### <span style="color: #1976D2;">📝 Steps</span>

1. Insert the bootable SD card into the device's SD card slot

2. Hold the indicated button while powering on
   > Please refer to the highlighted area in the image below.

   <div align="center">
      <img src="https://github.com/mikefd097021/rk-3568/blob/main/res/001.png?raw=true" alt="Boot mode button location on device" width="600">
   </div>

## <span style="border-bottom: 3px solid #2196F3; padding-bottom: 5px;">Download Resources</span>

### <span style="color: #1976D2;">💿 System Image</span>

| Item | Content |
|------|---------|
| File Name | sdupdate.img |
| SHA256 | e5952745f70e8ade64298275c975e2bf3d6994f10b319bbc3efb50883d15f0f3 |
| Download Link | Please contact the relevant personnel to obtain it. |

### <span style="color: #1976D2;">🔧 Writing Tools</span>

| Item | Content |
|------|---------|
| File Name | SDDiskTool_v1.69.rar |
| Download Link | [Google Drive](https://drive.google.com/file/d/1r7RXZHWlw9ci0WIcBxocYn9qbAhL48nu/view?usp=sharing) |
| Password | Please contact the relevant personnel to obtain it. |