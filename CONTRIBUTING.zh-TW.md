# 貢獻說明

你可以新增地區、新增語言，或只改正一句話。每個修改都是一個 Pull Request，檢查會自動跑，告訴你哪裡要改。English: `CONTRIBUTING.md`。

## 新增或修改地區

1. 把 `templates/region.json` 複製成 `regions/<代號>.json`。代號是小寫英文字母（可用連字號），最多 24 個字元，而且要跟檔名一樣（`tw.json` 裡寫 `tw`）。要改現有的地區，直接在 GitHub 上編輯那個檔就好。
2. 照下表填欄位。`en`（英文）與 `zh`（正體中文）都要寫。只會其中一種的話，另一種盡量寫，並在 `notes` 說明，維護者會整理。
3. 如果你不是當地人，維持 `"status": "draft"`（見下面「草稿與當地人看過」）。送出 Pull Request。

字數以字元計算。兩個數字時，前面是英文、後面是中文。

| 欄位 | 是什麼 | 上限 |
|---|---|---|
| `schema` | 固定是 `1` | |
| `code` | 地區代號，跟檔名一樣 | 24 |
| `countries` | 這個地區的國家，兩個字母的小寫 ISO 代碼。一個國家只能屬於一個地區 | 30 個國家 |
| `name` | `en`、`native`（當地人怎麼寫）、`zh` | 各 40 |
| `lang` | 主要語言，要用 [Gemini Live 官方清單](https://firebase.google.com/docs/ai-logic/live-api/limits-and-specs)上的代碼，例如 `en-US`、`ja-JP`、`th-TH`。中文只有 `cmn` | |
| `layer` | 選填。跟哪個語言資料夾共用。不寫就取 `lang` 的前半（`en-US` 用 `languages/en`） | |
| `stt` | 選填。聽的語言，只有跟 `lang` 不同才寫（例如說英文的地區填 `hi-IN`） | |
| `other_langs` | 選填。當地也聽得到的其他語言 | 4 個代碼 |
| `chinese_dialects` | 只有台灣、香港、澳門、中國大陸、新加坡、馬來西亞組成的地區才能填 `true` | |
| `hello` | 當地人怎麼打招呼，用當地語言：`hello` 與 `hello_again`。語言不在 Bageo 九種介面語言內時要填；非英語地區的國家不在 Bageo 自己的國家表內時也要填。不能含 `{owner}` | 30 與 60 |
| `delivery` | 包裹放哪裡 | 80 / 36 |
| `delivery_key` | 選填。那個地點的短詞，`en` 與 `zh` | 12 |
| `readback` | 電話號碼、時間、星期怎麼唸 | 80 / 36 |
| `fraud` | 當地常見的詐騙。英文要含 scam，中文要含「詐騙」 | 110 / 50 |
| `habits` | 跟隔壁地區真的不一樣的用詞與習慣 | 420 / 190，跟語言資料夾的合計 |
| `stall_local` | 陪詐騙來電時，可以卡住的日常狀況 | 150 / 70，跟語言資料夾的合計 |
| `talk_style` | `persona`（本人）與 `assistant`（助理），各有 `"1"` 到 `"5"` 五格，從隨興（1）到俐落公事（5） | 每格 200 / 90 |
| `vocab` | 選填。依情境分類的詞，例如 `"bank": ["card reader"]`。情境名稱用 `[a-z_]`，2 到 16 個字元 | 8 種情境、每種 6 個詞、每詞 24 字元 |
| `status` | `draft`（草稿）或 `local_reviewed`（當地人看過） | |
| `reviewed_on` | 日期 `YYYY-MM-DD`，`local_reviewed` 時必填，不能是未來的日子 | |
| `notes` | 選填。工作筆記，打包時會拿掉 | 1000 |

地區跟語言資料夾合併後，還有兩個合計上限。包裹、唸法、詐騙、習慣，加上最長的一格講話風格：英文最多 430、中文最多 410。詐騙加上卡關細節：最多 220 與 470。

每格講話風格要寫三件事：怎麼稱呼人、句子多長、熱絡程度。第 3 格一定要寫「對方講完一件事，用一句完整的話回應，不只回一兩個字」。每格最多三個例詞，用當地語言，結尾寫「每次換說法」。`{owner}` 代表主人的名字，只有講話風格那幾格可以用。

## 新增或修改語言資料夾

把 `templates/language-call.json` 複製成 `languages/<代號>/call.json`。資料夾名稱就是語言代碼（`es`、`th`、`cmn`），裡面的 `layer` 要一樣。只填這種語言的所有地區都共用的內容，地區檔就不用重複寫。

兩邊怎麼合併：地區的 `delivery`、`readback`、`fraud`、`hello`、`stt` 會取代語言資料夾的；`habits` 與 `stall_local` 是語言資料夾的文字接上地區的；講話風格逐格取代；詞彙是聯集，地區的詞排前面。

語言資料夾自己的上限比較小：`habits` 200 / 90、每格講話風格 120 / 55。`name` 有 `en` 與 `zh`（各 40）。其他欄位的上限跟地區一樣。

## 寫作原則

- 只給方向，不寫台詞。講處境和感覺，讓 AI 用自己的話說。不要寫逐字的句子，也不要規定固定的步驟順序。
- 不重複固定規則。Bageo 本來就禁止給驗證碼與個資、答應轉帳、替主人答應事情、叫對方等一下，這些不用再寫。
- 只提到 Gemini Live 支援的語言（看官方清單）。不要點名清單上沒有的方言或腔調，也不要要求 AI 只用一種語言回答。
- 錢、商店、日期、數字用當地人的說法，但不放真的網址、電話、email、真人姓名，也不要連續 6 位以上的數字。號碼寫成樣式，例如 06 xx xx xx xx。
- 寫短。只放當地真的不一樣的，到處都一樣的就不寫。

## 翻譯 Bageo 的文字

Bageo 的通知、控制台與電腦版程式，可以翻成 Gemini Live 清單上的任何語言（手機 APK 的多語字串直接內建於 `bageo-call`）。每種語言有一個資料夾：`languages/<代號>/`。

1. 英文原文在 `source/en`，不要改它。`source/meta` 寫了每一句出現在哪裡、給誰看，照它選合適的語氣。
2. 譯文放進你那種語言的資料夾：`notify.json`（通知訊息）、`console.json`（網頁控制台）、`desktop.json`（電腦版程式）、`names.json`（這種語言自己的名稱，複製 `templates/language-names.json`）。key 要跟英文檔一樣。
3. 佔位符都要保留，例如 `{n}`、`{name}`、`{}`、`%1$s`。可以搬到你的語言需要的位置，但不能多、不能少、不能改名。
4. 固定用詞每次都照 `source/glossary.json`。「Bageo」不翻。
5. 不放網址、email、電話，也不要連續 6 位以上的數字，除非英文那句本來就有。
6. `_review.json` 裡每一句有一個 `status`：`ai_draft`（AI 寫的，還沒人看過）、`ai_checked`（翻回英文，意思沒跑掉）、`needs_fix`（意思不對）、`local_reviewed`（當地人看過）。
7. 你是當地人，讀過某一句、改好或確認沒問題，就把那一句標成 `local_reviewed`，並在 `on` 寫今天的日期（`YYYY-MM-DD`）。一個檔的狀態取最低的那一句，所以每一句都看過，整個檔才算 `local_reviewed`。
8. 送出 Pull Request 前先跑檢查（見「在自己電腦上檢查」），要沒有任何問題。

## 草稿與當地人看過

新內容一開始是 `draft`（草稿）：還沒有當地人看過。Bageo 裡會標示它是草稿。

只有在你住在那個地區（或那種語言是你的母語）、讀過這個檔每一個欄位、而且符合當地人真正的說法時，才把 `status` 改成 `local_reviewed`，`reviewed_on` 填今天的日期，並在 Pull Request 勾選對應的方塊。如果你不是當地人卻改了已看過的檔案的文字，要改回 `draft`。

地區與它的語言資料夾合併時，取兩者中較低的狀態。檢查程式只確認有填日期；看過是不是真的，由維護者讀 Pull Request 時判斷。

## 在自己電腦上檢查

不一定要做，每個 Pull Request 都會自動檢查。想先檢查的話，需要裝 Rust 與 git：

```
git clone https://github.com/h4lo-void/bageo-call
cd bageo-call
git checkout <tools/bageo-call.ref 裡寫的 commit>
cargo run -p bageo-packs --release -- check <這個資料夾的路徑>
```

通過時只有一行：`ok: N region(s), M language layer(s)`。沒通過的話，每一行會寫出檔案、欄位、規則代號和哪裡不對，最後一行是問題總數。規則代號：R01 格式或多出的欄位、R02 代號、R03 國家、R04 語言、R05 缺欄位、R06 長度、R07 佔位符、R08 網址、電話或 6 位數字、R09 禁用的句子、R10 不支援的語言或腔調、R11 中文方言設定、R12 狀態或日期、R13 索引、R14 換行、隱藏字元或括號、R15 發布索引。

## Pull Request 會跑什麼

`Check` 工作流程在每個 Pull Request 與每次推送時執行。它會取得這個 repo，以及 `h4lo-void/bageo-call` 裡的檢查程式（`tools/bageo-call.ref` 指定的那個 commit），對整個資料夾跑上面的指令。要通過才能合併。維護者也會讀每個修改，因為沒有任何檢查能分辨「看起來正常、其實教錯了」的內容。

## 授權同意

送出 Pull Request 時，你在表單勾選同意：你的資料與翻譯以 CC0-1.0 釋出，腳本以 Apache-2.0 釋出。不用另外簽任何文件。

## 給維護者

`bageo-call` 的檢查規則改了，就另開一個 Pull Request 把新的 commit 寫進 `tools/bageo-call.ref`。要發布時推送像 `v2026112101` 的 tag，Release 工作流程會做完其餘的事。
