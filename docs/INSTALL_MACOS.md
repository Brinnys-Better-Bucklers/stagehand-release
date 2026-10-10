# Install Stagehand on macOS

[Back to downloads](../README.md) · [Update an existing installation](UPDATING.md)

## 1. Choose the right Mac build

Open **Apple menu → About This Mac** and check your chip or processor:

| About This Mac shows | Choose this release asset |
| --- | --- |
| **Chip: Apple M…** | Apple Silicon `.dmg`, labelled `aarch64` or `arm64` |
| **Processor: Intel…** | Intel `.dmg`, labelled `x64` or `x86_64` |

Use the native Apple Silicon download on an M-series Mac. The two downloads
are separate builds, not a universal app. An Apple Silicon build cannot run on
an Intel Mac.

Check the release notes for the macOS versions supported by that particular
build. Leave enough free space for the download, the installed app, and your
campaigns and attachments. Downloading the release needs an internet connection;
normal local workspace use is designed to work offline.

If Stagehand is already installed, follow the [update guide](UPDATING.md) first
to back up your data.

## 2. Download the disk image

1. Open the [latest public release](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases/latest).
2. Read the release notes, including compatibility information and known issues.
3. Expand **Assets** and download the `.dmg` matching your Mac's processor.
4. If the release provides checksums, you can
   [verify the download](TROUBLESHOOTING.md#verify-a-download) before opening it.

The automatically generated **Source code** archives are not Mac installers.

## 3. Install in Applications

1. Quit Stagehand if it is running. Use **Command-Q** or **Stagehand → Quit**;
   closing a window alone may leave the application running.
2. Double-click the downloaded `.dmg` to mount it.
3. Drag **Stagehand.app** to the **Applications** folder. If the disk image
   does not show an Applications shortcut, open Applications in another Finder
   window and drag the app there.
4. For an update, choose **Replace** when Finder asks about the existing app.
   If macOS asks for permission to write to Applications, authenticate with an
   account that has that permission.
5. Wait for the copy to finish, then eject the Stagehand disk image in Finder.
6. Open **Applications → Stagehand**.

Run the installed copy from Applications. Do not keep running the app inside
the mounted disk image or copy only the executable out of the `.app` bundle.
The bundle includes the local database executable and other required files.
You do not need Homebrew, Xcode, or a separate database installation.

## 4. If macOS blocks the first launch

macOS may ask you to confirm opening an app downloaded from the internet. If
you obtained it from this repository's release page and trust the download,
confirm **Open**.

For an **unidentified developer** or **cannot verify the developer** message,
check the release's signing and notarization information. If you trust the
specific download and choose to make an exception:

1. Try opening the installed app once, then dismiss the blocked-launch message.
2. Open **System Settings → Privacy & Security**.
3. Find the message about Stagehand and choose **Open Anyway**, when available.
4. Authenticate if requested and confirm **Open**.

On older macOS versions, the equivalent controls are in **System Preferences →
Security & Privacy → General**. Follow Apple's
[instructions for opening downloaded apps](https://support.apple.com/en-us/102445).

If macOS says the app **will damage your computer**, reports malware, or says
it is **damaged**, stop and check the
[troubleshooting guide](TROUBLESHOOTING.md#macos-says-the-app-is-damaged-or-blocked).
Do not disable Gatekeeper or remove quarantine attributes as a routine install
step. Managed Macs may require help from an IT administrator.

## 5. Check the first launch

1. Wait for the main window and database initialization to finish.
2. Check the version in the title bar against the release you downloaded.
3. Create a small test campaign or workspace and add a note.
4. Quit with **Command-Q**, reopen Stagehand from Applications, and confirm the
   test content is still there. If you use attachments, also check that an
   attachment opens after restarting.

If initialization fails or changes disappear after a restart, use the
[startup and data troubleshooting steps](TROUBLESHOOTING.md#stagehand-opens-but-cannot-load-data)
before adding important campaign content.

## Where your data lives

The default application data folder is:

```text
~/Library/Application Support/com.stagehand.stagehand-platform
```

It contains the database at `surreal/stagehand.db` and attachments under
`attachments`. In Finder, choose **Go → Go to Folder…** (**Shift-Command-G**) and
paste the path above. This folder is separate from `Stagehand.app` in
Applications. See the [macOS backup steps](UPDATING.md#macos-backup).

## Uninstall Stagehand

1. Back up your data if you may want it later.
2. Quit Stagehand with **Command-Q**.
3. Move **Stagehand.app** from Applications to the Trash.

Keep the application data folder if you plan to reinstall or recover campaigns.
Replacing or removing the application bundle is separate from removing your data.
