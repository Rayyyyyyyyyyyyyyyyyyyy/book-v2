# Repository Guidelines

本 repo 專責《喔！這裡還有一點》。架構與機制見 [CLAUDE.md](CLAUDE.md)，當前稿件狀態見 [docs/book-v2-handoff.md](docs/book-v2-handoff.md)。

## 來源與工作分工

- `manuscript/` 保存持續修訂的正文，一章一檔，共十六篇；`_continuity.md` 記跨章事實與資訊邊界，`_feedback/` 保存回饋與修訂來源。
- `docs/chapter-v2/` 是現行章卡，`docs/chapter.md` 只是舊路徑索引；`docs/my-story/` 是作者提供的原始故事與藍圖，不能直接覆蓋現稿。
- 回饋從 [manuscript/_feedback/README.md](manuscript/_feedback/README.md) 進入。新增或搬移記錄時更新所屬索引與引用；分類、固定來源檔與用法見 workflow。
- `materials/` 是私人素材與人物參考，供寫作取材，不由閱讀器發布。人物分析來自多個時期與關係，不能自行混入男主角或女主角的故事。
- `reader/` 是獨立書稿閱讀器；只載入 `manuscript/NN-*.md`，不載入素材、連續性、回饋或規劃檔。
- `openspec/` 保存本書寫作與閱讀器規格／變更。較大功能調整同步相關規格與 change。

## 寫作與校閱

處理本書正文、人物、章節或跨章問題，使用 [rui-xuan-book-v2](.agents/skills/rui-xuan-book-v2/SKILL.md)。先辨認使用者要提供回饋、整理本書材料還是寫作；貼上隨筆不等於要求改寫。討論人物時用「男主角／女主角」，不替人物取名字；正文按既有視角與人稱。

直接修改 `manuscript/*.md`，包括只改幾句、採用回饋或作者裁定，執行 skill 的 [正文直改分支](.agents/skills/rui-xuan-book-v2/references/book-v2-direct-edit.md)。同輪讀當前正文與相關 diff，依問題補讀章卡、回饋或跨章記錄；取材深度隨修改範圍調整，不設逐字引文門檻。流水線步驟按 prompt 取材。

作者自 2026-09-23 起取消「手改句一律不動」的限制。手改是聲音與取捨證據，可為閱讀體驗再修；修改可確認的親筆句時，記錄原句、改後句、來源與理由，交作者校閱，不把未核准修稿當定稿。

## 定稿與 Git

「第 N 章看完／改完／改好了」啟動整章與 diff 評讀，不等於核准定稿或提交。若同時請求修稿，處理已可確認的問題。只有明確「這章 OK／可以定稿／同意提交」，才依 [workflow](docs/book-v2-workflow.md) 的七步完成：核對定稿、同步事實、迭代修稿偏好、核實手改來源、更新字數與狀態、精準提交、回報。只核准局部就只套用局部，不擴大成整章核准。

逐一指定提交檔案，不用 `git add -A` 夾帶未校閱章節。Commit 使用簡短祈使英文主旨；包含可確認的作者親筆改句時含 `hand edit`，首次整章入庫不加。Git 新增行只作來源候選，以手改對照與校閱紀錄核實。

搬移前的 commit、整檔指紋與舊路徑是歷史來源；先查 [repo 分拆記錄](docs/repo-split.md)，不要把本次初始入庫的整章新增行當作者新手改。

## 建置與驗證

在 `reader/` 執行：

```bash
npm ci
npm run build
npm run reader
npm run reader:phone
```

本機預設 `127.0.0.1:4178`，可用 `READER_PORT` 調整；phone 綁 `0.0.0.0`。提交前跑 `npm run build`，確認十六篇、章名與順序；閱讀器互動修改另核對桌面／行動版、閱讀進度與註解匯出入。註解目前關閉，開關在模板 `NOTES_ENABLED`，既有 localStorage key 與資料格式維持不變。

JavaScript 使用兩格縮排、雙引號與分號。不要提交 `reader/dist/`、`node_modules/`、密鑰或 `.env`。閱讀器只發布正文，素材與流程檔不得放入靜態產物。
