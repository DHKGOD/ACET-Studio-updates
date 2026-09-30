# Arduino Simulator

Arduino Simulator（原 ACET Studio）是 Windows 桌面程式，可編寫、編譯及練習 Arduino 程式，並模擬 Corvette-F1／ACET 板的 LED、按鍵、七段顯示器、LCD 等功能。

## 下載與安裝

**第一次使用，請到 [Releases 最新版本](https://github.com/DHKGOD/Arduino-Simulator/releases/latest)，展開 Assets，下載 `ACET_Studio_Setup_版本號.exe` 完整安裝檔。**

1. 開啟上方的 Releases 連結。
2. 在 **Assets** 中選擇檔名含 **`Setup`** 的 `.exe`，例如 `ACET_Studio_Setup_1.7.7.exe`。
3. 下載完成後執行安裝檔，依畫面指示完成安裝。
4. 從開始功能表或桌面捷徑開啟 **Arduino Simulator**。

安裝檔已內附所需編譯工具與執行環境，無需另外安裝 Arduino IDE、Java 或 Python。適用於 **Windows 10／11 64 位元**。

> GitHub 的 **Code → Download ZIP**、**Source code (zip)** 和 **Source code (tar.gz)** 都不是完整安裝檔。第一次安裝請下載 **Setup.exe**。

## 已安裝的使用者如何更新？

在程式內開啟 **設定 → 檢查更新**，依提示下載並安裝新版。網路更新會保留工作區、程式文件與設定。

| Release 檔案 | 用途 |
|---|---|
| `ACET_Studio_Setup_版本號.exe` | 完整安裝檔，供新使用者安裝 |
| `ACET_Studio_Update_版本號.exe` | 已安裝程式使用的小型更新套件；建議透過程式內更新功能安裝 |
| `acet-update.json` | 程式自動讀取的更新資訊，使用者無需手動操作 |

## 第一次使用

開啟 **設定 → 互動新手導覽**，即可跟著畫面上的指示線了解工作區、程式編輯、編譯、模擬與更新功能。

桌面模擬不是 CPU 週期級模擬；精密硬體時序仍需在實際板子上確認。

---

Copyright © 2026 dhkgodez. All rights reserved.
