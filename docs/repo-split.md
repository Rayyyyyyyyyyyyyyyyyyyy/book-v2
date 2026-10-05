# Repo 分拆｜2026-10-05

作者要求原 repo 保留讀書心得，將本書相關內容完整移入 `/Users/ray.shao/book-v2/`，skills 一併分拆。搬移來源是 `book-reader` 的 `1e50cca`；本次不改十六篇故事內容、篇章順序、作者核准範圍或字數，只有路徑、規則分工與閱讀器包裝改變。

| 原位置 | 本 repo 的位置 |
|---|---|
| `book-reader/book-v2/` | `manuscript/`，包含 `_continuity.md` 與完整 `_feedback/` |
| `docs/` 的書稿流程、章卡、原始故事、研究及決策 | `docs/`，保留原分類與日期來源 |
| `book-reader/is-me/story-base.txt` | `materials/story-base.txt` |
| 人物分析與生命素材 | `materials/` 的獨立快照；原 repo 保留心得與隨筆用的素材 |
| `site/scripts/manuscript-reader*` | `reader/scripts/`，建置至 `reader/dist/` |
| 三個本書 OpenSpec changes | `openspec/changes/`，保留歷史設計與任務狀態 |
| `rui-xuan-book-v2`、讀者與編輯角色 | 本 repo 的 `.agents/skills/`，只負責書稿；心得使用原 repo 的 `rui-xuan-reading` |

## 來源與 Git 歷史

原 `book-reader` repo 的 Git 歷史保留，搬移前的 commit ID、作者手改、整檔指紋與 diff 仍屬原 repo。新 repo 的初始入庫不是作者新寫整章；不可因整章新增就標記為 hand edit。可透過原 repo 的 GitHub commit 或本機 checkout 查歷史，例如：

```bash
git -C /Users/ray.shao/book-reader show fe43eb4:book-reader/is-me/Rui-Xuan.md
```

已儲存的 `manuscript/_feedback/全書-手改對照.md`、作者校閱與修訂檔是本 repo 可獨立取用的來源。流水線不依賴原 repo 執行；讀書心得與網站也不再依賴本書。

## 發布與讀者資料

原網站建置不再產生書稿頁，獨立閱讀器的靜態產物只有十六篇正文及 service worker；素材、回饋與章卡不進產物。新 repo 的 GitHub Pages workflow 獨立建置 `reader/`；Pages Source 使用 GitHub Actions。若 Pages 尚未啟用，workflow 仍建置並保存靜態 artifact，略過部署；此 repo 分拆未替使用者開啟新的 Pages 站點。

註解 JSON 格式、localStorage key 與數字章節 ID 不改。不同 origin 的瀏覽器儲存不會自動轉移：換網址前可在舊頁匯出註解 JSON，在新頁啟用註解後匯入；閱讀進度與顯示偏好需在新網址重新設定。不宣稱來源網址的資料已搬入新 origin。

六個原已失效的歷史文件／本機產物連結保留原路徑文字並標示缺席，不用重新產生的截圖冒充舊驗收。

## 本輪驗證

- 搬移前逐檔 SHA-256 複製核對：273 份來源檔案全數有去處；兩份心得專用 skill reference 留在原 repo 的新閱讀 skill，其餘搬移或分拆到本 repo。
- 十六篇正文逐檔位元組一致，篇章順序與全書 88,896 字維持；163 份回饋與修訂記錄完整保留。
- 讀書心得網站的 121 份 src 檔、111 張原封面、15 份心得草稿逐檔一致；移除書稿建置後 npm run build 成功，產物不再包含 manuscript。
- 獨立 reader 的 npm ci、npm run build 成功，依賴版本與原 lockfile 相同；本機 HTTP 頁面與 service worker 可讀，十六篇與六個新章名正確，素材／章卡／回饋不在產物中。
- 從 /tmp 啟動 pipeline 的 audit 路徑檢查通過：使用 codex stub，只驗證新 repo 根目錄與稿件路徑，未執行模型、未修改正文。
- 兩邊六個核心 skills 的 quick_validate 通過；兩邊本地 Markdown 文件連結有效。本 repo 的 OpenSpec 全量 strict 驗證四項通過；心得 repo 的 site-delivery strict 通過，原 book-catalog Purpose 過短的既有 warning 保留，未擴大本次修改。
- 新 repo 遠端原先沒有 branch，GitHub Pages 尚未啟用；本輪不開啟新的站點。
