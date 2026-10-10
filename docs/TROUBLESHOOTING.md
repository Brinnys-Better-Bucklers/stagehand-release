# Troubleshoot Stagehand

[Back to downloads](../README.md) · [Windows](INSTALL_WINDOWS.md) · [macOS](INSTALL_MACOS.md) · [Updates and backups](UPDATING.md)

## No download, missing asset, or GitHub 404

- Open the [public release list](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases).
  A latest-release link may not resolve before a stable release is published.
- Expand **Assets**. Look for a Windows setup `.exe` or the `.dmg` for your Mac's
  processor. The source-code archives do not contain an installable app.
- A private internal release is not a public download. If a link asks for access
  to the private application repository, report it and use this repository's
  release list instead.
- If the required installer is missing, report the release version and your
  computer type. Download another compatible public release only after checking
  its release notes.

## Verify a download

If the release publishes `SHA256SUMS.txt` or a SHA-256 digest for your exact
installer, calculate its hash and compare all characters with that entry.
Replace the example filename below with the file you downloaded.

Windows PowerShell:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath "$env:USERPROFILE\Downloads\Stagehand_VERSION_x64-setup.exe"
```

macOS Terminal:

```bash
shasum -a 256 "$HOME/Downloads/Stagehand_VERSION_aarch64.dmg"
```

A matching digest confirms that the download matches the published file; it
does not replace code signing or establish the publisher's identity. If the
hash differs, discard that download and download again from the official release
page. If it still differs, report the mismatch and do not open the installer.
Without a published digest, calculating a hash alone cannot verify the download.

## Windows setup fails or the app shows a blank window

1. Confirm that you downloaded the Windows x64 installer for an x64 Windows PC.
2. Close Stagehand, restart Windows, and retry the installer.
3. If the message names WebView2, install or repair the **Evergreen WebView2
   Runtime** using [Microsoft's download page](https://developer.microsoft.com/en-us/microsoft-edge/webview2/).
   Its standalone installer supports offline installation. Stagehand setup
   normally includes this runtime when needed.
4. Reinstall the same Stagehand version if bundled application files are missing.
5. For SmartScreen prompts, use the [Windows guide](INSTALL_WINDOWS.md#4-if-windows-shows-a-security-prompt).

If a policy or antivirus product blocks a required file, keep the exact message
and contact the maintainers or your IT administrator. Do not disable protection
or download replacement executables from unofficial sources.

## macOS says the app is damaged or blocked

1. Confirm that the `.dmg` matches your Mac's processor.
2. Download it again from the official public release and compare the checksum
   if one is provided.
3. Quit Stagehand and copy the complete app into Applications again. Eject the
   disk image and launch the installed copy.
4. For an unidentified-developer prompt, follow the
   [macOS first-launch steps](INSTALL_MACOS.md#4-if-macos-blocks-the-first-launch).
5. If the app is still reported as damaged, malware, or incompatible, stop and
   report the exact text, your macOS version, and the installer filename.

A damaged-app message needs investigation; do not treat every security message
as a normal first-launch warning. See
[Apple's guidance](https://support.apple.com/en-us/102445) for the different alerts.

## Stagehand opens but cannot load data

1. Allow startup initialization to finish. If an error appears, record its exact
   wording and the Stagehand version.
2. Quit all Stagehand instances and restart the computer, then open one instance.
   Stagehand starts its bundled local database automatically; no separate
   SurrealDB installation is needed for standard public builds.
3. Check that your disk has free space and that the current OS account can write
   to the [application data folders](UPDATING.md#back-up-the-installed-apps-data).
4. If you previously configured an external database or custom folders, confirm
   that those locations are available. Stagehand's default local database uses
   port `8000`; another database or service using that port can interfere.
5. If required bundled files are missing, reinstall the same app version.

If new notes disappear after quitting and reopening, avoid adding important
content and report the persistence failure. Preserve the data folders. Do not
delete the database or reset application data as an initial troubleshooting step.

## An update opens the wrong version or appears to lose campaigns

- Check the version in the title bar. On Mac, launch the copy in Applications,
  rather than a copy in Downloads or a mounted disk image.
- Confirm that you are using the same OS user account and active data locations
  as before the update.
- Keep the pre-update backup and make a separate copy of the current data before
  trying recovery. Follow the [recovery guide](UPDATING.md#recover-from-a-failed-update).
- Do not repeatedly install older versions against the current database or merge
  old backup files into it. A newer app may have migrated the database.

## Report a problem

Search [existing issues](https://github.com/Brinnys-Better-Bucklers/stagehand-release/issues),
then [open an issue](https://github.com/Brinnys-Better-Bucklers/stagehand-release/issues/new)
with:

- Stagehand version, and the previous version if the problem followed an update.
- Windows or macOS version and whether the processor is x64 or Apple Silicon.
- Installer filename and the public release page it came from.
- Whether this is a fresh installation, an update, or a move from an internal build.
- Steps to reproduce, expected behavior, and actual behavior.
- Exact error text and a screenshot if useful.
- Whether you use default local storage or a custom database/data location.

Remove personal information, credentials, campaign details, and private source
references from anything you share. Do not attach database folders or backups
to a public issue.
