# 喔！這裡還有一點

這個 repo 保存書稿、章卡、原始故事、人物與生命素材、校閱／修訂記錄、寫作 skills，以及獨立書稿閱讀器。

- [當前狀態與交接](docs/book-v2-handoff.md)
- [書名與篇章名定案](docs/book-v2-titles.md)
- [寫作流程](docs/book-v2-workflow.md)
- [回饋與修訂索引](manuscript/_feedback/README.md)
- [repo 分拆與來源](docs/repo-split.md)

## 閱讀器

```bash
cd reader
npm ci
npm run build
npm run reader
```

預設開啟 `http://127.0.0.1:4178/`；手機同網段預覽使用 `npm run reader:phone`。閱讀器只讀 `manuscript/NN-*.md`，共十六篇；`reader/dist/` 是可直接託管的靜態產物。閱讀器的註解目前關閉，既有資料格式與儲存 key 保留。

## 維護

先讀 [AGENTS.md](AGENTS.md) 與 [CLAUDE.md](CLAUDE.md)。既有正文局部修稿使用 `.agents/skills/rui-xuan-book-v2/`，先核對現稿與 diff；整章是否可提交依作者明確確認，歷史回饋不等於現稿定稿。
