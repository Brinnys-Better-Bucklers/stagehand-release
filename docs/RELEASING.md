# Publish a public Stagehand release

[Back to public downloads](../README.md)

This guide is for maintainers. Build Stagehand in the private application
repository, then publish approved installers here. Public users should only
need this repository's release pages and documentation.

## Distribution boundary

- `stagehand_platform` holds private source code, build workflows, and internal
  releases.
- `stagehand-release` holds public documentation and public release assets.
- A release in the private repository stays private. This repository does not
  mirror it automatically.

The existing desktop workflow in the private repository publishes a GitHub
Release in that same repository. These documentation changes do not redirect
that workflow or configure automatic publication.

## Publish an existing internal build manually

1. Select the approved internal release. Confirm its app version, source commit,
   supported OS versions, architecture, and signing/notarization status.
2. Download the final distributable installers from that release. Use the
   Windows x64 setup `.exe`, Apple Silicon `.dmg`, and Intel `.dmg` as available.
   Preserve their contents and existing signatures.
3. Complete the validation checklist below. Do not assume that passing a build
   job verifies installation, persistence, or upgrading.
4. In **this public repository**, open **Releases → Draft a new release**.
5. Create or select a tag in this distribution repository and set a clear title,
   such as `Stagehand 0.2.0`. A public tag can use `v0.2.0` even if the internal
   release uses `v_0_2_0`; state the actual app version clearly. Do not push private
   source history here to create the public tag.
6. Write public release notes using the template below. Review the text instead
   of copying private release notes or commit messages unchanged.
7. Attach the approved installers. Keep architecture labels in the filenames;
   Apple Silicon and Intel disk images must have distinct names. Use those exact
   filenames in the release notes.
8. Generate SHA-256 checksums for the final installer files, save them in
   `SHA256SUMS.txt`, and attach it. Generate checksums after signing and
   notarization; do not alter installers afterward.
9. Mark preview builds as **pre-release**. For a stable release, set the appropriate
   latest-release status. Check the notes and assets in the draft, then publish.
10. Verify downloads in a signed-out browser. Test both the release page and, for
    a stable latest release, the README's `/releases/latest` link.

GitHub automatically offers source-code archives for the public repository's
tag. Those should contain only this distribution repository's public files.
Do not attach private source archives, build artifacts containing source, debug
symbols, credentials, `.env` files, database contents, or internal logs.

## Validate before publication

- [ ] Actual app version agrees with the public title and release notes.
- [ ] Each advertised architecture has the correct installer asset.
- [ ] Supported Windows/macOS versions are recorded from testing; do not infer
      support solely from a build runner or a configured minimum OS version.
- [ ] Fresh installation works on each advertised platform and architecture.
- [ ] The installed app includes the matching database executable and starts
      without developer tools or a separate SurrealDB installation.
- [ ] Windows setup supplies WebView2 when absent, including the intended
      offline installation path.
- [ ] A test campaign, note, and attachment survive a complete quit and restart.
- [ ] Updating from the previous public version retains campaigns and attachments.
- [ ] Any supported internal-to-public upgrade has also been tested.
- [ ] Database migrations, backup requirements, and downgrade limitations are
      described in the release notes.
- [ ] Signing/notarization status and expected first-launch prompts are stated
      accurately. Do not describe a build as signed or notarized without checking.
- [ ] Required third-party notices and applicable binary distribution terms are
      included with the distribution, including those for bundled dependencies.
- [ ] Final installer checksums match the published checksum entries.
- [ ] Public notes, filenames, and attachments have been reviewed for private data.
- [ ] Signed-out users can download every advertised asset after publication.

## Public release notes template

Replace every bracketed field and remove sections that do not apply. Do not
publish unfilled placeholders.

```markdown
## Stagehand [app version]

[Brief description of this release and its intended audience.]

### Downloads and compatibility

| Platform | Installer filename | Tested OS versions |
| --- | --- | --- |
| Windows x64 | [exact .exe filename] | [versions] |
| macOS Apple Silicon | [exact .dmg filename] | [versions] |
| macOS Intel | [exact .dmg filename] | [versions] |

### Changes

- [User-visible change or fix.]

### Installation and updates

- Installation guides: [Windows](https://github.com/Brinnys-Better-Bucklers/stagehand-release/blob/main/docs/INSTALL_WINDOWS.md), [macOS](https://github.com/Brinnys-Better-Bucklers/stagehand-release/blob/main/docs/INSTALL_MACOS.md).
- [Update and backup guide](https://github.com/Brinnys-Better-Bucklers/stagehand-release/blob/main/docs/UPDATING.md).
- Supported upgrade paths: [previous versions, including any internal versions].
- Database changes and special migration steps: [details, or none].
- Rollback compatibility: [details and whether a pre-update backup is required].

### Signing and download verification

- Windows signing: [verified status and publisher if signed].
- macOS signing/notarization: [verified status and developer if signed].
- SHA-256 checksums: see the attached SHA256SUMS.txt.

### Known issues

- [Issue and workaround, or none known from validation.]
```

## Future automated publication

Keep compilation and source checkout in the private repository. A separately
configured publishing step can upload only approved distributables, checksums,
and reviewed release notes to this repository. It needs credentials with release
write access to the public destination; the private repository's default workflow
token should not be assumed to grant access to another repository. Keep those
credentials in private workflow secrets, and scope them to the destination.

Do not add a public workflow that checks out the private application's source
or prints private build configuration. Any automation should preserve internal
release behavior as needed and explicitly select the public destination.
