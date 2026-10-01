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

## 1.7.10 起必做的核心完整性檢查

1. 更新套件必須是累積核心套件，不可只放版本號或本次修改的單一檔案。維護 upgrade-files-small.txt，涵蓋所有可變核心元件。
2. 完成 Release stage 的主程式、更新器、模擬核心、README 等檔案更新後，執行 Build_ReleaseCore.ps1 -Stage <stage> -Inventory <small inventory> -Version <version>，產生 core-integrity.json。之後若改動其中檔案，必須重新產生清單並重新封裝、簽章。
3. 小型及完整安裝器都必須內嵌同一清單，並安裝至原位置。UpgradeGuard Prepare 記錄內嵌清單 SHA256；VerifyInstalled 對照版本、清單本身及每個核心檔案，全部通過後才執行健康檢查與 Commit。失敗回復舊版，不將殘缺安裝標為成功。
4. 每次發布至少實測最舊支援版本 1.6.1 和上一公開版本升級，核對每個核心檔案，並測試缺漏／過時元件拒絕及回復。完整安裝測試需使用隔離位置與私人資料，保護實際登錄和工作區。
5. 更新來源保持 canonical GitHub Pages 優先，GitHub Release 為備援；先部署套件並核對下載 SHA256，公開 Release 後才切換 acet-update.json，避免公告早於檔案到位。

清單目前涵蓋 17 個可變核心元件。大型不變 SDK 工具鏈仍以基底支援與健康檢查判定；缺少必要基底時應選完整修復套件。
