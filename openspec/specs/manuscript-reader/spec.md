# Manuscript Reader Specification

## Purpose

定義《喔！這裡還有一點》獨立書稿閱讀器的來源、靜態產物、安裝與本機預覽，以及章節與讀者資料格式的相容性；僅發布十六篇正文，不依賴讀書心得網站，也不把素材、回饋或章卡混入閱讀器。

## Requirements

### Requirement: 書稿來源與靜態產物

系統 SHALL 從 `manuscript/00–15` 的 `NN-*.md` 取得十六篇，依數字順序產生 `reader/dist/index.html` 與 service worker；缺篇時 SHALL 明確失敗。正文之外的素材、章卡、回饋與連續性 SHALL NOT 進靜態產物。

#### Scenario: 只發布正文

- **WHEN** 建置閱讀器
- **THEN** 產物 SHALL 包含依序排列的十六篇正文，且不得包含 materials、章卡、回饋或連續性

### Requirement: 獨立安裝與預覽

`reader/` SHALL 有獨立 package manifest 與 lockfile，`npm ci` 後可 `npm run build`、`npm run reader`、`npm run reader:phone`。不得讀取另一個 repo 或依賴其 node_modules。

#### Scenario: 單獨 checkout 與執行

- **WHEN** 只 checkout 本 repo，在 reader 執行 npm ci 與 npm run build
- **THEN** 建置 SHALL 成功，且 reader 指令 SHALL 可在本機提供頁面

### Requirement: 既有讀者資料格式

系統 SHALL 保持數字章節 ID、現有 localStorage key 與註解 JSON 格式。註解關閉狀態保持；不同 origin 的 localStorage 不視為已自動移轉。

#### Scenario: 更新閱讀器保留資料相容性

- **WHEN** 讀者在相同 origin 載入搬移後的閱讀器
- **THEN** 系統 SHALL 繼續使用既有資料格式與章號，不因檔案目錄改變而重新定義儲存格式
