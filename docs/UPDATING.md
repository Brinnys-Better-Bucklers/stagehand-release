# Update Stagehand and protect your data

[Back to downloads](../README.md) · [Windows install](INSTALL_WINDOWS.md) · [macOS install](INSTALL_MACOS.md)

Stagehand currently uses **manual updates**. Download a newer installer from
this repository's public releases and install it over the existing application.
There is no built-in automatic updater or required “Check for Updates” button.

## Before every update

1. Note the current version from Stagehand's title bar and keep the installer
   for that version if you have it.
2. Read the target release's notes for supported OS versions, known issues,
   migration steps, and any required intermediate versions.
3. Finish your work and fully quit Stagehand. On Mac, use **Command-Q**. On
   Windows, close all Stagehand windows and confirm the app has exited.
4. Create a backup using the steps below. Wait for the copy to finish and verify
   that the backup contains the expected folders and files.
5. Download the new installer for the same operating system and processor type.

The app can apply database migrations on startup. Keep the backup from
**before the first launch of the new version**, even if the update appears to
work. An older version may not understand a migrated database.

## Back up the installed app's data

These steps cover the default, locally managed database. Make the copy only
after Stagehand and its managed database have stopped. If the bundled
`surreal`/`surreal.exe` process associated with Stagehand remains after quitting,
restart the computer and make the backup before opening Stagehand again.
Do not copy a database directory while it is being written to.

Copy the **whole application data folder**, including the complete
`surreal/stagehand.db` directory. Despite its name, `stagehand.db` is a directory;
copying one file from inside it is not a database backup. Include attachments
and other app files as described below.

Save backups outside the application and its data folders, for example in a
dated folder on another drive. Name the folder with the app version and date,
such as `Stagehand-backup-v0.2.0-2026-10-10`. This is an example name, not a
required version. Keep backups private: they contain your campaign content.

### Windows backup

Windows stores the database and attachments in different locations. Back up
both parent folders under the same Windows account used to run Stagehand.

| Paste into File Explorer's address bar | Save in your backup as |
| --- | --- |
| `%APPDATA%\com.stagehand.stagehand-platform` | `Roaming\com.stagehand.stagehand-platform` |
| `%LOCALAPPDATA%\com.stagehand.stagehand-platform` | `Local\com.stagehand.stagehand-platform` |

1. Create your dated backup folder, with separate `Roaming` and `Local` folders
   inside it. This avoids mixing two folders with the same name.
2. Open `%APPDATA%` in File Explorer. Copy the whole
   `com.stagehand.stagehand-platform` folder into your backup's `Roaming` folder.
3. Open `%LOCALAPPDATA%` and copy the whole
   `com.stagehand.stagehand-platform` folder into your backup's `Local` folder,
   if it exists.
4. Verify that the Roaming copy includes `surreal\stagehand.db` and that the
   Local copy includes `attachments` if you have uploaded attachments.

A missing Local folder may be normal before the app creates local files. If you
have used Stagehand but cannot find the database, check
[custom data locations](#custom-data-locations) before proceeding.

### macOS backup

1. In Finder, choose **Go → Go to Folder…** (**Shift-Command-G**).
2. Enter `~/Library/Application Support`.
3. Copy the entire `com.stagehand.stagehand-platform` folder into your dated
   backup folder.
4. Verify that the copy includes `surreal/stagehand.db` and `attachments` if you
   have uploaded attachments.

If you have used Stagehand but cannot find the database, check custom locations
before proceeding.

### Custom data locations

If you or an administrator configured `SURREALDB_DATA_DIR` or
`STAGEHAND_ATTACHMENTS_DIR`, also back up those actual locations. Defaults may
not contain your active data. An externally managed database needs its own
consistent database backup; copying the default local folder does not back it up.

These file copies are for restoring the same installation and compatible app
version. They are not a documented cross-platform migration or a substitute
for a database export when changing database versions.

## Update on Windows

1. Complete the backup above and keep Stagehand closed.
2. Download the new **Windows x64 setup `.exe`** from
   [public releases](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases).
3. Run setup under the same Windows account as before.
4. Keep the existing installation location and follow setup's upgrade prompts.
5. Finish setup and launch Stagehand.

A routine update should not need an uninstall first. If setup explicitly
requires removing an older installation, verify the backup first and keep any
option to delete user data **unchecked**. If setup reports that Stagehand is
still running, exit the app or restart Windows, then retry.

See [Windows installation](INSTALL_WINDOWS.md) for SmartScreen and WebView2 help.

## Update on macOS

1. Complete the backup above and quit Stagehand with **Command-Q**.
2. Download the new `.dmg` for your Mac's processor from
   [public releases](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases).
3. Open the disk image and drag **Stagehand.app** into the same Applications
   folder used by your existing installation.
4. Choose **Replace** and wait for the copy to finish.
5. Eject the disk image, then open Stagehand from Applications.

If Finder says the app is in use, quit it fully or restart the Mac before
retrying. See [macOS installation](INSTALL_MACOS.md) for first-launch prompts.

## Verify the update

1. Check the version in the title bar against the version you installed.
2. Allow startup initialization and any migrations to finish.
3. Open an existing campaign or workspace. Check notes, layouts, and attachments
   that matter to you.
4. Make a small test change, quit the app, reopen it, and confirm the change was
   saved and the existing content is still available.
5. Keep the pre-update backup until you are satisfied the new version works.

An ordinary update is intended to retain data in the app-data folders. A backup
is still necessary because migrations, failed writes, or an incompatible build
can affect that data. If something is wrong, avoid further changes and follow
[troubleshooting](TROUBLESHOOTING.md).

## Move from an internal build to a public build

Public distribution does not automatically mean a different application or
data folder. The current application identifier is
`com.stagehand.stagehand-platform`; builds using that identifier can access
the same local data under the same OS account.

1. Back up the internal installation's active database, attachments, and other
   app-data files before opening the public build.
2. Compare application versions, not just release tag names. An internal tag
   such as `v_0_2_0` can represent app version `0.2.0`.
3. Check the public release notes for compatibility with the internal build.
   Do not assume a public build is newer than an internal build.
4. If compatibility is confirmed, follow the normal update steps. Do not run
   the internal and public app against the same database simultaneously.

If the internal version is newer, or its data path or identifier differs, ask
the maintainers for a migration path before switching. A public download does
not automatically move a separately configured internal database.

## Recover from a failed update

First report the problem with the old and new versions and the exact error.
Keep the pre-update backup and the current data unchanged while investigating.

Reinstalling the **same version** can repair missing application files. It does
not reverse a database migration. Do not point an older app at data already
opened by a newer version unless the release notes explicitly allow it.

If maintainers confirm that restoring your pre-update backup is appropriate:

1. Fully quit Stagehand and ensure its database process has stopped.
2. Make a separate copy of the current data, even if it appears broken. It may
   contain work created after the update.
3. Obtain the matching application version from public releases. Windows setup
   currently blocks normal downgrades; an older version may require uninstalling
   the newer app first while preserving user data. Use maintainer guidance for
   the affected versions.
4. With the app closed, move the current app-data folders to a separate recovery
   location. Restore the backup folders to their original locations. On Windows,
   restore both the Roaming and Local copies. On Mac, restore the Application
   Support copy. Restore configured custom locations as well, if applicable.
5. **Replace the complete folders; do not merge old and new database files.**
   Restore the database and attachments from the same backup.
6. Launch only the matching app version and verify your campaigns and attachments.

Restoring a backup returns to the content at the time it was made. Changes made
afterward are not automatically recovered. Keep the separate copy of newer data
until the recovery is resolved.
