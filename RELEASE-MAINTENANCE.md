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
