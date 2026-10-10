# Stagehand — Public Downloads

Stagehand is an offline-first workspace for tabletop role-playing games, with
campaigns, notes, events, and widgets.

This repository distributes **public Stagehand desktop builds** and installation
guides. The application source code and internal development releases remain in
the private `stagehand_platform` repository. You do not need access to that
repository to download or install a public build.

## Download Stagehand

**[Download the latest public release](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases/latest)**

For earlier versions or preview builds, visit
[all public releases](https://github.com/Brinnys-Better-Bucklers/stagehand-release/releases).
Read the selected release's notes for supported operating system versions,
known issues, and any special installation or migration steps.

Expand **Assets** on the release page and choose the installer for your computer:

| Computer | Download | Installation guide |
| --- | --- | --- |
| Windows, Intel or AMD 64-bit | Windows `x64` setup file ending in `.exe` | [Windows installation](docs/INSTALL_WINDOWS.md) |
| Mac with Apple Silicon (M-series chip) | `.dmg` labelled `aarch64` or `arm64` | [macOS installation](docs/INSTALL_MACOS.md) |
| Mac with an Intel processor | `.dmg` labelled `x64` or `x86_64` | [macOS installation](docs/INSTALL_MACOS.md) |

Asset names include the version and may differ between releases. There is no
single universal Mac download in the current build configuration. Native
Windows ARM64 and 32-bit Windows installers are not currently part of that
configuration; do not assume the x64 build is supported on those systems.

**Do not download GitHub's “Source code (zip)” or “Source code (tar.gz)” to
install Stagehand.** Those archives contain this distribution repository's
files, not the desktop application. If a release has no installer for your
computer, that build is not available from that release. If GitHub cannot find a
latest release, check the full release list: a stable public release may not
have been published yet.

## Install and update

- [Install on Windows](docs/INSTALL_WINDOWS.md)
- [Install on macOS](docs/INSTALL_MACOS.md)
- [Update Stagehand, back up your data, and recover an installation](docs/UPDATING.md)
- [Troubleshoot installation and startup](docs/TROUBLESHOOTING.md)

Stagehand installers bundle the required local database. You do not need to
clone a repository or install Git, Node.js, Rust, Docker, or SurrealDB separately.
Windows uses Microsoft Edge WebView2; the Windows setup includes its offline
installer when the runtime is needed.

Updates are installed manually by downloading a newer public release. Back up
your data before updating, then install over your existing installation using
the instructions above. There is currently no built-in automatic updater.

## Get help or report a problem

Search [existing issues](https://github.com/Brinnys-Better-Bucklers/stagehand-release/issues)
before [opening an issue](https://github.com/Brinnys-Better-Bucklers/stagehand-release/issues/new).
Include your Stagehand version, operating system version, processor type,
installer filename, and the steps that reproduce the problem. See the
[troubleshooting guide](docs/TROUBLESHOOTING.md#report-a-problem) for a checklist.
Public issues are visible to everyone; remove personal information and campaign
content from screenshots and logs.

## For maintainers

Use the [public release publishing guide](docs/RELEASING.md) to distribute
installers built from the private application repository. Making this repository
public does not automatically make releases in the private repository public.
