# LightNews workflow 交接

這是供下一位開發者或 AI agent 閱讀的**公開、去識別交接包**，不是完整可部署的 n8n 備份。請先閱讀 [HANDOFF.md](HANDOFF.md) 和 [TODO.md](TODO.md)。

## 必須先知道

- 原始 workflow 含大量內嵌歷史、實際文章、執行證據、人工修補登錄、內網位址及本機設定，不能直接放進公開 Git。
- `workflows/` 保留已驗證快照的節點結構、連線和可安全保留的小型程式碼。所有節點都設為 disabled，workflow 設為 inactive。
- 私有設定與無法安全完整拆開的大型節點已移除，用明確拋錯的佔位程式代替。**不要直接匯入後全選啟用。** 每個遺漏節點都列在 `docs/*-omissions.json`。
- 本包不是對線上版本的修改，也不聲稱去識別 JSON 與原始版本位元相同。原始快照版本與 SHA-256 在 `manifest.json`；公開檔案另有 `SHA256SUMS`。
- 02、03、05 尚無本次確認為最新的完整匯出，未以舊版或實驗檔冒充。
- `src/` 是自然文章 v1 的程式片段（core／renderer 為函式；review 是依賴既有 crFresh 系列的整合片段，不可單獨執行）；不是 rev3 候選，也不代表自然文章全流程已通過實測。

## 目錄

- `HANDOFF.md`：現況、限制、操作交接和驗收標準。
- `TODO.md`：建議下一步與完成條件。
- `AGENTS.md`：後續 AI agent 必讀約束。
- `manifest.json`：已知正式快照來源狀態、版本、雜湊及缺件。
- `workflows/`：五個已去識別、停用的結構參考快照。
- `src/`：自然中文生成 schema、渲染函式及依賴既有基底的審查整合片段。
- `scripts/validate_public_bundle.py`：公開包結構／隱私／停用檢查。
- `docs/`：節點省略清單與本包檢查結果。

## 驗證

```sh
python3 scripts/validate_public_bundle.py
node scripts/test_natural_core.cjs
node scripts/check_node_syntax.cjs
node --check src/natural-core.js
node --check src/natural-renderer.js
node --check src/natural-review.js
```

這些檢查只驗證公開包，不會呼叫模型、網站、n8n、Unsplash 或寫入任何歷史檔，也不等於線上端對端成功。交接時應先取得獲授權的私人原始匯出，再在私有環境補齊設定和被省略的程式。不得將憑證或私人紀錄加回公開 repo。
