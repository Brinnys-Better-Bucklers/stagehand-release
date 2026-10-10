# Install Stagehand on Windows

[Back to downloads](../README.md) · [Update an existing installation](UPDATING.md)

## 1. Check your computer

You need a Windows PC with an Intel or AMD 64-bit processor and an operating
system version supported by the selected release. Check the release notes for
the tested Windows versions and any additional requirements.

Open **Settings → System → About**, then look under **System type**. Choose the
Windows `x64` installer for an **x64-based processor** with a **64-bit operating
system**. A 32-bit system or an ARM-based processor is not the same target.

Allow space for the installer, the application, the WebView2 runtime if needed,
and your campaign data and attachments. Downloading the release needs an
internet connection; normal local workspace use is designed to work offline.

If Stagehand is already installed, follow the [update guide](UPDATING.md) first
to back up your data.

## 2. Download the installer

1. Open the [latest public release](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases/latest).
2. Read its release notes, including known issues and compatibility information.
3. Expand **Assets** and download the **Windows x64 setup `.exe`**. Its name
   normally includes `Stagehand`, the version, `x64`, and `setup`.
4. Save it somewhere easy to find, such as **Downloads**. If the release provides
   checksums, you can [verify the download](TROUBLESHOOTING.md#verify-a-download)
   before opening it.

Use the public repository above as the download source. The automatically
generated source-code archives are not installers.

## 3. Run setup

1. Close any running Stagehand windows.
2. Double-click the downloaded setup `.exe` in File Explorer.
3. Follow the setup prompts. Keep the default destination unless you have a
   reason to change it. For updates, use the existing destination.
4. Let setup finish installing Stagehand and any required WebView2 runtime.
5. Launch **Stagehand** from the Start menu or the shortcut created by setup.

The current setup installs Stagehand for the signed-in Windows user. Install
and update under the same Windows account you use to run the app. Windows or
your organization's policies may request additional permission for runtime
installation.

The local database is included with Stagehand and starts with the app. Do not
move `Stagehand.exe` out of its installed folder: it needs the bundled files
beside it.

## 4. If Windows shows a security prompt

A new or unsigned build may show **“Windows protected your PC”** because
Microsoft Defender SmartScreen has not established its reputation. Confirm
that the installer came from this repository's release page and check the
release's signing information. If you trust that specific download, choose
**More info → Run anyway**, when offered. A warning may appear again for a new
version. Microsoft explains this behavior in its
[SmartScreen documentation](https://learn.microsoft.com/en-us/windows/apps/package-and-deploy/smartscreen-reputation).

If Windows identifies the file as malware, or policy blocks it without a
**Run anyway** option, stop and report the exact message or contact your IT
administrator. Smart App Control or managed-device policies may block unsigned
apps. Do not turn off Windows security features to install Stagehand.

## 5. Check the first launch

1. Wait for the main window and database initialization to finish.
2. Check the version displayed in the title bar against the release you downloaded.
3. Create a small test campaign or workspace and add a note.
4. Fully exit Stagehand, reopen it, and confirm that the test content is still
   there. If you use attachments, also check that an attachment opens after
   restarting.

You are ready to use Stagehand when it starts normally and your test content
survives a restart. If initialization fails or data disappears, see
[startup and data troubleshooting](TROUBLESHOOTING.md#stagehand-opens-but-cannot-load-data).

## Where your data lives

The default database is under:

```text
%APPDATA%\com.stagehand.stagehand-platform\surreal\stagehand.db
```

Attachments are stored separately under:

```text
%LOCALAPPDATA%\com.stagehand.stagehand-platform\attachments
```

Paste either parent folder into File Explorer's address bar to open it. These
folders are separate from the installed application. Back up **both** application
data folders; see [Windows backup steps](UPDATING.md#windows-backup).

## Uninstall Stagehand

1. Back up your data if you may want it later.
2. Exit Stagehand.
3. Open **Settings → Apps → Installed apps** on Windows 11, or **Apps & features**
   on Windows 10, find **Stagehand**, and choose **Uninstall**.
4. If the uninstaller offers to remove user data, leave that option unchecked
   unless you intend to erase it and have verified your backup.

Do not manually remove the app-data folders during a normal update. For a
reinstallation, install the appropriate public build again and verify your data.
