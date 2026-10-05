# CLAUDE.md

共用規則先讀 [AGENTS.md](AGENTS.md)。本 repo 維護《喔！這裡還有一點》的敘事、修訂與書稿閱讀器；讀書心得網站另有自己的 repo 與 skills。

## 書稿來源

正文在 `manuscript/`，序章 00、第一至十三章 01–13、結語 14、後記 15，共十六篇。只有 `NN-*.md` 進閱讀器；`_continuity.md`、`_feedback/` 與 `materials/` 不發布。正式書名與篇章名決議見 [命名紀錄](docs/book-v2-titles.md)。

章卡在 `docs/chapter-v2/`；歷史原稿在 `docs/my-story/`；當前事實由 `manuscript/_continuity.md` 維護。作者校閱、局部修訂與跨章診斷從 [回饋索引](manuscript/_feedback/README.md) 查找，歷史章號與字數不能當成當前正文。

## 閱讀器建置

`reader/scripts/manuscript-reader.mjs` 讀正文與 HTML 模板，以 `@astrojs/markdown-remark` 產生 `reader/dist/index.html` 與 `sw.js`。產物是 gitignored，每次建置重生；`--serve` 在本機開 HTTP server，`--phone` 使用 `0.0.0.0`。

閱讀區段、導覽與 localStorage 對應維持數字章號 `section-NN`，檔名只用來定位來源。持續使用既有註解／偏好／進度 key 與 JSON 版本；搬移網站網址會改變瀏覽器 origin，舊 origin 的本機資料不會自動移過來。註解目前以 `NOTES_ENABLED = false` 關閉。

## 寫作流水線與 skills

流程見 [docs/book-v2-workflow.md](docs/book-v2-workflow.md)，由 `docs/book-v2-pipeline.sh` 驅動：寫作 → 讀者 → 編輯 → 潤飾 → 稽核。每步使用新的 `codex exec` session（目前 `gpt-5.6-sol`、high），限時 30 分鐘；log 在 `~/.cache/book-v2-logs/`，可用 `BOOK_V2_LOG` 改。

腳本從自身位置解析 repo 根目錄，不依賴舊 checkout。正文、回饋與素材路徑分別是 `manuscript/`、`manuscript/_feedback/`、`materials/`。

| Skill | 分工 |
|---|---|
| `rui-xuan-book-v2` | 本書敘事與後記聲音、直接修稿、人物時間分層與校閱流程 |
| `ai-reader` | 依當前正文試讀；刻意不先讀章卡與作者診斷 |
| `ai-editor` | 對照原稿判讀閱讀障礙、修改價值與人物基準 |
| `openspec-*` / `source-command-opsx-*` | 本書相關規格與變更流程 |

Skills 位於 `.agents/skills/`；流水線寫作、擴寫及潤飾指定 `rui-xuan-book-v2`，稽核不掛聲音 skill。手改抽取只定位新 repo 的 Git 候選；搬移前來源需核對固定手改檔與作者校閱，不用初始入庫判斷親筆。

## 分拆與發布

2026-10-05 從原專案分拆，詳見 [docs/repo-split.md](docs/repo-split.md)。本 repo 的 standalone reader 可由 `.github/workflows/deploy.yml` 建置發布到 GitHub Pages；Pages 必須設定為 GitHub Actions。只有正文、閱讀器或 workflow 變動會觸發發布。
