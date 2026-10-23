# SailX Desktop Application Setup Guide

This guide provides step-by-step instructions to configure, run, and automate the SailX Java application (`app.jar`) as a background service on **Windows**, **Linux**, and **macOS** environments.

---

## ☕ Step 1: Verify Java JVM Availability

Before initiating any configuration or deployment scripts, you must verify that the Java Virtual Machine (JVM) is correctly installed on your machine and accessible system-wide via your command-line interface.

### Verification Commands

Open your platform-specific terminal (Command Prompt/PowerShell on Windows, or Terminal on Linux/macOS) and execute the following command:

```bash
java -version
```

#### Expected Output

If a JVM is available, the system will return the runtime version details. Ensure your version is **Java 17 or higher** :

```text
openjdk version "17.0.8" 2023-07-18
OpenJDK Runtime Environment (build 17.0.8+7-Debian-1deb11u1)
OpenJDK 64-Bit Server VM (build 17.0.8+7-Debian-1deb11u1, mixed mode, sharing)
```

### Troubleshooting Unrecognized Commands

#### On Windows

If you receive the error message `'java' is not recognized as an internal or external command`, the runtime binary path is missing from your system variables:

1. Ensure Java is installed (look for it in `C:\Program Files\Java\`).
2. Press `Win + R`, type `sysdm.cpl`, hit **Enter**, and select the **Advanced** tab.
3. Click **Environment Variables**, find the **Path** variable under _System variables_, and click **Edit**.
4. Click **New** and paste the absolute path to your Java `bin` directory (e.g., `C:\Program Files\Java\jdk-17\bin`).
5. Re-open your command window and verify with `java -version` again.
6. **Note:** Windows background deployment via `sail.bat` also strictly requires `javaw.exe` to be present in this directory to handle windowless background processing.

#### On Linux / macOS

If `java` cannot be found, update your local software index and install the headless OpenJDK runtime package environment:

- **Ubuntu/Debian:** `sudo apt update && sudo apt install default-jre-headless`
- **RHEL/CentOS/Fedora:** `sudo dnf install java-latest-openjdk-headless`
- **macOS (via Homebrew):** `brew install openjdk`

---

## 📦 Step 2: Download and Extract the Software Package

Extract the contents of the downloaded archive file and enter its root workspace folder.

1. **Unzip the Archive:** Locate your downloaded SailX software ZIP package and extract its contents to a preferred installation folder on your local storage.
2. **Open Your Terminal:** Launch your platform's terminal application (Command Prompt/PowerShell for Windows, Terminal for Linux/macOS).
3. **Navigate to the Directory:** Use the change directory (`cd`) command to enter your newly extracted installation folder.
   ```bash
   cd /path/to/extracted/sailx-directory
   ```
4. **Context Rule:** From this point forward, the relative path syntax `./` strictly refers to this extracted application root folder directory.

---

## ⚙️ Step 3: Initialize Configuration File

The application requires an active configuration file named exactly `application.properties` located in the same directory as `app.jar`.

1. Locate the template file `application.properties.txt` in your application folder.
2. Duplicate or rename it to exactly `application.properties`.
3. Open `application.properties` in a text editor and fill in your connection data.

### Configuration Template Reference

```properties
# Remote Server Connection
params.remoteHost=your-server.com
params.remotePort=443
params.sni=your-server.com             # just set it the same as remoteHost

# Local Concurrent Proxy Listeners
params.localHost=127.0.0.1
params.localPort=1080                  # Local SOCKS5 listener (Supports FTP via UDP Relay)
params.httpPort=8080                   # Local HTTP/HTTPS listener (Blind forwarding)

# Infrastructure Assets
params.certPath=./ca.crt
params.jwtTokenFile=./token.jwt         # File where your active token string is stored
```

---

## 🔑 Step 4: Choose and Configure Your Operational Mode

Inside your `application.properties`, uncomment and populate **only one** of the three following mode blocks based on your privacy and device usage goals:

### Option A: Anonymous Mode (Highest Privacy)

_No account or credentials needed. Uses standalone data vouchers._

```properties
params.crypto=JWT2
# 1. Purchase an anonymous pass from the SailX portal.
# 2. Paste the generated JWT RSA token string directly into your './token.jwt' file.
# 3. This token remains valid on multiple concurrent devices until its quota or expiration runs out.
```

### Option B: Automatic Mode (Single User / Single Device)

_The client automatically requests, injects, and renews tokens using your credentials._

```properties
params.crypto=JWT
params.tokenMode=AUTO
params.username=your_portal_username
params.password=your_portal_secure_password
params.expireMins=60
params.renewInterval=10
```

> ⚠️ **Critical Constraint:** Setting a device to `AUTO` mode will instantly invalidate the tokens on all other devices sharing this account whenever a renewal cycle triggers.

### Option C: Manual Mode (Multi-Device / Family Sharing)

_Prevents automatic updates from disrupting other active hardware endpoints._

```properties
params.crypto=JWT
params.tokenMode=MANUAL
# 1. Log into the web portal, manually generate a token string.
# 2. Paste the payload into your local './token.jwt' file.
# 3. You must manually update this file with a new token before its expiration window closes.
```

---

## 🐧 Linux & macOS Deployment

### 1. Pre-execution Requirements

Before launching the service script, you must grant explicit executable permissions to the management script:

```bash
chmod +x sail.sh
```

### 2. Service Management Commands

Control the application state using the following target arguments:

- **Start Backend Service:** `nohup` triggers the JAR silently and writes the tracking ID to `app.pid`.
  ```bash
  ./sail.sh start
  ```
- **Check Core Status:** Verifies if the background process ID is actively mapped in memory.
  ```bash
  ./sail.sh status
  ```
- **Stop Backend Service:** Issues a graceful termination signal (`SIGTERM`). If the application remains open after 5 seconds, it forces an ungraceful shutdown (`SIGKILL`).
  ```bash
  ./sail.sh stop
  ```

### 3. Enable Automatic Persistence on Boot (Systemd Linux Only)

To hook the SailX script into the initialization pipeline without requiring an active user login session:

1. Open `sail.service` and modify the environment specific variables (`User` and `WorkingDirectory`):
   ```ini
   [Service]
   Type=forking
   User=your_system_username
   WorkingDirectory=/absolute/path/to/your/app/folder
   ExecStart=/absolute/path/to/your/app/folder/sail.sh start
   ExecStop=/absolute/path/to/your/app/folder/sail.sh stop
   Restart=on-failure
   ```
2. Move the customized unit template to the system services catalog:
   ```bash
   sudo cp sail.service /etc/systemd/system/
   ```
3. Update systemd manager configurations, authorize boot hooks, and boot the script instantly:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable sail.service
   sudo systemctl start sail.service
   ```
4. Confirm daemon execution diagnostics:
   ```bash
   sudo systemctl status sail.service
   ```

---

## 🪟 Windows Deployment

### 1. Pre-execution Requirements

Ensure your system `PATH` environmental variables point correctly to your Java installation. The automation architecture relies on `javaw.exe` to intercept visual CLI prompt window instances and host the operation invisibly.

### 2. Service Management Commands

Execute your command terminal (`cmd.exe`) directly inside the deployment directory and issue:

- **Start Backend Service:** Launches a window-title tracked process tree.
  ```cmd
  sail.bat start
  ```
- **Check Core Status:** Scans the active system `tasklist` matching the targeted background window string identifier.
  ```cmd
  sail.bat status
  ```
- **Stop Backend Service:** Triggers `taskkill` to cleanly close the runtime thread. Stubborn instances are aggressively closed via a forced termination flag (`/F`).
  ```cmd
  sail.bat stop
  ```

### 3. Enable Automatic Persistence on Boot (Task Scheduler)

To ensure the proxy backend initializes silently in the background at system startup:

1. Launch Run (`Win + R`), execute `taskschd.msc`, and choose **Create Task...** inside the right-hand panel.
2. **General Tab Configuration:**
   - Assign an identifiable name (e.g., `SailX Background Service`).
   - Toggle **Run whether user is logged on or not**.
   - Check **Run with highest privileges** to clear administrative context traps.
3. **Triggers Tab Configuration:**
   - Click _New..._ and adjust the "Begin the task" rule framework selection to **At startup**.
4. **Actions Tab Configuration:**
   - Click _New..._, choose **Start a program**.
   - Target your script destination inside the _Program/script_ file explorer picker: `C:\path\to\your\folder\sail.bat`
