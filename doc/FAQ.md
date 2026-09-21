# ❓ Frequently Asked Questions (FAQ)

Find answers to common questions about using Sail, managing your access vouchers, and ensuring optimal privacy.

---

### 1. What happens when my JWT RSA token runs out of data or expires?

Once your token hits its data quota limit (gigabytes consumed), the secure connection tunnel will close automatically.

- To resume service under **Anonymity Mode**, you must obtain a brand-new token string and add it as a new profile in your client app.
- Because we hold user privacy as our first priority, there is no automatic billing, auto-renewal, or linked credit cards to charge.

### 2. Can I use the same anonymous token on my phone and computer at the same time?

Yes. Anonymous tokens (**JWT RSA**) are self-contained data vouchers. you can connect multiple devices using the exact same anonymous token string simultaneously.

### 3. How do I back up my anonymous token safely?

Since anonymous tokens are completely unrecoverable if lost, you must safeguard them like physical currency:

- **Encrypted Notes/Vaults:** Copy and paste your token string into a secure, password-protected password manager or an encrypted digital vault file on your hardware device.
- **Avoid Plaintext:** Do not store token strings in unencrypted text files, emails, or public messaging apps where malware or third parties could intercept them.
- **Remember:** If you delete the client app without backing up your token string elsewhere, your balance is permanently gone. Sail support cannot retrieve it.

### 4. Why does my web browser occasionally show a normal website when I try to connect?

If your client app attempts to connect using a corrupted, expired, or invalid token string, the server invokes the **Web Disguise Layer**. Instead of opening a proxy tunnel, it routes the connection to a normal, innocent public HTTPS landing page. If this happens, open your client app, verify your token string is pasted correctly, check your voucher balance, and try again.

### 5. Does Sail work for peer-to-peer (P2P) connections or heavy downloading?

Yes. The **Troad** protocol is optimized for high-volume, low-latency data transit. It handles standard web traffic, specialized peer-to-peer protocols, and crypto exchange network pipelines smoothly across all server nodes.

### 6. Android apk package installation failed

An Android APK installation failure is typically caused by insufficient storage, permission blocks, or conflicts with an existing app version

Here are the most effective ways to fix the "App Not Installed" or package failure error:

#### Enable "Install Unknown Apps" Permissions

Android blocks installations from outside the Google Play Store by default. You must give permission to the specific app (like Chrome or your File Manager) that you are using to open the APK.
Open your device Settings.
Go to Apps &gt; Special app access (sometimes under Advanced or Privacy).
Tap Install unknown apps.
Select the app you are using (e.g., Chrome or My Files) and toggle Allow from this source to ON.

#### Check for App Version or Signature Mismatches

If you already have a version of this app on your phone, the new installation will fail if the signatures don't match or if you are trying to downgrade the version.
Uninstall the existing app: Fully delete any older or official versions of the app from your phone before trying to install the new APK.
Check hidden users: If you have a Guest profile or Secure Folder, make sure the app is uninstalled there as well.

#### Temporarily Turn Off Google Play Protect

Google Play Protect will occasionally block unverified APK files for security.
Open the Google Play Store.
Tap your profile icon in the top-right corner.
Select Play Protect and then tap the Settings (gear) icon.
Turn off Scan apps with Play Protect. Remember to turn this back on after installing the app.

#### Clear the Package Installer Cache

The system application responsible for installing apps may have glitched.
Go to Settings &gt; Apps &gt; See all apps.
Tap the three dots (menu icon) in the top right and select Show system.
Search for Package Installer, tap it, and go to Storage & cache.
Tap Clear Cache.

#### Check File Integrity and Compatibility

Free up space: Android generally requires at least 10–15% of your internal storage to be free to successfully unpack and install a new application.
Corrupted download: The APK file might be incomplete. Try downloading it again over a stable Wi-Fi connection, preferably from a reputable source like APKMirror .
Incompatible hardware: The APK might be built for a different processor architecture (e.g., a 64-bit app trying to install on an older 32-bit phone) or requires a newer version of Android than your device has.
