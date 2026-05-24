---
title: 'How to Unlock Bootloader and Flash Pixel Firmware'
date: 2026-05-24
draft: false
categories: ["Android Rescue"]
---

Flashing a Pixel is a two-part process. You must unlock the bootloader before you can overwrite the system firmware.

### Checklist
* **USB-C Cable:** Use a high-quality data cable (avoid charge-only cables).
* **Platform-Tools:** Download [Android SDK Platform-Tools](https://developer.android.com/tools/releases/platform-tools){:target="_blank" rel="noopener noreferrer"} and extract it.
* **Google USB Drivers:** Install the [Google USB Driver](https://developer.android.com/studio/run/win-usb){:target="_blank" rel="noopener noreferrer"} if you are on Windows.
* **Factory Image:** Download the correct firmware for your specific model from [Google’s Pixel Factory Images](https://developers.google.com/android/images){:target="_blank" rel="noopener noreferrer"}. Extract the zip file and move all contents into your `platform-tools` folder.

### Part 1: Unlocking the Bootloader
*Note: This will wipe your phone entirely. Back up your data first.*

1. **Enable Developer Options:** Go to **Settings > About Phone** and tap **Build Number** 7 times.
2. **Enable OEM Unlocking:** Go to **Settings > System > Developer Options** and toggle on **OEM Unlocking**.
3. **Boot to Fastboot:** Turn the phone off. Hold **Volume Down + Power** until the Fastboot menu appears.
4. **Connect:** Plug the phone into your PC.
5. **Unlock:** Open a terminal in your `platform-tools` folder and run:
   `fastboot flashing unlock`
6. **Confirm:** Use the volume buttons on the phone to select "Unlock the bootloader" and press Power to confirm. The phone will reset.

### Part 2: Flashing the Firmware

1. **Boot to Fastboot:** Turn off the phone and hold **Volume Down + Power** again to reach the bootloader menu.
2. **Connect:** Ensure the phone is connected to your PC.
3. **Flash:** Run the script from the files you moved into the `platform-tools` folder:
   * **Windows:** Double-click `flash-all.bat`.
   * **Linux/Mac:** Run `./flash-all.sh`.
4. **Wait:** The phone will reboot multiple times. Do not touch the cable until the phone boots into the initial welcome/setup screen.

### Troubleshooting
* **"Command not found":** You are not running the command inside the `platform-tools` folder.
* **"Device not found":** Drivers are missing or the cable is faulty. Try a different USB port.
* **"Flash-all script fails":** If the script fails, try flashing the `bootloader`, `radio`, and `image` files manually using `fastboot flash` commands rather than the batch file.