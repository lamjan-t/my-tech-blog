---
title: 'How to Flash Official Stock Firmware on Google Pixel'
date: 2026-05-24
draft: false
categories: ["Android Rescue"]
---

If your Pixel is stuck in a bootloop, or you need to revert to stock after experimenting with custom ROMs, flashing the factory image is the only way to get a clean, official start.

### Checklist
* **USB-C Cable:** Use a high-quality data cable (avoid the cheap ones that only charge).
* **Platform-Tools:** You need the latest [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools) downloaded and extracted on your PC.
* **Battery:** Your phone must have at least 60% charge. If it dies mid-flash, you are looking at a hard-brick.
* **Backup:** This process wipes everything. If your data is still accessible, back it up now.

### The Fix

1. **Get the Image:** Go to the [official Google Pixel Factory Image site](https://developers.google.com/android/images), find your specific model, and download the latest version.
2. **Prepare the Files:** Extract the zip file you just downloaded. You will see a folder containing a series of `flash-all.bat` (Windows) or `flash-all.sh` (Linux/Mac) files, plus a large `image-modelname-version.zip` file.
3. **Connect to PC:** Move all those extracted files into your `platform-tools` folder.
4. **Bootloader Mode:** Turn your phone off. Hold **Volume Down + Power** until you see the Fastboot menu (the one with the Android lying on its back). Connect it to your PC.
5. **Unlock Bootloader (If needed):** If you are flashing from a different firmware or the device is locked, ensure `fastboot flashing unlock` has been run. 
6. **Execute:** * On Windows: Double-click `flash-all.bat`.
    * On Linux/Mac: Run `./flash-all.sh` in your terminal.

### Troubleshooting
* **"Command not found" or "Device not found":** Your PC is not talking to the phone. Reinstall your Google USB drivers or try a different USB port. 
* **The terminal window closes immediately:** Open a command prompt/terminal inside the `platform-tools` folder and run `flash-all.bat` manually. This lets you see the error message if the script crashes.
* **Stuck on the Google Logo:** This is normal after a flash. Give it at least 10 minutes. If it doesn't move, you may need to factory reset from the recovery menu.

---
### Cleanup
Once the phone reboots, it will be factory fresh. Go to **Settings > About Phone** and verify the build number matches what you flashed. If you want to keep the device secure, run `fastboot flashing lock` to re-lock the bootloader.