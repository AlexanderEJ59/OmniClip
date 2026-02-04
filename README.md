# 📋 OmniClip

OmniClip is a lightweight Xposed module designed to restore universal, global clipboard access across all applications and display environments.

### 📜 Origin & Credits
**Please Note:** OmniClip is a modification of the logic found in Entr0pia's fork of the **[xposed-clipboard-whitelist module](https://github.com/entr0pia/xposed-clipboard-whitelist)**. This specific iteration was born out of the frustration of trying to use a functional clipboard while **Android Auto** is running, where the system's "Invalid Device ID" checks break the copy-paste flow between the phone and external interfaces.

> 📢 IMPORTANT:
>
> >**Source Code Unavailable:** Original source code is not included in this repository, the provided APK is the result of decompiling the original APK of [this module](https://github.com/entr0pia/xposed-clipboard-whitelist) and applying several smali patches.

---

### ⚠️ SECURITY WARNING
**OmniClip bypasses Android's built-in clipboard security model.** By design, Android restricts clipboard access to prevent background apps from "scraping" sensitive information like passwords or 2FA codes. 

**By installing this module, you acknowledge that:**
* **Any app** on your device can read your clipboard at any time.
* Background access protections are completely disabled.
* Sensitive data copied to your clipboard is potentially exposed to all installed applications.

---

### 🤔 Why OmniClip?
In recent Android versions (particularly Android 13 and 14), access is often denied if:
1.  **Background Restrictions:** The requesting app does not have current window focus.
2.  **Virtual Displays:** The app is running on **Android Auto**, **scrcpy**, or **WSA**, which the system flags with an "Invalid Device ID" (`-1`).
3.  **Cross-User Barriers:** The app is trying to access data across different user profiles.

### 🎓 How It Works
The module applies hooks to `com.android.server.clipboard.ClipboardService`:

* **Device ID Normalization:** Forces `getIntendingDeviceId` to return `0` (`DEVICE_ID_DEFAULT`), tricking the system into believing every request originates from the main phone display.
* **Permission Authorization:** Short-circuits `clipboardAccessAllowed` to always return `true`, granting access to background callers.

### 📝 Installation
1.  Install the OmniClip APK.
2.  Enable the module in your Xposed manager (e.g., **LSPosed**).
3.  Set **"System Framework"** as the scope.
4.  **Reboot** your device.
