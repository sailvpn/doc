# SailX Product Guide & Configuration Manual

---

## 1. What is SailX?

**SailX** is an anonymous, prepaid VPN service built on a strict privacy-first model.

---

## 2. How SailX Works

SailX can be configured to operate in two distinct modes: **Anonymous Mode** and **Registered Mode**. Users can switch between these modes at any time, but each mode requires a different type of token.

### Mode Configuration Matrix

| Feature / Parameter         | Anonymous Mode                   | Registered Mode                |
| :-------------------------- | :------------------------------- | :----------------------------- |
| **Desktop Parameter**       | `params.crypto=JWT2`             | `params.crypto=JWT`            |
| **Android App Auth Method** | `JWT2`                           | `JWT`                          |
| **Token Type**              | JWT RSA (Self-contained voucher) | JWT SHA256 (Linked to account) |
| **Account Required**        | No                               | Yes                            |

---

### Anonymous Mode

In Anonymous Mode, you do not need to create an account. Instead, you purchase a **JWT RSA token** that contains a one-time random ID and a specific data quota. You load this token directly into your VPN client to start using the service. The serving VPN proxy node has absolutely zero knowledge of your identity.

#### Purchase & Setup Process

1. **Select a Package:** Visit [SailX Offers](https://sailsecuretech.com/offer) to view available packages and pricing.
2. **Payment:** Click **Buy Anonymous Pass** to be redirected to the secure Stripe checkout page to enter your card or wallet information.
3. **Token Retrieval:** After a successful payment, you will be redirected to [SailX Stripe Confirmation](https://sailsecuretech.com/stripe), where your unique JWT RSA token will be generated.

> ⚠️ **CRITICAL WARNING:** The token is generated and displayed **ONLY ONCE**. If you do not save or copy it immediately, it is lost forever. The system does not store your tokens.

4. **Installation:** Download the client software package from [SailX Downloads](https://sailsecuretech.com/download). Unzip or install the package.
5. **Configuration:** Configure the client using your saved token and the VPN proxy node details found at [SailX Nodes](https://sailsecuretech.com/nodes).

_For detailed instructions, refer to the `README` file inside the downloaded package, visit [SailX Documentation](https://sailsecuretech.com/docs), or contact support at [SailX Support](https://sailsecuretech.com/support)._

#### Checking Balance

You can verify your token's remaining data balance at any time by entering or uploading your token at [SailX Token Checker](https://sailsecuretech.comcheck-token) and clicking **Check**.

---

### Registered Mode

In Registered Mode, you create and log into an account with the VPN service. Purchased data packages are added directly to your profile balance. You then generate a **JWT SHA256 token**, which contains a temporary random ID linked to your account and an expiration date, and load it into your client.

#### Purchase & Setup Process

1. **Refill Balance:** Go to [SailX Refill](https://sailsecuretech.com/refill) to view available packages and prices.
2. **Payment:** Click **Add to Profile Balance** for your chosen package to proceed to Stripe checkout.
3. **Confirmation:** Once payment is complete, you will be redirected back to [SailX Stripe Confirmation](https://sailsecuretech.com/stripe). The platform automatically detects your registered status, displays a success message, and adds the data quota to your account profile.
4. **Token Generation:** Visit [SailX Token Generation](https://sailsecuretech.com/token) to generate your custom JWT SHA256 token. You can also generate a token by your username/password in your Android apps, and sahe it with your other devices
5. **Installation:** Download the client software package from [SailX Downloads](https://sailsecuretech.com/download). Unzip or install the package.
6. **Configuration:** Configure the client using your saved token and the VPN proxy node details found at [SailX Nodes](https://sailsecuretech.com/nodes).

_For detailed instructions, refer to the `README` file inside the downloaded package, visit [SailX Documentation](https://sailsecuretech.com/docs), or contact support at [SailX Support](https://sailsecuretech.com/support)._

---

## 3. Operating System Proxy Configuration

SailX runs **simultaneous proxy listeners** for both **HTTP/HTTPS** and **SOCKS5**. Users can configure and use both protocols at the same time depending on their specific application requirements.

> 📌 **FTP Note:** FTP workloads are fully supported and handled natively by the SOCKS5 protocol via its built-in **UDP Relay** feature.

### Windows Configuration

#### Via Graphical Settings (For HTTP/HTTPS Apps)

1. Press `Windows Key + I` to open **Settings**.
2. Select **Network & internet** (Windows 11) or **Network & Internet** (Windows 10).
3. Click on the **Proxy** option.
4. Locate the **Manual proxy setup** section and click **Set up** (or toggle **Use a proxy server** to **ON**).
5. Input your SailX node **HTTP/HTTPS IP address** and **Port**, then click **Save**.

#### Via Windows Legacy Internet Properties (For Concurrent HTTP & SOCKS5 Setup)

1. Press `Windows Key + R`, type `inetcpl.cpl`, and press **Enter**.
2. Go to the **Connections** tab and click **LAN settings**.
3. Check **Use a proxy server for your LAN** and click **Advanced**.
4. To route traffic natively, enter your SailX **HTTP** and **Secure (HTTPS)** parameters in their designated fields.
5. To simultaneously activate SOCKS5 (enabling FTP UDP relay support), enter your SOCKS5 server node IP and port in the **Socks** text box.

---

### Linux Configuration

#### Environment Variables (Session-specific CLI)

For standard terminal workloads, you can choose to define your protocols individually or combine them in your shell session profile (`~/.bashrc` or `~/.zshrc`).

- **For Apps that Require HTTP / HTTPS Proxies:**
  ```bash
  export http_proxy="http://ipaddress:port"
  export https_proxy="http://ipaddress:port"
  ```
- **For Apps that Require SOCKS5 & FTP Traffic (Utilizing SOCKS5 UDP Relay):**
  `bash
export all_proxy="socks5://ipaddress:port"
`
  _To clear these variables, run: `unset http_proxy https_proxy all_proxy`_

#### System-wide Configuration (Debian/Ubuntu Server)

To enforce proxy protocols across background daemons, append the parameters directly to your environment defaults:

1. Open `/etc/environment` using a terminal text editor with `sudo` privileges.
2. Add the concurrent configuration strings:
   ```text
   http_proxy="http://ipaddress:port/"
   https_proxy="http://ipaddress:port/"
   all_proxy="socks5://ipaddress:port/"
   ```
3. Save the modifications and apply changes instantly by running: `source /etc/environment`

---

## 4. Data & Privacy Policies

- **Prepaid Data Features:** In both modes, purchases are done as one-time prepaid data packages. The data package never expires and remains active as long as there is a positive balance.
- **Absolute Privacy & Decoupling:** In both modes, user card information and purchasing details are deliberately decoupled from the VPN service. The VPN system does not hold any information about users' cards or purchasing activities. It is technically impossible to establish a 1-to-1 correspondence between a user's card/purchasing data and a JWT RSA token or registered account.

# SailX Frequently Asked Questions & Troubleshooting

---

## 1. General & Account Questions

#### What is the difference between Anonymous Mode and Registered Mode?

- **Anonymous Mode** requires no account creation or login. You simply buy a JWT RSA token, load it into your client, and connect. The system holds zero knowledge of your identity.
- **Registered Mode** requires you to register and log in. Data purchases are added directly to your account profile balance, and you generate your own JWT SHA256 tokens linked temporarily to your profile.

#### Do my purchased data packages expire?

- **No.** In both modes, data packages are one-time prepaid purchases. Your data balance will never expire and remains active as long as your balance is above zero.

#### Is my payment history linked to my VPN activity?

- **No.** Card processing and purchasing data are completely decoupled from the core VPN routing service. The system does not store card information, making it technically impossible to link a specific payment method or transaction history to a specific JWT token or account.

---

## 2. Token & Session Management

#### What happens when my JWT RSA token runs out of data or expires?

- Once your token hits its data quota limit (gigabytes consumed), the secure connection tunnel will close automatically.
- To resume service under Anonymous Mode, you must purchase a brand-new token string and configure it as a new profile in your client app.
- Because user privacy is our first priority, there is no automatic billing, auto-renewal, or linked credit cards to charge.

#### Can I use the same anonymous token on my phone and computer at the same time?

- **Yes.** Anonymous tokens (JWT RSA) are self-contained data vouchers. You can connect multiple devices using the exact same anonymous token string simultaneously.

#### Can I use the same JWT SHA token on my phone and computer at the same time?

- **Yes.** You can connect multiple devices using the exact same token string simultaneously.

#### How do I back up my anonymous token safely?

Since anonymous tokens are completely unrecoverable if lost, you must safeguard them like physical currency:

- **Encrypted Notes/Vaults:** Copy and paste your token string into a secure, password-protected password manager or an encrypted digital vault file on your hardware device.
- **Avoid Plaintext:** Do not store token strings in unencrypted text files, emails, or public messaging apps where malware or third parties could intercept them.
- **Remember:** If you delete the client app without backing up your token string elsewhere, your balance is permanently gone. SailX support cannot retrieve it.

---

## 3. Connection & Application Troubleshooting

#### Why does my web browser occasionally show a normal website when I try to connect?

- If your client app attempts to connect using a corrupted, expired, or invalid token string, the server invokes the **Web Disguise Layer**. Instead of opening a proxy tunnel, it routes the connection to a normal, public HTTPS landing page.
- If this happens, open your client app, verify your token string is pasted correctly, check your voucher balance, and try again.

#### Does SailX work for peer-to-peer (P2P) connections or heavy downloading?

- **Yes.** The underlying **Troad** protocol is optimized for high-volume, low-latency data transit. It handles standard web traffic, specialized peer-to-peer protocols, and crypto exchange network pipelines smoothly across all server nodes.

#### How do I configure apps that only support specific proxy protocols?

Because SailX serves both **HTTP/HTTPS** and **SOCKS5** protocol channels simultaneously, you can customize your application-level settings:

- **Web Browsers (Chrome, Edge, Firefox):** Most modern browsers use the operating system's built-in network settings, mapping automatically to the SailX HTTP/HTTPS interface.
- **Developer Tools & Scripts (`curl`, `wget`, `npm`):** These platforms read system environment parameters natively and should be mapped using your SailX HTTP or HTTPS configuration.
- **Instant Messengers & FTP Clients (Telegram, FileZilla):** For apps that handle continuous data pipelines or legacy protocols like FTP, bypass HTTP entirely and select **SOCKS5** within the app's connection menu to exploit the **UDP Relay** feature.

---

## 4. Android Installation Troubleshooting

#### How do I fix an Android APK package installation failure?

An Android APK installation failure ("App Not Installed") is typically caused by insufficient storage, permission blocks, or conflicts with an existing app version. Follow these sequential triage steps to resolve it:

##### Step 1: Enable "Install Unknown Apps" Permissions

Android blocks installations from outside the Google Play Store by default. You must grant permission to the specific app (like Chrome or your File Manager) that you are using to open the APK:

1. Open your device **Settings**.
2. Go to **Apps** > **Special app access** (sometimes found under _Advanced_ or _Privacy_).
3. Tap **Install unknown apps**.
4. Select the application you are using to open the file (e.g., Chrome or Files) and toggle **Allow from this source** to **ON**.

##### Step 2: Check for App Version or Signature Mismatches

If you already have a version of this app on your phone, the new installation will fail if the signatures do not match or if you are attempting to downgrade the version.

- **Uninstall the existing app:** Fully delete any older or official versions of the app from your phone before trying to install the new APK.
- **Check hidden users:** If your device utilizes a _Guest Profile_ or _Secure Folder_, ensure the app is fully uninstalled from those environments as well.

##### Step 3: Temporarily Turn Off Google Play Protect

Google Play Protect may occasionally block unverified APK files for security reasons.

1. Open the **Google Play Store**.
2. Tap your profile icon in the top-right corner.
3. Select **Play Protect**, then tap the **Settings (gear)** icon.
4. Toggle **Scan apps with Play Protect** to **OFF**. _(Note: Remember to turn this back on after the installation is complete)._

##### Step 4: Clear the Package Installer Cache

The system application responsible for installing apps may have encountered a temporary glitch.

1. Go to **Settings** > **Apps** > **See all apps**.
2. Tap the three dots (menu icon) in the top right and select **Show system**.
3. Search for **Package Installer**, tap it, and go to **Storage & cache**.
4. Tap **Clear Cache**.

##### Step 5: Check File Integrity and Device Compatibility

- **Free up space:** Android generally requires at least 10–15% of your internal storage to be completely free to successfully unpack and install a new application.
- **Corrupted download:** The APK file might be incomplete. Try downloading it again over a stable Wi-Fi connection.
- **Incompatible hardware:** The APK might be built for a different processor architecture (e.g., a 64-bit app trying to install on an older 32-bit phone) or may require a newer version of the Android OS than your device currently runs.
