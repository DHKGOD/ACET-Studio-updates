# Release maintenance

Canonical repository: `DHKGOD/Arduino-Simulator`.

Public downloads: https://github.com/DHKGOD/Arduino-Simulator/releases/latest

Signed update feed: https://dhkgod.github.io/Arduino-Simulator/acet-update.json

## Preserve installed clients

- Keep the same signing key and internal `ACETStudio` product identifier.
- Keep existing Release tags and asset names. Repository branding does not change the updater protocol or Windows installation identity.
- Do not create another repository named `DHKGOD/ACET-Studio-updates`: GitHub redirects the old repository and Release URLs to this repository. Reusing that name would disable the redirects relied upon by installed clients.
- GitHub Pages project URLs do not redirect after a repository rename. New signed manifests must use the canonical Pages download URL, with the canonical GitHub Release asset URL as a mirror.
- Publish matching signed `acet-update.json` to both Pages and the latest Release. Upload and verify packages before advertising a new version.
- Test the legacy feed URL `https://github.com/DHKGOD/ACET-Studio-updates/releases/latest/download/acet-update.json`, signature verification, package download and SHA256 after publishing.
- Existing clients retaining the old repository preference can reach the canonical Release through GitHub's redirect. New builds should normalize the old preference to the canonical repository and use canonical Pages first.

Fresh installations use the complete Setup.exe. Existing installations use the small signed update and preserve user workspaces and preferences.

## Cross-version upgrade contract (from 1.7.9)

- Keep cumulative small packages containing the latest app, helper, ScintillaNET, fonts/licenses, runtime headers and Worker.cpp. Current verified minimum is 1.6.1.
- Both installer types embed the guard and owned-file inventory. The guard must run before replacing files even for legacy clients.
- Do not uninstall or purge an old installation before replacing files. Retain AppId, per-user privileges and UsePreviousAppDir.
- A small package needs a usable bundled toolchain; incomplete or unsupported bases select a separately signed full envelope embedded in the manifest. The full envelope must have the same target version and packageType=full. Publish acet-update-full.json as well.
- Verify the new app using isolated data, bundled compiler and GPIO simulation before committing. Restore backup files and uninstall registration on failure. Keep journal/recovery tools if cleanup or recovery cannot finish.
- Test legacy helper jumps (1.6.1, 1.7.3, previous version), fresh install, prior-install path detection, deliberately failed health, incomplete toolchain, interrupted journal, source-data preservation and signed published downloads.
- These tests do not guarantee recovery from hardware loss or a destroyed backup. Never silently delete a failed backup or user's workspaces.
