Some device manufacturers have made modifications to the Android system that prevent Gator from functioning properly. This issue can be observed on non-rooted devices that rely on Gator's Accessibility service to clear the cache, where the service is stopped despite previously being enabled.

To resolve this issue for affected users, Gator requires the `WRITE_SECURE_SETTINGS` permission, which cannot be obtained through the app on non-rooted devices. The `WRITE_SECURE_SETTINGS` permission allows Gator to re-enable the Accessibility service without requiring manual user interaction.

# How to Grant `WRITE_SECURE_SETTINGS` Permission to Gator

### Step 1: Install ADB on Your Computer

1. **Download ADB:**
   - Go to the [Android SDK Platform Tools download page](https://developer.android.com/tools/releases/platform-tools).
   - Download and extract the ZIP file to a folder on your computer (e.g., `C:\adb` on Windows or `/Users/yourname/adb` on macOS).

2. **Install ADB Drivers (for Windows users):**
   - If you're on **Windows**, make sure you have the correct USB drivers installed for your device. You can download them [here](https://developer.android.com/studio/run/oem-usb).

---

### Step 2: Enable Developer Options and USB Debugging on Your Android Device

1. **Open Settings** on your Android device.
2. Scroll down and tap **About Phone**.
3. Tap **Build Number** 7 times to unlock Developer Options.
4. Go back to **Settings** and tap **System** > **Developer Options**.
5. Enable **USB Debugging** by turning on the toggle.

---

### Step 3: Additional Device-Specific Steps

Before you can grant the `WRITE_SECURE_SETTINGS` permission, you may need to perform some additional steps depending on your device's manufacturer. 

#### **MIUI (Xiaomi, POCO)**

1. In **Developer Options**, enable **USB Debugging (Security options)**.
   - This option is separate from **USB Debugging** itself, and it is necessary for granting certain permissions.

#### **ColorOS (OPPO & OnePlus)**

1. In **Developer Options**, disable **Permission monitoring**. This will allow ADB commands to grant permissions to apps.

#### **Flyme (Meizu)**

1. In **Developer Options**, disable **Permission monitoring** to allow the necessary permissions to be granted via ADB.

---

### Step 4: Connect Your Device to Your Computer

1. Use a USB cable to connect your Android device to your computer.
2. A pop-up should appear on your phone asking if you want to allow USB debugging. Tap **Allow**.

---

### Step 5: Verify ADB Connection

1. Open **Command Prompt** (on Windows) or **Terminal** (on macOS/Linux).
2. Navigate to the folder where you extracted ADB. For example:
   - On **Windows**: `cd C:\adb`
   - On **macOS/Linux**: `cd /Users/yourname/adb`
3. Run the following command to check if your device is connected:
   ```bash
   adb devices

### Step 6: Grant the `WRITE_SECURE_SETTINGS` Permission to Gator

1. In your terminal or command prompt, run the following command:
   ```bash
   adb shell pm grant com.mitigator.gator android.permission.WRITE_SECURE_SETTINGS

### Step 7: Verify the Permission (Optional)

1. To confirm that the permission was successfully granted, you can run this command:
   ```bash
    adb shell dumpsys package com.mitigator.gator | grep WRITE_SECURE_SETTINGS

If everything is correct, you'll see the permission listed in the output.

```bash
android.permission.**WRITE_SECURE_SETTINGS**
android.permission.**WRITE_SECURE_SETTINGS**: granted=true
