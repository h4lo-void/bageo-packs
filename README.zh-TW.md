# bageo-packs

[Bageo](https://github.com/h4lo-void/bageo-call) 的公開資料與資源資料庫：各地講電話的方式、多語翻譯、各國詐騙資料庫、語音包台詞與小動畫圖案。Bageo 主程式只保留 9 種核心語言與基本引擎，其餘地區與擴充資源都隔離在這裡，讓安裝檔保持精簡並讓各地使用者都能貢獻。

目前多數檔案仍是 AI 草稿（`draft`／`ai_checked`），經當地人讀過確認後才改標為 `local_reviewed`。如果你住在當地或熟悉某種語言，幫忙審閱就是最大的貢獻。

English: [README.md](README.md).

## 裡面有什麼

- `regions/<代號>.json`：一個地區一個檔（目前 74 區）。國家、語言、包裹習慣、號碼與時間唸法、當地用詞、本人與助理各 5 格講話風格，以及陪聊細節。
- `languages/<代號>/`：額外語言與共通層（70 種譯語）。包含 `call.json`、`names.json`、`notify.json`、`desktop.json`、`console.json` 與 `_review.json`（手機 APK 的多國語言已直接內建於 `bageo-call` 的 APK 中）。
- `art/<地區>.json`：64 區非內建八哥小動畫 SVG 資料，控制台在該區通過審閱後按需下載。
- `scams/`：隔離出來的各國電信詐騙資料（`country_scams.json` 與 `countries/<國碼>.json`，共 112 國）與核心九語以外的詐騙／正常來電關鍵字（`keywords.json`）。
- `voices/`：各地區語音包試聽／拒接台詞（`lines.json`）與語音包索引（`bageo-voices-index.json`）。
- `source/`：英文原文、說明與固定用詞表（`glossary.json`）。請勿直接改這裡（原文由 `bageo-call` 同步）。
- `templates/`：新增地區、語言或名稱檔的範本。

## 三步幫忙

1. 在 GitHub 打開對應地區或語言的檔案（例如 `regions/tw.json` 或 `languages/it/notify.json`），按編輯修改內容；新增地區可複製 `templates/region.json`。
2. 送出 Pull Request，檢查流程會自動驗證格式與翻譯規則並列出說明。
3. 在 Pull Request 表單勾選授權同意與是否為當地母語者，等待維護者審閱合併。

細節見 [CONTRIBUTING.zh-TW.md](CONTRIBUTING.zh-TW.md)。

## Bageo 怎麼使用

Bageo 主程式內建核心基準；其餘語言文字、地區小動畫、語音包與更新資料都在你於控制台啟用或按下更新時，才從這個資料庫的 GitHub Release 下載，並用同一套檢查規則在本機驗證後才生效。

維護者推送 `vYYYYMMDDNN` 格式的 tag（例如 `v2026112101`）即可自動建置全套資料包與索引檔並附在 Release 中。

## 授權

資料、圖檔與翻譯：[CC0-1.0](LICENSE)（公眾領域）。

工作流程與腳本（`.github/` 與 `tools/`）：Apache-2.0，見 [LICENSE-scripts](LICENSE-scripts)。
